# WAF (Web Access Firewall)
* AWS Firewall Manager simplifies your administration and maintenance tasks across multiple accounts and resources for 
    * AWS WAF
    * AWS Shield Advanced
    * Amazon VPC security groups
    * AWS Network Firewall

![](https://d1.awsstatic.com/Solutions/Solutions%20Category%20Template%20Draft/Solution%20Architecture%20Diagrams/waf-security-automations-architecture.520fa104475cd846b62df3b2027a64094dfad31a.png)

* Firewall Manager provides these benefits:
    * Helps to protect resources across accounts
    * Helps to protect all resources of a particular type, such as all Amazon CloudFront distributions
    * Helps to protect all resources with specific tags
    * Automatically adds protection to resources that are added to your account
    * Allows you to subscribe all member accounts in an AWS Organizations organization to AWS Shield Advanced, and automatically subscribes new in-scope accounts that join the organization
    * Allows you to apply security group rules to all member accounts or specific subsets of accounts in an AWS Organizations organization, and automatically applies the rules to new in-scope accounts that join the organization
    * Lets you use your own rules, or purchase managed rules from AWS Marketplace

* At the simplest level, AWS WAF lets you choose one of the following behaviors:
    * Allow all requests except the ones that you specify – This is useful when you want Amazon CloudFront, Amazon API Gateway, Application Load Balancer, or AWS AppSync to serve content for a public website, but you also want to block requests from attackers
    * Block all requests except the ones that you specify – This is useful when you want to serve content for a restricted website whose users are readily identifiable by properties in web requests, such as the IP addresses that they use to browse to the website.
    * Count the requests that match the properties that you specify – When you want to allow or block requests based on new properties in web requests, you first can configure AWS WAF to count the requests that match those properties without allowing or blocking those requests. This lets you confirm that you didn't accidentally configure AWS WAF to block all the traffic to your website. When you're confident that you specified the correct properties, you can change the behavior to allow or block requests.
* Using AWS WAF has several benefits:
    * Additional protection against web attacks using conditions that you specify. You can define conditions by using characteristics of web requests such as the following:
        * IP addresses that requests originate from
        * Country that requests originate from
        * Values in request headers
        * Strings that appear in requests, either specific strings or string that match regular expression (regex) patterns
        * Length of requests
        * Presence of SQL code that is likely to be malicious (known as SQL injection)
        * Presence of a script that is likely to be malicious (known as cross-site scripting)
    * Rules that can allow, block, or count web requests that meet the specified conditions. Alternatively, rules can block or count web requests that not only meet the specified conditions, but also exceed a specified number of requests in any 5-minute period.
    * Rules that you can reuse for multiple web applications
    * Managed rule groups from AWS and AWS Marketplace sellers
    * Real-time metrics and sampled web requests
    * Automated administration using the AWS WAF API


## What Should I Choose? ** WAF | AWS Shield | AWS Firewall Manager **
It all starts with AWS WAF. You can automate and then simplify AWS WAF management using AWS Firewall Manager. Shield Advanced adds additional features on top of AWS WAF, such as dedicated support from the DDoS Response Team (DRT) and advanced reporting.

If you want granular control over the protection that is added to your resources, AWS WAF alone is the right choice. If you want to use AWS WAF across accounts, accelerate your AWS WAF configuration, or automate protection of new resources, use Firewall Manager with AWS WAF.

Finally, if you own high visibility websites or are otherwise prone to frequent DDoS attacks, you should consider purchasing the additional features that Shield Advanced provides.