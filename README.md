# High availability zone server deployment with Ansible and AWS

This Ansible code automates the provisioning of an AWS infrastructure using various AWS modules. It creates a security group, a classic load balancer, a launch configuration, and an auto scaling group. The infrastructure includes an EC2 instance with the Apache web server installed and an ELB for load balancing. The code retrieves information about the instances and displays their public IP addresses. It can be used as a starting point for deploying a scalable web application on AWS.

Here's a breakdown of the playbook's structure and tasks:

# Task 1: Ensure boto Existence
1. This task uses the pip module to ensure that the required boto3 and botocore Python libraries are installed.
2. It installs the libraries using pip3 and sets the state to present.

# Task 2: Creating Security Group
1. This task uses the amazon.aws.ec2_security_group module to create a security group on AWS.
2. It sets the necessary parameters such as aws_access_key, aws_secret_key, name, description, region, and the inbound and outbound rules for the security group.
3. The register parameter is used to store the output of this task in the security_group variable for later use.

# Task 3: Creating ELB (Elastic Load Balancer)
1. This task uses the amazon.aws.elb_classic_lb module to create an Elastic Load Balancer on AWS.
2. It sets the necessary parameters such as region, aws_access_key, aws_secret_key, zones, security_group_ids, name, listeners, health_check, and other load balancer configurations.
3. The register parameter is used to store the output of this task in the elb variable for later use.

# Task 5: Display DNS Address
1. This task uses the debug module to display the value of the dns_address variable.

# Task 6: Creating Launch Configuration
1. This task uses the community.aws.autoscaling_launch_config module to create an Auto Scaling launch configuration on AWS.
2. It sets the necessary parameters such as aws_access_key, aws_secret_key, name, image_id, key_name, instance_type, region, security_groups, and user_data.
3. The register parameter is used to store the output of this task in the lc_info variable for later use.

# Task 7: Creating Auto Scaling Group
1. This task uses the amazon.aws.autoscaling_group module to create an Auto Scaling group on AWS.
2. It sets the necessary parameters such as aws_access_key, aws_secret_key, region, name, load_balancers, availability_zones, desired_capacity, launch_config_name, max_size, and min_size.

# Task 8: Gather Information About All Instances
1. This task uses the amazon.aws.ec2_instance_info module to gather information about all running EC2 instances.
2. It sets the necessary parameters such as aws_access_key, aws_secret_key, region, and filters for instances in the running state.
3. The register parameter is used to store the output of this task in the ec2_info variable for later use.

# Task 9: Display Public IP Addresses of Instances
1. This task uses the debug module to display the public IP addresses of the instances.
2. It retrieves the public IP addresses from the ec2_info variable using the map filter and displays them.

# Prerequisites:
1. AWS account with free tier
2. AWS Credentials (AWS Home page -> Click on your nickname on the right upper corner -> Security Credentials -> Look for Access Key section -> Create your credentials)
3. Preinstalled software:
   - Python3 and pip3
   - Boto and Boto3
   - Ansible and Ansible-galaxy
   - amazon.aws collection (latest version)

# Usage
1. Clone the repository from the github.
2. Make sure you have Ansible installed and configured on your local machine.
3. Run the playbook using the following command: "sudo ansible-playbook main.yaml"
4. Follow the prompts to enter your AWS access key and secret key.
5. The playbook will execute the tasks to create the necessary resources on AWS and display the DNS address and public IP addresses of the instances.
