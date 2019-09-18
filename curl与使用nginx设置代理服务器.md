# curl与使用nginx设置代理服务器

1.curl 使用

curl -l -H "Content-type: application/json" -H "Authorization: 722dc60db2bb49aeab8259b3eea5b93f" -X POST -d '{"id_num":"1174224626667466752","name":"DADAN SURYAMAN","id_type":99}' http://161.117.111.34:8888/authorize_api/createReportTask


2.使用nginx设置代理服务器

    resolver      8.8.8.8;
    server {
       listen 8888;
       location / {
           proxy_pass http://$http_host$request_uri;
       }
    }
    
3. 重启 nginx sudo nginx -s reload

   1.注意, resolver是必填的

4.测试

import urllib.request

import urllib.parse

req_url = "http://www.baidu.com"

proxy_addr = "163.204.240.138:8090"

def use_proxy(req_url, proxy_addr):

    proxy = urllib.request.ProxyHandler({"http": proxy_addr})
    
    opener = urllib.request.build_opener(proxy, urllib.request.HTTPHandler)
    
    urllib.request.install_opener(opener)
    
    data = urllib.request.urlopen(req_url).read().decode("utf-8", "ignore")
    
    return data
    
data = use_proxy(req_url, proxy_addr)

print(len(data))



5.国内免费代理IP

  https://www.xicidaili.com/
  
