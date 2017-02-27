# Commodity cloud first

To take full advantage of cloud capabilities, you should design your application architecture taking into account cloud characteristics such as elasticity, self-service, and multi-tenancy. You will also need to understand the best practices for and constraints of distributed systems. You should also consider using provided SaaS such as AWS S3 and SES.

## Structural Principles

|   |    |
|---|---|
|Principle|Description
|Resiliency|• applications should handle failure seamlessly and automatically, either with reduced performance and / or with (gracefully) degraded functionality<br/>

## Cloud native maturity model

The table below shows cloud native maturity. You should strive at least for level 2. Note there is a large overlap between the principles below and the [twelve factor app](twelve-factor.md) principles.

|   |    |
|---|---|
|Maturity Level|Description
|Level 1: loosely coupled|• loosely coupled services, no monoliths<br/>• compute and storage are separated - application is separated from the data storage tiers, network constructs, config and logs<br/>• services are discoverable by name<br/>
|Level 2: abstracted|• elastically scalable, resilient and avoid cascading failures <br/>• services are stateless<br/>• application is unaware and unaffected by failure of dependent services<br/>• application is infrastructure agnostic and can run anywhere
|Level 3: adaptive|• application can dynamically migrate across infrastructure providers without interruption<br/>• application can elastically scale out/in based on stimuli.


## References and further reading

[Cloud native application maturity model](http://www.nirmata.com/2015/03/cloud-native-application-maturity-model/)

