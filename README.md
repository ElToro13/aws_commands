# Create EC2 Instance from CLI

### Create a security group
```cmd
aws ec2 create-security-group --group-name EC2SecurityGroup --description "Security Group for EC2 instances to allow port 22"
```

### Add security setting. Here 0.0.0.0/0 means anyone can access this machine. 
```cmd
aws ec2 authorize-security-group-ingress --group-name EC2SecurityGroup --protocol tcp --port 22 --cidr 0.0.0.0/0
```

### Create a key-pair which will be used to login
```cmd
aws ec2 create-key-pair --key-name "NAME OF KEY" --output text> NAME_OF_KEY.pem
```

### Create the instance
Now, to create the instance, we will require AMI ID. Choose any AWS instnce and copy it's AMI -ID 
For example, AMI ID for "Ubuntu Server 20.04 LTS (HVM), SSD Volume Type" is ami-0aef57767f5404a3c

using that and the key value pair we generate, we can now create an instance

```cmd
aws ec2 run-instances   --image-id ami-06fd8a495a537da8b --security-groups EC2SecurityGroup --instance-type t2.micro --key-name NAME_OF_KEY  --block-device-mappings DeviceName=/dev/sdh,Ebs={VolumeSize=100} --count 1
```
This should be it. Now login to your instance 
