## nginx

nginx是一个开源且高性能、可靠的HTTP中间件和代理服务器

#### 一些概念

**正向代理**：通过自己的电脑访问服务器a通过a访问网站b，a就是代理服务器，这种访问方式是正向代理，特点是明确的知道访问那个网站。

**反向代理**：当有一个服务器集群，并且内容一样，我们通过一个第三方服务器来访问这个集群的方式就是反向代理，此时我们并不知道我们访问的是那个服务器。

**负载均衡**：访问压力较大时建立服务器集群，用户访问网站实现访问一个中间服务器，中间服务器在请求时选择压力较小的服务器，以保证每个服务器的压力基本平衡，避免崩溃的情况。

nginx是通过反向代理实现的负载均衡，用户会首先访问到nginx服务器，nginx服务器再选择压力较小的服务器进行访问，如果其中一个服务器崩溃了，将会从待选服务器中删除。

#### HTTP Upstream模块

nginx服务器的一个重要模块，实现在客户端ip之间轮询实现后端的负载均衡，常用指令：ip_hash，server，upstream等

ip_hash：若用户已经访问了fuwuqia并且登陆，那么第二次请求会通过哈希算法自动定位到改后台服务器

server：指定服务器的名称和参数（比如权重）

upstream：用于设置一组可以在proxy_pass和fastcgi_pass指令中使用的代理服务器，默认负载均衡方式是轮询

#### 其他负载均衡方式

#### 部署NodeJS上线步骤

jc99-101

