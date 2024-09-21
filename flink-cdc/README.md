（1）在mysql中创建表：

CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100),
    email VARCHAR(100)
);


（2）进入job-manager，打开flink sql：

./bin/sql-client.sh


（3）创建flink表：

CREATE TABLE mysql_source (
    id INT,
    name STRING,
    email STRING,
    PRIMARY KEY(id) NOT ENFORCED
) WITH (
    'connector' = 'mysql-cdc',
    'hostname' = 'mysql',
    'port' = '3306',
    'username' = 'root',
    'password' = 'root',
    'database-name' = 'test_db',
    'table-name' = 'users',
    'debezium.snapshot.mode' = 'initial'
);


（4）验证表数据是否正常：

select * from mysql_source;

（5）创建es索引：

PUT /users_index
{
    "mappings": {
        "doc": {
            "properties": {
                "id": { "type": "integer" },
                "name": { "type": "text" },
                "email": { "type": "keyword" }
            }
        }
    }
}

（6）创建flink表：

CREATE TABLE es_sink (
    id INT,
    name STRING,
    email STRING,
    PRIMARY KEY(id) NOT ENFORCED
    ) WITH (
        'connector' = 'elasticsearch-6',
        'hosts' = 'http://elasticsearch:9200',
        'index' = 'users_index',
        'document-type' = 'doc',
        'format' = 'json'
);

（7）启动数据流：

INSERT INTO es_sink SELECT * FROM mysql_source;