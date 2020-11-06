## The pillars of the AWS Well-Architected Framework

|Name | Description | Design Principles |
|-|-| - |
| Operational Excellence  | The ability to support development and run workloads effectively, gain insight into their operations, and to continuously improve supporting processes and procedures to deliver business value.  | <ul style="width:300px"><li>Perform operation as code</li><li>Make frequent small reversible changes</li><li>Refine operation procedures frequently</li><li>Anticipate failures</li><li>Learn from all operational failures</ul> |
| Security | The security pillar encompasses the ability to protect data, systems, and assets to take advantage of cloud technologies to improve your security. | <ul><li>Implement a strong identity foundation</li><li>Enable traceability</li><li>Apply security at all layers</li><li>Automate security best practices</li><li>Protect data in transit and at rest</li><li>Keep people away from data</li><li>Prepare for security events</ul> |
| Reliability | The reliability pillar encompasses the ability of a workload to perform its intended function correctly and consistently when it’s expected to. This includes the ability to operate and test the workload through its total lifecycle. This paper provides in-depth, best practice guidance for implementing reliable workloads on AWS. | <ul><li>Automatically recover from failure</li><li>Test recovery procedures</li><li>Scale horizontally to increase aggregate workload availability</li><li>Stop guessing capacity</li><li>Manage change in automation</ul> |
| Performance Efficiency | The ability to use computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve. | <ul><li>Democratize advanced technologies</li><li>Go global in minutes</li><li>Use serverless architectures</li><li>Experiment more often</li><li>Consider mechanical sympathy</ul> |
| Cost Optimization | The ability to run systems to deliver business value at the lowest price point. | <ul><li>Implement Cloud Financial Management</li><li>Adopt a consumption model</li><li>Measure overall efficiency</li><li>Stop spending money on undifferentiated heavy lifting</li><li>Analyze and attribute expenditure</ul> |
| | |


* Component - Code, config, AWS resource that together delivers against a requirement.
* Workload - A set of components that together delivers business value.
* Architecture - Is about how component work together in a workload. How components interact and communicates.
* Milestones - Mark key changes in the architecture as it evolves throughout the product lifecycle.
* Technology Portfolio - Within an organization is a collection of workloads.