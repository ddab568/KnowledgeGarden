
### Domain Name System (DNS)

The phonebook of the internet. Translates domain names into their corresponding IP addresses e.g. www.mywebsite.com will direct to the an IP address such as 192.0.2.1. DNS will find the associated IP address and direct your request to the appropriate server

Some examples of DNS services are Cloudflare DNS, Route 53 (AWS), Google Cloud DNS.

### Load Balancer

A load balancer is responsible for distributing network requests across servers to ensure optimal resource utilization, reduce latency and maintain high availability. The requirement for a load balancer depends on the scale of the architecture and the requirement for fault tolerance.  AWS Example: Elastic Load Balancer

![Load balancer](/vault/assets/images/load-balancer.png)
[source](https://codeburst.io/load-balancers-an-analogy-cc64d9430db0)

### API Gateway 
An API Gateway is a server or service which acts as a single entry point for clients to access various microservices or backend services. It can handle routing, authentication, request transformation, rate limiting and caching. It is well suited to when multiple microservices need a single entry point as it helps centralise concerns such as routing, security and monitoring. 

Examples of API gateways: Amazon API Gateway, Apigee, NGINX

### Content Delivery Network (CDN)

A distributed network of servers that store and deliver content such as images, videos, stylesheets and scripts to users from locations which are geographically closer to them. 