## Documentation for Lab Assignments with Apache Metron

Note: Putty users on Windows use .ppk private key to login. Mac users should use .pem key instead.

Command to create and start AWS EC2 instance from an AMI image:
```
aws ec2 run-instances --image-id ami-20271545 --count 1 --instance-type r4.xlarge --key-name metron-cluster --subnet-id subnet-c2e6fbab --security-group-ids sg-c28e5ba9 --user-data file://aws_metron_script.sh  --tag-specifications --tag-specifications ResourceType=instance,Tags=[{Key=Name,Value=Ec2InstanceTag}] ResourceType=volume,Tags=[{Key=Name,Value=VolumeTag}]
```
Where ami-5af0c33f is an AMI image ID, 
File aws_metron_script.sh is stored in the same folder on local machine as the AWS CLI downloaded files. It contains commands to be executed at boot of an AWS EC2 instance

Schedule a script to terminate instances from Windows 10 command line interface
```
Schtasks /CREATE /tn taskName /sc ONCE /TR "C:\path_to_AWS_CLI\stop_instances.bat" /ST 23:59
```

Command to stop an EC2 instance using AWS CLI:
```
aws ec2 stop-instances --instance-ids i-0c1f28b6e1c849f65
```

### Potential errors 
1. New instances are not created and "The quota for number of instances of this type has been reached." message is displayed. 
 - Solution 1. Submit a request to raise the quota for particular instances. In the top right corner, click Support, then Support Center. Create a case regarding service limit increase.
 - Solution 2. Terminate unneeded instances of this type. 
2. The number of instances is less than allowed quota but new instances are not created with the same message as in (1).
 - Solution. When certain instances are deleted, corresponding storage volumes are not deleted automatically. In the EC2 Volumes menu delete those volumes in the Available state.
 
 

