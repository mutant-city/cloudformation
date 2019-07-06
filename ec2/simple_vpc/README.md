### Build a simple publicly accessible VPC to spin up instances.

* To use:
    1. Spin up main vpc_with_igw_and_subnet.yaml stack
        * ```aws cloudformation create-stack --stack-name public-vpc --template-body file://vpc_with_igw_and_public_subnet.yaml```
        * note: default VPC in the 10/16 block/ Subnet in 10/24 block
    2. Add an simple_ec2_instance.yaml after the VPC is created 
        *  ```aws cloudformation create-stack --stack-name nickk-ec2-2 --template-body file://simple_ec2_instance.yaml --parameters file://parameters.json ```

* Notes:  
    1. The default size of attached disks (ebs volume) inside of AWS is 8gb.  
        * This template ups that to 50gig via the ```BlockDeviceMappings``` parameter.
    2. The Instance is also automatically given a public I.P. addy due to the subnet setting: 
        * ```MapPublicIpOnLaunch: true```
    

### Finding AMI images
* https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/finding-an-ami.html
* https://cloud-images.ubuntu.com/locator/ec2/
* you can look into the ec2 console as well under the AMI section


#### Interesting References
* https://www.infoq.com/articles/aws-vpc-cloudformation/
* all of the AWS cloudformation docs for these resources

#### Gotchas
1.
```
    AvailabilityZone: !Select [ 0, !GetAZs ]
        
        or
    
    AvailabilityZone:  
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