Spring Boot 2.x 集成 Elasticsearch

### 步骤一：运行 docker 容器
1.下载镜像：
```
docker pull elasticsearch:6.5.4
```
2.创建容器（9200：Elasticsearch 对外提供的web端口，9300：Elasticsearch 内部使用的端口）：
```
docker run -it -p 9200:9200 -p 9300:9300 elasticsearch:6.5.4
```
3.本地访问：
```
http://localhost:9200/
```

### 步骤二：集成 Elasticsearch
1.pom.xml 引入依赖
```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-elasticsearch</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```
2.application.properties 配置
```
spring.data.elasticsearch.cluster-nodes=localhost:9300
spring.data.elasticsearch.cluster-name=docker-cluster
```
3.下载谷歌浏览器扩展程序：https://chrome.google.com/webstore/detail/elasticsearch-head/ffmkiejjmecolpfloofpjologoblkegm ，并在浏览器中打开

4.测试 controller/BlogController.java 中的各个接口（使用 Postman 或 [SwaggerUI](http://localhost:8080/swagger-ui.html)(推荐)），并在 elasticsearch-head 浏览器扩展程序中查看结果

### 步骤三：返回 JSON 数据的封装
1.参考：http://blogspring.cn/view/391

### 步骤四：全局异常处理
1.参考：http://blogspring.cn/view/397

### 注意点
1. 添加记录时，如果 blogModel 实体参数中没有 id 字段，即数据没有自然的 ID， Elasticsearch 可以帮我们自动生成 ID；此时，blogModel 中的 id 为 null，_id 为自动生成的 ID，查询、更新、删除时，可以使用此自动生成的 ID。参考：https://www.elastic.co/guide/cn/elasticsearch/guide/cn/index-doc.html#index-doc

### 参考

参考资料 | 网址
--- | ---
Elasticsearch实战篇——Spring Boot整合ElasticSearch | https://segmentfault.com/a/1190000018625101
学习SpringBoot（二）：Spring Boot 返回 JSON 数据及数据封装 | http://blogspring.cn/view/391
学习SpringBoot（八）：Spring Boot 中的全局异常处理 | http://blogspring.cn/view/397