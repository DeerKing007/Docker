## Ubuntu 下安装Elasticsearch Docker镜像

#### 拉取镜像

```shell
docker pull elasticsearch:7.6.2
```

#### 创建挂载的目录

```shell
mkdir -p /mydata/elasticsearch/config
mkdir -p /mydata/elasticsearch/data
echo "http.host: 0.0.0.0" >> /mydata/elasticsearch/config/elasticsearch.yml
```

#### 创建容器并启动

```shell
docker run --name elasticsearch -p 9200:9200 -p 9300:9300  -e "discovery.type=single-node" -e ES_JAVA_OPTS="-Xms64m -Xmx128m" -v /mydata/elasticsearch/config/elasticsearch.yml:/usr/share/elasticsearch/config/elasticsearch.yml -v /mydata/elasticsearch/data:/usr/share/elasticsearch/data -v /mydata/elasticsearch/plugins:/usr/share/elasticsearch/plugins -d elasticsearch:7.6.2
```

*其中elasticsearch.yml是挂载的配置文件，data是挂载的数据，plugins是es的插件，如ik，而数据挂载需要权限，需要设置data文件的权限为可读可写,需要下边的指令*

```shell
chmod -R 777 /mydata/elasticsearch/data
```

*-e "discovery.type=single-node" 设置为单节点*

##### 特别注意：

*-e ES_JAVA_OPTS="-Xms256m -Xmx256m" \ 测试环境下，设置ES的初始内存和最大内存，否则导致过大启动不了ES*



#### 访问：http://自己的IP地址:9200





## Ubuntu 下安装Kibana Docker镜像

#### 拉取镜像

```shell
docker pull kibana:7.6.2
```

#### 启动镜像

```shell
docker run --name kibana -e ELASTICSEARCH_HOSTS=http://自己的IP地址:9200 -p 5601:5601 -d kibana:7.6.2
```

#### 进入容器修改相应内容

```shell
server.port: 5601
server.host: 0.0.0.0
elasticsearch.hosts: [ "http://自己的IP地址:9200" ]
i18n.locale: "Zh-CN"
```



#### 访问：http://自己的IP地址:5601/app/kibana





