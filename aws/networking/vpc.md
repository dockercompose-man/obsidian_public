The following terminology can be useful when you work with a VPC and Amazon QuickSight.

A _VPC_ is a virtual private cloud, which works like a private network to isolate the resources within it. The solution described in these topics uses an AWS service called Amazon VPC.

A _route table_ contains a set of rules, called _routes,_ that are used to determine where network traffic is directed. You can view the route table in the Amazon VPC console at [https://console.aws.amazon.com/vpc/](https://console.aws.amazon.com/vpc/)

. The VPC details display the route table that the VPC is using. You can also see **Route tables** listed in the Amazon VPC console.

A _subnet_ is a defined set of network IP addresses that are used to increase the security and efficiency of network communications. You can think of them like postal codes, used for routing packages from one location to another. The **Subnets** list in the Amazon VPC console displays subnet IDs and also their associated VPC IDs, route tables, and network ACLs. You need to provide at least two subnets in different availability zones to create a VPC connection.

A _network interface_ represents a virtual network card. The network interface automatically created by QuickSight is called a _QuickSight network interface._ Each network interface in a VPC connection is configured based on the subnet it's attached to. You can view your QuickSight network interfaces in the Amazon EC2 console at [https://console.aws.amazon.com/ec2/](https://console.aws.amazon.com/ec2/)

. The network interface displays its network interface ID, subnet ID, VPC ID, security group, and the Availability Zone that it exists in. You can click on the security group name to see its group ID and its inbound and outbound rules. The term _network interface_ in the following sections always means elastic network interface.

A _security group_ is a set of rules that controls the network access to the resources it is associated with. Access is permitted only to and from the components defined in the security group's inbound and outbound rules. If no rules are defined, the security group prevents all access. You can view security groups from several different consoles, depending on which resource that a particular security group applies to. You can see all the security groups and their settings in one place in the VPC console. For the QuickSight VPC connection, create a new security group.

_Inbound and outbound rules_ define the following:

- The type of traffic to allow, for example `"All TCP"` or `"RDS"`.
    
- The protocol to allow (TCP, UDP, or ICMP).
    
- The traffic source to allow for inbound rules, or the traffic destination to allow for outbound rules. When you work with a VPC and QuickSight, you specify the security group ID to use.
    
- An optional description. We recommend that you add the word `QuickSight` to the description for QuickSight VPC rules.
    

An _internet gateway_ is a VPC component that allows communication between instances in your VPC and the internet. You don't need an internet gateway to use QuickSight VPC connections.

A _VPC endpoint_ enables you to privately connect your VPC to supported AWS services without using public IP addresses. You don't need to set up a VPC endpoint to use QuickSight VPC connections.

### Examples

10.0.0.0/24
10.0.0.0/16
10.0.0.0/8

/24 last number - 10.0.0.1 - 10.0.0.254
/16 last two numbers - 10.0.0.1 - 10.0.255.254
/8 last three numbers - 10.0.0.1 - 10.255.255.254