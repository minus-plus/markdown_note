## docker+python+django+redis 配置
最近在做一个项目,用django框架,redis做缓存.遇到了一个问题,如何部署redis呢.在dockerfile中我install了redis-server:
```sh
FROM ubuntu:14.04
RUN apt-get update -y && apt-get install -y libpq-dev \
                                            python-dev \
                                            ssh \
                                            redis-server

RUN apt-get install -y python-setuptools
RUN easy_install pip
ADD requirements.txt /src/requirements.txt
RUN cd /src; pip install -r requirements.txt

# Copy source code
ADD . /src
RUN mkdir -p /var/log/django
EXPOSE 8000
CMD ["/src/start.sh"]
```
运行docker image的时候,首先要启动redis-server,我是这么做的:
`start.sh`
```sh
#!/bin/bash
redis-server
python /src/manage.py runserver 0.0.0.0:8000
```
结果运行后一直停留在redis-server界面.查了很多资料一直没找到答案,最后终于发现这个界面特妈跟我linux系统运行的界面一样啊.在terminal中运行redis-server之后你就不能运行别的了.事实证明早界面ctrl + c之后运行了下一条命令了....   
很多帖子说redis-server默认开机运行的,但在docker中却不一样,docker run APP_IMAGE后,redis-server并没有启动,需要用`service redis-server restart`重启,否则redis client连接不上.  
我改成了这样:
```sh
#!/bin/bash
service redis-server restart  #重启redis-server
echo "redis-server started .."
echo "runserver .."
python /src/manage.py runserver 0.0.0.0:8000
```
python如何连接redis呢?  
```
$ pip install redis
```
```
import redis
redis_client = redis.Redis(host="localhost", port=6379, db=0)
redis_client.get(KEY)
redis_client.set(KEY, VALUE)
```
最后view.py代码很简单:

```python
# views.py
from django.shortcuts import render
from django.http import HttpResponse
import redis
import socket

# Create your views here.

def request_handler(request):
	count = get_count()
	html = "Welcome to the homepage! You'v been here %s times!" % count;
	return HttpResponse(html);

def get_count():
	redis_client = redis.Redis(host="localhost", port=6379, db=0)
	count = redis_client.get("count")
	if count == None:
		count = 1
	else:
		count = int(count) + 1
	redis_client.set("count", count)
	return count
```
### It works!!!
***
**END**

