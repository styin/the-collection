![[6 Pillars of WAF.png]]
##### 1. Operational Excellence
1. Perform operations as code 
	- (IaC - Infrastructure as Code) via [[AWS CloudFormation]]
2. Make frequent, small, reversible changes
	- Incremental changes
3. Refine operations procedures frequently
	- continuous improvement
4. Anticipate failures
	- monitoring via [[Amazon CloudWatch]]
5. Learn from all operational failures
##### 2. Security
1. Implement a strong identity foundation
	- [[AWS Identity and Access Management (IAM)]]
2. Maintain traceability
	 - [[AWS CloudTrail]]
1. Apply security at all layers
	- [[Amazon Inspector]]
	- [[AWS Trusted Advisor]]
1. Automate security best practices
2. Protect data in transit and at rest
3. Keep people away from data
4. Prepare for security events
##### 3. Reliability
1. Automatically recover from failure
	- disaster recovery
1. Test recovery procedures
2. Scale horizontally to increase aggregate workload availability
	- via [[Elastic Load Balancer]]
3. Stop guessing capacity
	- Automatic Scaling via [[Elastic Load Balancer]]
4. Manage change in automation
	 - Intelligent Tiering for [[Amazon S3]]
##### 4. Performance Efficiency
1. Democratize advanced technologies
2. Go global in minutes
	- [[Amazon CloudFront]]
3. Use serverless architectures
	 - [[AWS Lambda]]
1. Experiment more often
2. Consider mechanical sympathy
	- understanding how tools/systems operate the best
##### 5. Cost Optimization
1. Ability to run systems and deliver business value at the lowest price point
##### 6. Sustainability
1. Understand your impact
2. Establish sustainability goals
3. Maximize utilization
4. Anticipate and adopt new, more efficient hardware and software offerings
5. Use managed services
6. Reduce the downstream impact of your cloud workloads