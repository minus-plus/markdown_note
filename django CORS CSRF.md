## CORS - Cross-origin resource sharing 
[Detailed information of CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS)
CORS-Application of domain-A request resourse in belongs to domain-B.
The Cross-Origin Resource Sharing (CORS) mechanism gives web servers cross-domain access controls, which enable secure cross-domain data transfers. Modern browsers use CORS in an API container - such as XMLHttpRequest or Fetch - to mitigate risks of cross-origin HTTP requests.
Sometimes, when you send a http request using certain module, you may get CORS error. 
## Enable CORS in AWS apiGateway
Sometimes CORS errors might be raised when you send a request in your html page to other domain of yours. To deal with this error, set Access-Control-Allow-Origin header in your target domain. 
In django:
```
# diange set headers with response[header_key] = header_value
response = HttpResponse("DATA")
response["Access-Control-Allow-Origin"] = * # to set Access-Control-Allow-Origin to all
OR
response["Access-Control-Allow-Origin"] = "YOUR ORINGIN DOMAIN"
return response
```
In AWS API:
Enable CORS in the target API method

## CSRF - Cross-Site Request Forgery
[Detailed information of CSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)_Prevention_Cheat_Sheet)
[CSRF attack](https://segmentfault.com/a/1190000006963312)
This problem was encountered when I post AWS SQS messages to crawl_server. web server通过tocken或cookie进行身份验证，但SQS将message post到crawl server时无法处理server返回的cookie或tocken，在http请求中也无法将cookie或tocken添加到请求中。
## how to solve CRSF problem
The simplest way is unable CSRF middleware to make csrf authentication ineffective for all request. But this method is not recommended because it is dangerous. 
Some post in StackOverflow use the following method to exempt scrf authentication for specific request handler, but it is not works for me. 
```
from django.views.decorators.csrf import csrf_exempt
@csrf_exempt
def handler(request):
    ...
```
