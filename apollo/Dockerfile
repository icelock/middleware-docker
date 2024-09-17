FROM mysql:8.0
COPY sql/apolloconfigdb.sql docker-entrypoint-initdb.d/
COPY sql/apolloportaldb.sql docker-entrypoint-initdb.d/

# 当前使用的apollo版本是，apollo-sql:2.1.0
# apollo-mysql:latest
# docker build -f Dockerfile -t apollo-mysql:latest .


