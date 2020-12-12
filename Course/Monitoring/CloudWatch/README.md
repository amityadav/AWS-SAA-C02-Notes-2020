# CloudWatch
* CloudWatch has available Amazon EC2 Metrics for you to use for monitoring. 
* CPU Utilization identifies the processing power required to run an application upon a selected instance. 
* Network Utilization identifies the volume of incoming and outgoing network traffic to a single instance. 
* Disk Reads metric is used to determine the volume of the data the application reads from the hard disk of the instance. This can be used to determine the speed of the application. 
* There are certain metrics that are not readily available in CloudWatch such as **memory utilization, disk space utilization**, and many others which can be collected by setting up a custom metric.


You need to prepare a custom metric using CloudWatch Monitoring Scripts which is written in Perl. You can also install CloudWatch Agent to collect more system-level metrics from Amazon EC2 instances. Here's the list of custom metrics that you can set up:

- Memory utilization
- Disk swap utilization
- Disk space utilization
- Page file utilization
- Log collection

![](https://img-a.udemycdn.com/redactor/raw/2019-02-13_00-48-03-503799cd694a657201456b3add758b53.png?f_eRSdPtGKo1fw6aXDQ8dbIFcdf1HkQUY5Rf2630972Pjvc9asuxJL_P_p7N82f2RdHfQZd6zry4XBHR6vntxTTgOP3tqrdGA2Nlx1gOtmO0u7gFD_Tyzd_Bbb2UHeDckOqVTFyHlfuvRki85NCFLcsHLM9o9kXw1App9oP0KQ6_LNbv)