# AWS SWF
* Amazon SWF helps developers build, run, and scale background jobs that have parallel or sequential steps. You can think of Amazon SWF as a fully-managed state tracker and task coordinator in the Cloud.


## Amazon SWF Functionality
Using Amazon SWF to manage workflows within your application is easy. Amazon SWF acts as the coordination hub for all of the different components of your application:

* Maintaining application state
* Tracking workflow executions and logging their progress
* Holding and dispatching tasks
* Controlling which tasks each of your application hosts will be assigned to execute

![](https://dmhnzl5mp9mj6.cloudfront.net/bigdata_awsblog/images/Wangechi_Workflow_Image_2.png)

| Feature | Amazon SWF | AWS Data Pipeline | AWS Lambda |
|---|---|---|---|
| Runs in response to | Anything | Schedules | Events from AWS services/direct invocation |
| Execution order | Orders execution of application steps |  Schedules data movement | Reacts to event triggers / Direct calls |
| Scheduling | On-demand | Periodic | Event-driven / on-demand / periodic |
| Hosting environment | Anywhere | AWS/on-premises | AWS |
| Execution design | Exactly once | Exactly once, configurable retry | At least once |
| Programming language | Any | JSON | Supported languages|