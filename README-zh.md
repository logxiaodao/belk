# 功能实现
* 使用 filebeat + logstash + elasticsearch + kibana 收集日志

# 服务启动
* 修改.env文件来设置版本及账户
* 修改 docker-compose.yml 来设置elk、filebeat的启动配置 
* 启动服务
    1. docker compose up  -d
    1. 打开你的kibana web服务 http://localhost:5601
    
# filebeat 服务配置
* 修改 filebeat.yml文件 中的 output.logstash
    1. docker exec -it ${logstash CONTAINER ID} sh
    1. cat /etc/hosts
    1. 将读取到的 ip 替换成 output.logstash 中的 ip
    1. 将要收集的日志放到filebeat挂载的文件中【已配置filebeat/in-logs】，并在logstash中配置对应的filters(过滤规则)
  

# 日志收集建议
* 怎么查找日志？
  1. 使用 requestID 作为唯一标识来查找日志
  2. 通过 userId + 接口路由地址 作为唯一标识来查找日志
* 应该记录那些日志？
  1. http的 request and response
  2. 程序报错：空指针错误、堆栈溢出、下标越界等
  3. 持久化数据的变更
  4. 异常的用户行为