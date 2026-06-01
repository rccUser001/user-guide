# Accessing RCC clusters
 This tutorial shows the basic steps to use the Midway3 cluster at the RCC. For complete RCC technical documentation, see the main sections of this user guide. The information here describes how users can connect to Midway to access RCC resources. All users are responsible for knowing and abiding by the [RCC Terms of Use](https://rcc.uchicago.edu/about-rcc/rcc-user-policy).

## RCC account credentials
To connect to RCC resources, you must have an RCC user account sponsored by PI ([request an account](https://rcc.uchicago.edu/accounts-allocations/request-account){:target='_blank'}). The RCC account uses your UChicago CNetID and its corresponding password. 

## Supported protocols
The following table provides a summary of supported connection methods:

|  <div style="width:150px">Connection Method | Description | GUI Support | Access to Compute Nodes | Data Transfer | Data Sharing |  
| ------------------------------------------- | ----------- | ------- | ------- |------------- | ------------ | 
| [SSH](ssh/main.md)  | Command line interface | Limited | Yes | Yes (two-way) | RCC Internal |
| [Open OnDemand](open_ondemand/open_ondemand.md) | A user-friendly web-based portal  | Full-scale  | Yes | Yes (two-way) | RCC Internal + Globus |
| [ThinLinc](thinlinc/main.md) | A web-based or client-based desktop  | Full-scale | Yes | Yes (two-way) | RCC Internal |
|[SAMBA](../data_transfer/persistent_mapping/samba.md)| An persistend network drive to sync local data with remote | File Manager | No | Yes (two-way) | No |
|[Globus](globus/access-files.md)| A web-based platform for asynchronous data transfer, sharing, and management | File Manager | No | Yes (two-way) | External and RCC collaborators |




