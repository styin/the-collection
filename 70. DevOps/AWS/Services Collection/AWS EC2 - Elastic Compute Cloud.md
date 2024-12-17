---
aliases:
  - EC2
  - AWS EC2
---
### Amazon EC2 - Cloud Compute Capacity - AWS

#### Amazon EC2 Instance Types
1. General Purpose
	- balances compute, memory, networking resources
	- ideal for diverse workflows:
		- Application Backend
		- Small-Medium Databases
2. Compute Optimized
	- ideal for compute-intensive tasks:
		- Gaming
		- Scientific Modeling
3. Memory Optimized
	- ideal for memory-intensive tasks
4. Accelerated Computing
	- high-performance GPUs, hardware accelerators, co-processors
	- ideal for deep-learning tasks, and also:
		- floating point calculations
		- graphics processing
		- data pattern matching
5. Storage Optimized
	- high-performance local storage -> high IOPS
	- ideal for data tasks:
		- distributed file systems
		- data warehousing
		- high-frequency online transaction processing (OLTP)
6. HPC Optimized
	- high-performance workflows at scale

#### Amazon EC2 Pricing Options
1. On-Demand Pricing
	- Pay-as-you-go
	- Billed for the duration the instance is running
	- fixed instance size, fixed instance family
2. Savings Plan
	- Committed consistent usage over a 1 year or 3 year term.
	- instance size and family not specified
	- instance region not specified
	- no capacity reservation -> no guarantee in times of high demand
3. Reserved Instances
	1. Standard Reserved Instances
		- fixed instance size, fixed instance family
		- fixed instance OS, tenancy, region 
    2. Convertible Reserved Instances
	    - instance size and family not specified
	    - instance availability zone not specified
	- full upfront payment
	- partial upfront payment
	- no upfront payment
4. Spot Instances
	- Reclaimable workload
	- 2-minute warning in case of reclaim
	- provisioned via spot requests
5. Dedicated Hosts
	- no multi-tenancy
	- compliance purposes