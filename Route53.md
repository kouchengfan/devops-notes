### Route 53

**Route 53** is a managed DNS which is a collection of rules and records to help clients reach servers using urls. the most common records are A: url to Piv4, AAAA URL to IPPv6, CNAME for url to url and Alias utl to aws resource. Route 53 can work with public or private domains. It also has load balancing using DNS not IP, called client side load balancing, health checks and routing policies based on geolocation, failover, latency,etc. Use Alias instead of CNAME because it is faster.
