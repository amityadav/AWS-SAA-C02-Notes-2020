# CHAPTER 5 | Route53

## DNS

_You won't be questioned in the exam about the next sections (up to ALIAS record).
It's just for your knowledge and very good for better understanding the course._

### [What's DNS](https://www.cloudflare.com/learning/dns/what-is-dns/)

The Domain Name Systems (DNS) is the phonebook of the Internet. Humans access information online through domain names, like nytimes.com or espn.com. Web browsers interact through Internet Protocol (IP) addresses. DNS translates domain names to IP addresses so browsers can load Internet resources.

### [IPv4 vs IPv6](https://www.guru99.com/difference-ipv4-vs-ipv6.html)

* IPv4 is a 32-Bit IP Address.
* IPv6 is 128 Bit IP Address and was created to fulfil the need for more Internet addresses.

### [Top Level Domains:](https://en.wikipedia.org/wiki/Top-level_domain)

A top-level domain is one of the domains at the highest level in the hierarchical Domain Name System of the Internet (```.com``` ```.net``` ```.org``` as an example).

In the case of ```.co.uk```, ```.co``` is the second level domain and ```.uk``` is the top level domain

### [SOA Record](https://en.wikipedia.org/wiki/SOA_record)

A Start of Authority record (abbreviated as SOA record) is a type of resource record in the Domain Name System (DNS) containing administrative information about the zone, especially regarding zone transfers.

Example of a SOA record

```bash
$ dig SOA +multiline google.com

[...]
;; ANSWER SECTION:
google.com.        55 IN SOA ns1.google.com. dns-admin.google.com. (
                238640061  ; serial
                900        ; refresh (15 minutes)
                900        ; retry (15 minutes)
                1800       ; expire (30 minutes)
                60         ; minimum (1 minute)
                )
[...]
```

### [NS Record](https://www.cloudflare.com/learning/dns/dns-records/dns-ns-record/)

NS stands for 'name server' and this record indicates which DNS server is authoritative for that domain (which server contains the actual DNS records)

```bash
$ dig NS google.com

[...]

;; ANSWER SECTION:
google.com.        2073    IN    NS    ns4.google.com.
google.com.        2073    IN    NS    ns1.google.com.
google.com.        2073    IN    NS    ns2.google.com.
google.com.        2073    IN    NS    ns3.google.com.

[...]
```

### [A Record](https://www.cloudflare.com/learning/dns/dns-records/dns-a-record/)

The ‘A’ stands for ‘address’ and this is the most fundamental type of DNS record, it indicates the IP address of a given domain

```bash
$ dig A google.com

[...]

;; ANSWER SECTION:
google.com.        62    IN    A    216.58.201.14

[...]
```

### [TTL, Time to Live](https://en.wikipedia.org/wiki/Time_to_live#DNS_records)

When a caching (recursive) nameserver queries the authoritative nameserver for a resource record, it will cache that record for the time (in seconds) specified by the TTL.

### [CNAME Record](https://support.dnsimple.com/articles/cname-record/)

CNAME records can be used to alias one name to another. CNAME stands for Canonical Name.

A common example is when you have both example.com and www.example.com pointing to the same application and hosted by the same server.

```bash
$ dig www.dnsimple.com

[...]

;; ANSWER SECTION:
www.dnsimple.com.    3595    IN    CNAME    dnsimple.com.
dnsimple.com.        55    IN    A    104.245.210.170

[...]
```

CNAME can't be used on the root domain. (This is a contractual limitation imposed by the RFC 1912 and RFC 2181, not a technical one.)

### [ALIAS record](https://support.dnsimple.com/articles/alias-record/)

An ALIAS record is a virtual record type we created to provide CNAME-like behaviour on apex domains.
For example, if your domain is example.com and you want it to point to a hostname like myapp.herokuapp.com, you can’t use a CNAME record, but you can use an ALIAS record. The ALIAS record will automatically resolve your domain to one or more A records at resolution time, and resolvers see your domain simply as if it had A records.

In AWS you have to use ALIAS records to point your root domain to other DNS records such as your ELB.

Amazon Route 53 alias records provide a Route 53–specific extension to DNS functionality. Alias records let you route traffic to selected AWS resources, such as CloudFront distributions and Amazon S3 buckets. They also let you route traffic from one record in a hosted zone to another record.

Unlike a CNAME record, you can create an alias record at the top node of a DNS namespace, also known as the zone apex. For example, if you register the DNS name example.com, the zone apex is example.com. You can't create a CNAME record for example.com, but you can create an alias record for example.com that routes traffic to www.example.com.

## DNS IN AWS

### [Routing policies available in AWS](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy.html)

* Simple routing policy: Use for a single resource that performs a given function for your domain. You can have 1 record with multiple addresses.
* Weighted routing policy: Use to route traffic to multiple resources in proportions that you specify. You can send 40% of the traffic on one IP and 60% to another IP.
* Latency routing policy: Use when you have resources in multiple AWS Regions and you want to route traffic to the region that provides the best latency.
* Failover routing policy: Use when you want to configure active-passive failover.
You need to create a health check before.
* Geolocation routing policy: Use when you want to route traffic based on the location of your users.
* Multivalue answer routing policy: Use when you want Route 53 to respond to DNS queries with up to eight healthy records selected at random.
* Geoproximity routing policy: Use when you want to route traffic based on the location of your resources and, optionally, shift traffic from resources in one location to resources in another.

A zone apex record (example.com v/s www.example.com) can be pointed to the following services using AWS Route 53 Alias record and using the name of the following services instead of IP address.
* a load balancer  
* a website hosted on S3
* CloudFront distribution
* AWS Elastic Beantalk
* Amazon API Gateway
* Amazon VPC endpoint


Q. Can I have a Geo DNS record for a continent and different Geo DNS records for countries within that continent? Or a Geo DNS record for a country and Geo DNS records for states within that country?
---
Yes, you can have Geo DNS records for overlapping geographic regions (e.g., a continent and countries within that continent, or a country and states within that country). For each end user’s location, Route 53 will return the most specific Geo DNS record that includes that location. In other words, for a given end user’s location, Route 53 will first return a state record; if no state record is found, Route 53 will return a country record; if no country record is found, Route 53 will return a continent record; and finally, if no continent record is found, Route 53 will return the global record.

Q. What is the difference between Latency Based Routing and Geo DNS?
---
Geo DNS bases routing decisions on the geographic location of the requests. In some cases, geography is a good proxy for latency; but there are certainly situations where it is not. LatencyBased Routing utilizes latency measurements between viewer networks and AWS datacenters. These measurements are used to determine which endpoint to direct users toward.

If your goal is to minimize end-user latency, we recommend using Latency Based Routing. If you have compliance, localization requirements, or other use cases that require stable routing from a specific geography to a specific endpoint, we recommend using Geo DNS.

Q. What is Private DNS?
---
Private DNS is a Route 53 feature that lets you have authoritative DNS within your VPCs without exposing your DNS records (including the name of the resource and its IP address(es) to the Internet.

Q. What happens if all of my endpoints are unhealthy?
---
Route 53 can only fail over to an endpoint that is healthy. If there are no healthy endpoints remaining in a resource record set, Route 53 will behave as if all health checks are passing.


What does Amazon Route53 provide?
---
* A global Content Delivery Network.
* None of these.
* **A scalable Domain Name System**
* An SSH endpoint for Amazon EC2.

Does Amazon Route 53 support NS Records?
---
* Yes, it supports Name Service records.
* No
* It supports only MX records.
* **Yes, it supports Name Server records.**

Does Route 53 support MX Records?
---
* **Yes**
* It supports CNAME records, but not MX records.
* No
* Only Primary MX records. Secondary MX records are not supported.

Which of the following statements are true about Amazon Route 53 resource records? Choose 2 answers
---
* **An Alias record can map one DNS name to another Amazon Route 53 DNS name.**
* A CNAME record can be created for your zone apex.
* **An Amazon Route 53 CNAME record can point to any DNS record hosted anywhere.**
* TTL can be set for an Alias record in Amazon Route 53.
* An Amazon Route 53 Alias record can point to any DNS record hosted anywhere.

Which statements are true about Amazon Route 53? (Choose 2 answers)
---
* Amazon Route 53 is a region-level service
* **You can register your domain name**
* **Amazon Route 53 can perform health checks and failovers to a backup site in the even of the primary site failure**
* Amazon Route 53 only supports Latency-based routing

A customer is hosting their company website on a cluster of web servers that are behind a public-facing load balancer. The customer also uses Amazon Route 53 to manage their public DNS. How should the customer configure the DNS zone apex record to point to the load balancer?
---
* Create an A record pointing to the IP address of the load balancer
* Create a CNAME record pointing to the load balancer DNS name.
* Create a CNAME record aliased to the load balancer DNS name.
* **Create an A record aliased to the load balancer DNS name**

A user has configured ELB with three instances. The user wants to achieve High Availability as well as redundancy with ELB. Which of the below mentioned AWS services helps the user achieve this for ELB?
---
* **Route 53**
* AWS Mechanical Turk
* Auto Scaling
* AWS EMR

How can the domain’s zone apex for example “myzoneapexdomain com” be pointed towards an Elastic Load Balancer?
---
* By using an AAAA record
* By using an A record
* By using an Amazon Route 53 CNAME record
* By using an Amazon Route 53 Alias record

You need to create a simple, holistic check for your system’s general availability and uptime. Your system presents itself as an HTTP-speaking API. What is the simplest tool on AWS to achieve this with?
---
* **Route53 Health Checks (Refer link)**
* CloudWatch Health Checks
* AWS ELB Health Checks
* EC2 Health Checks

Your organization’s corporate website must be available on www.acme.com and acme.com. How should you configure Amazon Route 53 to meet this requirement?
---
* ***Configure acme.com with an ALIAS record targeting the ELB. www.acme.com with an ALIAS record targeting the ELB.***
* Configure acme.com with an A record targeting the ELB. www.acme.com with a CNAME record targeting the acme.com record.
* Configure acme.com with a CNAME record targeting the ELB. www.acme.com with a CNAME record targeting the acme.com record.
* Configure acme.com using a second ALIAS record with the ELB target. www.acme.com using a PTR record with the acme.com record target.


