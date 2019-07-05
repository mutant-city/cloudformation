```
        Fn::Select: 
          - 0
          - Fn::GetAZs: "" 
```

* Selecting availability zones
     * This dynamically selects an availability zone
     * Note: This Fn:GetAZs function is not super clear
     i.e. the first availability zone in the region
     the command break down is as follows:
     * Fn::Select(\<array item>,  \<array>]) 
        * selects an item from an array
    * Fn::GetAzs(\<region>) 
        * returns an array of az from a region, 
        * if <region> is blank return current region
        * order not guaranteed 
        * see reference for what it returns, this is not straightforward if there are mixed subnet/non-subnet AZ's
    * Note: Explore further what this returns if some AZ's have subnets and some don't
        * according to the docs it will only return the ones with subnets
    * View AZ's via cli: ```aws ec2 describe-availability-zones```
    * Interesting References:
        * https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-getavailabilityzones.html
        * https://konekti.us/blog/2018/01/24/aws-intrinsic-functions.html
        * https://stackoverflow.com/questions/21390444/is-there-a-way-for-cloudformation-to-query-available-zones-for-subnet-creation
        * https://acloud.guru/forums/aws-certified-devops-engineer-professional/discussion/-KK6yFxSY2oqXGaiLzCh/getazs
        * https://medium.com/linux-academy/using-cloudformation-intrinsic-functions-1865413f3bc2
        * https://www.kencochrane.net/2016/12/16/understanding-aws-regions-and-availability-zones-in-cloudformation/