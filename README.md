Nacos Docker仓库

## 外置数据库单节点集群运行
#### 1. 修改.env<br/>
```
# example/.env
NACOS_VERSION=v2.3.0
MYSQL_ROOT_PASSWORD=1009
```
为了正确载入compose.yaml中的${}变量
#### 2. 修改compose文件
`example/cluster-hostname.yaml`<br/>
mysql的test修改为
```
test: [ "CMD", "mysqladmin" ,"ping", "-h", "localhost", "-u", "root", "-p${MYSQL_ROOT_PASSWORD}" ]
```
#### 3. 按需修改
按需修改`example/cluster-hostname.yaml`以及它们的env文件

#### 4.运行
在根目录运行`docker-compose -f example/cluster-hostname.yaml up`
