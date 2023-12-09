Nacos Docker仓库

## 外置数据库单节点集群运行
#### 1. 修改.env<br/>
```
# example/.env
NACOS_VERSION=1.4.2
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

## nginx反向代理，负载均衡
```bash
docker run -id --name=nacos_nginx ^
-p 80:80 ^
-v C:\Users\mumu\IdeaProjects\nacos-docker\nginx\nginx.conf:/etc/nginx/nginx.conf ^
-v C:\Users\mumu\IdeaProjects\nacos-docker\nginx\conf.d\default.conf:/etc/nginx/conf.d/default.conf ^
-v C:\Users\mumu\IdeaProjects\nacos-docker\nginx\logs:/var/log/nginx ^
-v C:\Users\mumu\IdeaProjects\nacos-docker\nginx\html:/usr/share/nginx/html ^
--network example_default ^
nginx:stable
```