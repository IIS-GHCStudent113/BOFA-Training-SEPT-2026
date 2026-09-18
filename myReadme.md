
https://github.com/jruels/modern-automation/tree/main


https://github.com/jruels/modern-automation/blob/main/labs/playbook-fun/index.md


Modern Automation with Terraform and Ansible
This site includes the labs for the Modern Automation with Terraform and Ansible class.

Labs
Lab information

Day 1
Lab 1: Python guessing game
Lab 1a: Intro Python guessing game
Lab 2: Using Python to interact with APIs
Lab 3: AWS Setup

Day 2
Lab 1: Terraform First Instance
Lab 2: Terraform Variables and Outputs
Lab 3: Terraform Multi-Resource Deployment
Lab 4: Strings, bool, and numbers

Day 3
Lab 5: HCP Terraform Setup
Lab 6: HCP Terraform Modify Infrastructure
Lab 7: Write your own module
Lab 8: HCP Terraform Publish Module

Day 4
Lab 9: Connect to Ansible Controller
Lab 10: Ansible inventory
Lab 11: Ansible ad-hoc
Lab 12: Ansible playbook fundamentals
Lab 12a: Ansible playbooks - beyond the basics

Day 5
Lab 13: Ansible roles
Lab 13a: Ansible roles - extended
Lab 14: AAP inventory and credentials
Lab 15: AAP projects and jobs
Lab 16: Ansible Playbook Error Handling
Lab 17: Ansible Templating
Lab 18: Write an Ansible module





------------


login info


https://github.com/jruels/modern-automation/tree/main
https://docs.google.com/spreadsheets/d/1puE5aAzxZR4JvnBy07pxbJLZ-_fiPv6CbkgCSIbzt1g/edit?usp=sharing


---------------------Github name----------------------------------------------------------------------------------------
IIS-GHCStudent113

---------------------Ablaze----------------------------------------------------------------------------------------------
First Name	Last Name	Ablaze VM	    Ablaze Password	    GH Username	            GH Password
TBD	        TBD	         

---------------------AWS-----------------------------------------------------------------------------------------------
First Name	Last Name	AWS Account Name	Username	Password	    LoginUrl	
TBD	        TBD	        https://
------------------------------------------------------------------------------

First Name	Last Name	ControllerIP	TargetIP1	    TargetIP2
TBD	        TBD	        1.1.1.1	1.1.1.1	1.1.1.1


---------------------HCP--------------------------------------------------------------------------------------------
First Name	Last Name	HCP Username	HCP Password
TBD	TBD	hcpstu



-----------------------------------------------------------------------------------------------------------------
Terraform STEPS:
1.<VM> = https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/instance
2.<S3> = https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket
3.<IAM> = https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role
4.<Policy Att> = 


Terraform Note: 
0.Terraform = Core Terraform + Modules + Providers
1.<data> keyword in Terraform meannig, resource ALREADY exsist in provider / AWS account. Pulling data from provider.
2.if data = something already means, we pulling, not creating. 
3.AMI =Amazon Machine Image
4.<resource> keyword in terraform - meaning we CREATING INSTANCE/ somethign in cloud /onprim /provider account.
    <resource>: subnet_id, depends_on, ami, instace_type, vpc_security_group_ids, key_name, count, root_block
    Look up at https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/instance
5.Terraform work on HCL Hashicorp config Lang 
6.provisioner = avoid this, not good idea, very imperretive, not declarative. Declarative = declare fix, imperative = force withour declarative, not controllable
7. terraform -chdir=environments/dev (apply|plan|destroy) 






-----------------------------------------------------------------------------------------------------------------
Day2 = Terraform (IAC) from https://github.com/jruels/modern-automation/blob/main/labs/tf-first-instance/index.md
-----------------------------------------------------------------------------------------------------------------
    PS C:\Users\tekstudent> aws configure 
    AWS Access Key ID [None]: ###
    AWS Secret Access Key [None]: ###
    Default region name [None]: us-west-1
    Default output format [None]: 
    PS C:\Users\tekstudent> aws sts get-caller-identity
    {                                                                                                                                              
        "UserId": "AIDASPWQIHENNQ3IGWYKH",
        "Account": "171161696538",
        "Arn": "arn:aws:iam::171161696538:user/students/Student17"
        }


    -----------------------------------------------------------------------------------------------------------------
    >>>>>>>>>>>> Lab-1 Start here = https://github.com/jruels/modern-automation/blob/main/labs/tf-first-instance/index.md
    -----------------------------------------------------------------------------------------------------------------
    PS C:\Users\tekstudent\Desktop\terraform\tf-lab1> 
        making main.tf file here ---> 
                        terraform {
                    required_providers {
                        aws = {
                        source  = "hashicorp/aws"
                        }
                    }
                    }

                    provider "aws" {
                    region  = "us-west-1"
                    }

                    resource "aws_instance" "lab1-tf-example" {
                    ami           = "ami-06e4ca05d431835e9"
                    instance_type = "t2.micro"

                    tags = {
                        Name = "Lab1-TF-example"
                    }
                    }



     PS C:\Users\tekstudent\Desktop\terraform\tf-lab1> terraform init
        Terraform has been successfully initialized!

        You may now begin working with Terraform. Try running "terraform plan"


    Format and Validate Configuration
    PS C:\Users\tekstudent\Desktop\terraform\tf-lab1> terraform fmt
        main.tf

    This command formats the file to meet HCL standards
    PS C:\Users\tekstudent\Desktop\terraform\tf-lab1> terraform validate
        Success! The configuration is valid.
        
    
    Create infra
    PS C:\Users\tekstudent\Desktop\terraform\tf-lab1> terraform apply
        Terraform will perform the following actions:
        # aws_instance.lab1-tf-example will be created
        aws_instance.lab1-tf-example: Creating...

    UI verify created on UI bylogin this ---> 
        http://us-west-1.console.aws.amazon.com/ec2/home?region=us-west-1#Instances:instanceState=running if the 1 instance is running or not

    CLI view - command to verify using this command --- AWS cli command to read instance (copilot)
        PS C:\Users\tekstudent\Desktop\terraform\tf-lab1> aws ec2 describe-instances --region us-west-1 --output table
        ---------------------------------------------------------------------------------------                      
        |                                  DescribeInstances                                  |
        +-------------------------------------------------------------------------------------+
        ||                                   Reservations                                    ||
        |+----------------------------------+------------------------------------------------+|
        ||  OwnerId                         |  171161696538                                  ||
        ||  ReservationId                   |  r-04e162cf4bcb93aef                           ||
        |+----------------------------------+------------------------------------------------+|
        |||                                    Instances                                    |||
        ||+---------------------------+-----------------------------------------------------+||
        |||  AmiLaunchIndex           |  0                                                  |||
        |||  Architecture             |  x86_64                   -- More  -- 

    Cleanup 
        terraform destroy

    Done
        https://github.com/jruels/modern-automation/blob/main/labs/tf-first-instance/index.md 

    -----------------------------------------------------------------------------------------------------------------
    >>>>>>>>>>>> Lab-2 Start here =  https://github.com/jruels/modern-automation/blob/main/labs/tf-variables-and-output/index.md
    -----------------------------------------------------------------------------------------------------------------

    main.tf 
            terraform {
                required_providers {
                    aws = {
                    source = "hashicorp/aws"
                    }
                }
                }

                provider "aws" {
                region = "us-west-1"
                }

                resource "aws_instance" "lab1-tf-example" {
                ami           = "ami-06e4ca05d431835e9"
                instance_type = "t2.micro"

                tags = {
                    Name = var.instance_name
                }
            }



    variable.tf
        variable "instance_name" {
        description    = "Name tag for EC2 instance - Sumit here for testing"
        type           = string
        default        = "Lab2-TF-example"
        }

    PS C:\Users\tekstudent\Desktop\terraform\tf-lab2> terraform init
            Initializing the backend...


    PS C:\Users\tekstudent\Desktop\terraform\tf-lab2> terraform apply
        will start

    But to update thing in already running use this---->   Apply the configuration again, passing the variable via the command line:
    
    This will modify / apply the configuration again, passing the variable via the command line:
    PS C:\Users\tekstudent\Desktop\terraform\tf-lab2> terraform apply -var 'instance_name=SumitMistry'


    CREATE a new file = outputs.tf
            output "instance_id" {
            description    = "ID of the EC2 instance"
            value          = aws_instance.lab2-tf-example.id
            }

            output "instance_private_ip" {
            description   = "Private IP address of EC2 instance"
            value       = aws_instance.lab2-tf-example.private_ip
            }

            output "instance_arn" {
            description   = "ARN of EC2 instance"
            value       = aws_instance.lab2-tf-example.arn
            }



    
    PS C:\Users\tekstudent\Desktop\terraform\tf-lab2> terraform apply  --> The above changes will add these 2 lines in terminal while entering this cmd

        Outputs:
        instance_arn = "arn:aws:ec2:us-west-1:171161696538:instance/i-0d0cde7b37e7fc146"
        instance_id = "i-0d0cde7b37e7fc146"
        instance_private_ip = "1.1.1.1"
            
    

    Note that all available output are located at -   https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/instance#attribute-reference
    
    
    PS C:\Users\tekstudent\Desktop\terraform\tf-lab2> terraform output
            instance_arn = "arn:aws:ec2:us-west-1:171161696538:instance/i-0d0cde7b37e7fc146"
            instance_id = "i-0d0cde7b37e7fc146"
            instance_private_ip = "1.1.1.1"


            


PS C:\Users\tekstudent\Desktop\terraform\tf-lab2> terraform destroy -auto-approve
Check cleanup or not --> https://us-west-1.console.aws.amazon.com/ec2/home?region=us-west-1#Instances:instanceState=running


Lab Done. Ends ===> https://github.com/jruels/modern-automation/blob/main/labs/tf-variables-and-output/index.md
       
-----------------------------------------------------------------------------------------------------------------
 Lab-3 = https://github.com/jruels/modern-automation/blob/main/labs/tf-more-variables/index.md
 
PS C:\Users\tekstudent\Desktop\terraform\tf-lab2> cd..
PS C:\Users\tekstudent\Desktop\terraform> cd tf-lab3
PS C:\Users\tekstudent\Desktop\terraform\tf-lab3> git clone https://github.com/jruels/learn-terraform-variables.git
        Cloning into 'learn-terraform-variables'...
        remote: Enumerating objects: 54, done.
        remote: Counting objects: 100% (23/23), done.
        remote: Compressing objects: 100% (13/13), done.
        remote: Total 54 (delta 13), reused 10 (delta 10), pack-reused 31 (from 1)
        Receiving objects: 100% (54/54), done.


              
PS C:\Users\tekstudent\Desktop\terraform\tf-lab3\learn-terraform-variables> terraform init
    Initializing the backend... 


PS C:\Users\tekstudent\Desktop\terraform\tf-lab3\learn-terraform-variables> terraform apply
    module.ec2_instances.data.aws_ami.amazon_linux: Reading...
    data.aws_availability_zones.available: Reading...

    Outputs:
    public_dns_name = "lb-lmS-project-alpha-dev-1780598940.us-west-1.elb.amazonaws.com"



Now there is empty variable.tf file in there add below data:
    # Variable declarations


    variable "aws_region" {
    description = "AWS region"
    type        = string
    default     = "us-west-1"
    }


    variable "vpc_cidr_block" {
    description = "VPC CIDR block"
    type        = string
    default     = "1.1.1.1/16"
    }



    variable "instance_count" {
    description = "Number of instances to provision"
    type        = number
    default     = 2
    }

Now adjust main.tf to accept hard coded value to take from var. valuess and run thats it.

-----------------------------------------------------------------------------------------------------------------
 Lab-4 = https://github.com/jruels/modern-automation/blob/main/labs/tf-even-more-variables/index.md
 -----------------------------------------------------------------------------------------------------------------

    Use lab-3 exisitng code.
    this lab is to add more data type of variable in the exisitng code and test and make confident coders



    go to variable.tr 
    add     below :
    

        variable "enable_vpn_gateway" {
            description = "Enable a VPN gateway in your VPC"
            type        = bool
            default     = false
        }


        variable "resource_tags" {
            description = "Tags to set for all resources"
            type        = map(string)
            default     = {
                project     = "project-alpha",
                environment = "dev"
            }
        }


    PS C:\Users\tekstudent\Desktop\terraform\tf-lab3\learn-terraform-variables> terraform console
        >> 
        > var.resource_tags["environment"]
        "dev"
        > exit
    PS C:\Users\tekstudent\Desktop\terraform\tf-lab3\learn-terraform-variables> 


    go to main.tf

        change-1
            
            remove----->
            -  tags = {
            -    project     = "project-alpha",
            -    environment = "dev"
            -  }


            replace ---->
            +  tags = var.resource_tags
        
    

        change-2
            -  instance_type  = "t2.micro"
            +  instance_type  = var.ec2_instance_type


    add new file terraform.tfvars

        resource_tags = {
            project     = "new-project",
            environment = "test",
            owner       = "me@example.com"
        }

        ec2_instance_type = "t2.nano"

        instance_count = 3



    go to  variables.tf and add these validation parameters in the resourse_tags module:

        variable "resource_tags" {
        description = "Tags to set for all resources"
        type        = map(string)
        default     = {
            project     = "my-project",
            environment = "dev"
            }

        validation {
            condition     = length(var.resource_tags["project"]) <= 16 && length(regexall("/[^a-zA-Z0-9-]/", var.resource_tags["project"])) == 0
            error_message = "The project tag must be no more than 16 characters, and only contain letters, numbers, and hyphens."
        }

        validation {
            condition     = length(var.resource_tags["environment"]) <= 8 && length(regexall("/[^a-zA-Z0-9-]/", var.resource_tags["environment"])) == 0
            error_message = "The environment tag must be no more than 8 characters, and only contain letters, numbers, and hyphens."
        }
        }








-----------------------------------------------------------------------------------------------------------------
Day-3
-----------------------------------------------------------------------------------------------------------------
Lab 5: HCP Terraform Setup = https://github.com/jruels/modern-automation/blob/main/labs/hcp-tf-setup/index.md



    1. Fork and Clone the Example Terraform Configuration
    Go to git clone https://github.com/jruels/learn-terraform-variables


    Forked = https://github.com/IIS-GHCStudent113/learn-terraform-variables

    go to that dir

    2. terraform login

    3. generate token = X

    4.
    workspace is here --> https://app.terraform.io/app/policy-as-code-training/workspaces


    5. verify by doing
        PS C:\Users\tekstudent\Desktop\terraform\tf-lab5> terraform login

        Welcome to HCP Terraform!   


    6.main.tf 
        Update + SAVE Your Configuration with a Cloud Block and add this

        

        terraform {
            cloud {
                organization = "policy-as-code-training"
                workspaces {
                name = "tf-vault-qa-sumit-{todays-date}"
                }
            }
        }

    7. go to main.tf file folder
        cd C:\Users\tekstudent\Desktop\terraform\tf-lab5\learn...


    8. terraform init 
        --> will start all resources, once done next

    9. Go to site:
        https://app.terraform.io/app/policy-as-code-training/workspaces/tf-vault-qa-sumit-09162026/
        >open my workspace
        >navigate to variable page

    10. Set AWS Credentials as Workspace Environment Variables  
        instrcutor provided >>> make >>> 
        
        Environment variable
            AWS_ACCESS_KEY_ID = ###
            AWS_SECRET_ACCESS_KEY = ###

    11.








-----------------------------------------------------------------------------------------------------------------

Lab 6: HCP Terraform Modify Infrastructure  | https://github.com/jruels/modern-automation/blob/main/labs/hcp-tf-modify/index.md

    1.Open your main.tf file and comment out the cloud block,
                terraform {
                /*
                cloud {
                    organization = "policy-as-code-training"
                    workspaces {
                    name = "tf-vault-qa-{your-initials}"
                    }
                }
                */
                }
    2.
    git add .
    git commit -m "Remove cloud block"
    git push

    3. Connect VCS integration in HCP terraform
        UI -> Settings  -> Version Control -> Connect to version control -> Version Control Workflow -> Github.com
        
        POPUP - Authorize HCP Terraform to access your repository
        Keep all default.

    4. Lab goal is to check if the code change will trigger the whole run automatically?

-----------------------------------------------------------------------------------------------------------------
Lab 7: Write your own module ///  a module to manage AWS S3 buckets

    1. git clone https://github.com/jruels/learn-terraform-modules-create.git

    
    2.


    3.


    4.



-----------------------------------------------------------------------------------------------------------------
Day 4
-----------------------------------------------------------------------------------------------------------------
Lab 9: Connect to Ansible Controller
https://github.com/jruels/modern-automation/blob/main/labs/setup/index.md#add-the-ssh-configuration-for-the-lab-servers

    1. login git bash
    2. git clone https://github.com/jruels/modern-automation.git
    3. Set up a remote SSH session in Visual Studio Code.
        clikc on VS code and SSH icon "Remote explorer"
         gear icon --> seelct --> C:\Users\tekstudent\.ssh\config
         

    4. in config file --> Add the SSH configuration for the lab servers.

                Host tower
            HostName 1.1.1.1
            IdentityFile ~/Downloads/repos/modern-automation/keys/lab.pem
            User ansible
    5. save it and now ready to open the terminal.

    6. Connect to the lab servers.
            In the Remote Explorer, you should now see the entry for the Tower server under "SSH Targets."
            Click on the entry to connect to the Tower server.
            Visual Studio Code will open a new window connected to the Tower server.
            When prompted for the Operating System, choose 'Linux'.
            Accept the SSH fingerprint
            You can now open a terminal in this new window and run commands on the Tower server.


    7.Check all ansible helath check-----

        [ansible@ip-10-100-16-67 ~]$ ansible all -i inventory -m ping
                ControlNode | SUCCESS => {
                    "ansible_facts": {
                        "discovered_interpreter_python": "/usr/bin/python3"
                    },
                    "changed": false,
                    "ping": "pong"
                }
                TargetNode-2 | SUCCESS => {
                    "ansible_facts": {
                        "discovered_interpreter_python": "/usr/bin/python3"
                    },
                    "changed": false,
                    "ping": "pong"
                }
                TargetNode-1 | SUCCESS => {
                    "ansible_facts": {
                        "discovered_interpreter_python": "/usr/bin/python3"
                    },
                    "changed": false,
                    "ping": "pong"
                }
                [ansible@ip-10-100-16-67 ~]$ `
    


    8. Help -->
            [ansible@ip-10-100-16-67 ~]$ ansible --help

            [ansible@ip-10-100-16-67 ~]$ ansible-doc -l | grep ansible.builtin

            ----> I picked randonly from above, "Shell"

            Current server info = hostnamectl --> run on other web-servers ---> how --> see below:

            instead of ssh each worker node and see health, use this cmd to check health using ANSIBLE = 

            [ansible@ip-10-100-16-67 ~]$ ansible webservers -i inventory/ -m shell -a "hostnamectl"
                    TargetNode-2 | CHANGED | rc=0 >>
                    Static hostname: ip-10-100-16-196.us-west-1.compute.internal
                        Icon name: computer-vm
                            Chassis: vm 🖴
                        Machine ID: ec2dd84a7b192fa82a5059b7f9519263
                            Boot ID: 75c8cfae567849d88d4ec93a18a19a52
                    Virtualization: amazon
                    Operating System: CentOS Stream 9
                        CPE OS Name: cpe:/o:centos:centos:9
                            Kernel: Linux 5.14.0-742.el9.x86_64
                        Architecture: x86-64
                    Hardware Vendor: Amazon EC2
                    Hardware Model: t3.micro
                    Firmware Version: 1.0
                    TargetNode-1 | CHANGED | rc=0 >>
                    Static hostname: ip-10-100-16-62.us-west-1.compute.internal
                        Icon name: computer-vm
                            Chassis: vm 🖴
                        Machine ID: ec2516b43a0b313ecfb9080adfbd0016
                            Boot ID: 3a73edeeeb57491187bce3269ddf522b
                    Virtualization: amazon
                    Operating System: CentOS Stream 9
                        CPE OS Name: cpe:/o:centos:centos:9
                            Kernel: Linux 5.14.0-742.el9.x86_64
                        Architecture: x86-64
                    Hardware Vendor: Amazon EC2
                    Hardware Model: t3.micro
                    Firmware Version: 1.0
                    [ansible@ip-10-100-16-67 ~]$ 


-----------------------------------------------------------------------------------------------------------------
Lab 10: Ansible inventory: https://github.com/jruels/modern-automation/blob/main/labs/inventory/index.md
-----------------------------------------------------------------------------------------------------------------

    1.Create an folder /file:
        lab-inventory/inventory.yaml

            Paste in the following:

            [media] 
            media1 ansible_host=<IP of TargetNode-1 from /home/ansible/inventory/inventory.yaml>
            media2 ansible_host=<IP of TargetNode-2 from /home/ansible/inventory/inventory.yaml>



    2. Create a group_vars directory:

            In the group_vars directory, create a media file with the following:

            media_content: /tmp/var/media/content/
            media_index: /tmp/opt/media/mediaIndex


    3. Configure the webservers
    append into inventory
            [webservers] 
            web1 ansible_host=<IP of TargetNode-1 from /home/ansible/inventory/inventory.yaml>
            web2 ansible_host=<IP of TargetNode-2 from /home/ansible/inventory/inventory.yaml>

    4. Define Variables for webservers:
        in folder -group_vars directory, create a "webservers" file with below:"

            httpd_webroot: /var/www/
            httpd_config: /etc/httpd/



    5.  script_files variable for web1

            In the lab directory (lab-inventory), create a host_vars directory

            Inside the host_vars directory, create a web1 file

            Paste in the following:

            script_files: /tmp/usr/local/scripts 

            Copy the scripts directory from the clone repository to the lab directory.

            cp -r /home/ansible/automation-dev/labs/inventory/scripts /home/ansible/lab-inventory/.



6. Testing
        Ensure you're in the lab-inventory directory and run the following.

        bash ./scripts/backup.sh 

        If you have correctly configured the inventory, you won't see any errors.

                    
        ansible webservers -m copy -a "src=files/index.html dest={{httpd_webroot}}index.html"
        ansible webservers -m shell -a "ls"

        ansible webservers -m shell -a "cat {{httpd_webroot}}index.html"







-----------------------------------------------------------------------------------------------------------------
Lab 11: Ansible ad-hoc:  https://github.com/jruels/modern-automation/blob/main/labs/ad-hoc/index.md
-----------------------------------------------------------------------------------------------------------------


    1. within above same strcutrue, add one more folder.... create fdolder "lab-ad-hoc"
        create file inside inventory 
        
        cd lab-ad-hoc/


    2. inventory file add
            [dbsystems]
            db1 ansible_host=1.1.1.1
            db2 ansible_host=1.1.1.1

    3. Copy the user accounts file

            cp /home/ansible/automation-dev/labs/ad-hoc/files/userlist.txt /home/ansible/lab-ad-hoc/userlist.txt

    4.  read the userlist.tx that has 2 users. so now....Create the User Accounts

        ansible -i inventory dbsystems -b -m user -a "name=consultant" 
        TO TEST = ansible -i inventory dbsystems -m shell -a "ls /home"


        ansible -i inventory dbsystems -b -m user -a "name=supervisor" 
        TO TEST = ansible -i inventory dbsystems -m shell -a "ls /home"

    5.Create keys for users, Create keys for the consultant and supervisor users.

        Create keys for the consultant and supervisor user
            mkdir -p keys/{consultant,supervisor}/.ssh


        Generate SSH key for consultant and supervisor users. RUN EACH LINE SEPARATELY
            ssh-keygen -f keys/consultant/.ssh/id_rsa
            ssh-keygen -f keys/supervisor/.ssh/id_rsa


        Create the authorized_keys files
            cat keys/consultant/.ssh/id_rsa.pub > keys/consultant/authorized_keys
            cat keys/supervisor/.ssh/id_rsa.pub > keys/supervisor/authorized_keys



    6.Place Key Files in the Correct Location, /home/$USER/.ssh/authorized_keys, on Hosts in dbsystems

        ONE by ONE ---> 
            ansible -i inventory dbsystems -b -m file -a "path=/home/consultant/.ssh state=directory owner=consultant group=consultant mode=0755" 


            ansible -i inventory dbsystems -b -m copy -a "src=/home/ansible/lab-ad-hoc/keys/consultant/authorized_keys dest=/home/consultant/.ssh/authorized_keys mode=0600 owner=consultant group=consultant" 


            ansible -i inventory dbsystems -b -m file -a "path=/home/supervisor/.ssh state=directory owner=supervisor group=supervisor mode=0755"


            ansible -i inventory dbsystems -b -m copy -a "src=/home/ansible/lab-ad-hoc/keys/supervisor/authorized_keys dest=/home/supervisor/.ssh/authorized_keys mode=0600 owner=supervisor group=supervisor" 




    7. Ensure auditd Is Enabled and Running on All Hosts

            ansible -i inventory dbsystems -b -m service -a "name=auditd state=started enabled=yes" 
            
            ansible -i inventory dbsystems -b -m user -a "name=consultant" 
            ansible -i inventory dbsystems -m shell -a "ls /home"
            

    8. Another Test / Valdiation check if ssh directly working or not?
            ssh consultant@1.1.1.1 -i keys/consultant/.ssh/id_rsa
            ssh supervisor@1.1.1.1 -i keys/consultant/.ssh/id_rsa
            ssh supervisor@1.1.1.1 -i keys/supervisor/.ssh/id_rsa

    
    8. Done-------------

-----------------------------------------------------------------------------------------------------------------
Lab 12: Ansible playbook fundamentals https://github.com/jruels/modern-automation/blob/main/labs/playbook-fun/index.md
-----------------------------------------------------------------------------------------------------------------

    1.create and go 
        cd lab-playbook-fun/

    2. create file - inventory 
            [web]
            node1 ansible_host=<IP of TargetNode-1 from /home/ansible/inventory/inventory.yaml>
            node2 ansible_host=<IP of TargetNode-2 from /home/ansible/inventory/inventory.yaml>

    3. Create a Playbook
            Create/home/ansible/lab-playbook-fun/web.yml file with these contents:

                ---
                - hosts: web
                become: yes
                tasks:
                    - name: install httpd
                    yum: 
                        name: httpd 
                        state: latest
                    - name: start and enable httpd
                    service: 
                        name: httpd 
                        state: started 
                        enabled: yes
                    - name: retrieve website from repo
                    get_url: 
                        url: https://github.com/jruels/ansible-best-practices/raw/main/labs/playbook-fun/files/website.zip 
                        dest: /tmp/website.zip
                    - name: install website
                    unarchive: 
                        remote_src: yes 
                        src: /tmp/website.zip 
                        dest: /var/www/html/

        4. Execute the playbook
                ansible-playbook -i inventory web.yml  ---> will fail so next

        
        
        5. change above web.yml file
                
           tasks:
            - name: install httpd
            yum: 
                name: 
                - httpd
                - unzip
                state: latest


        6.ansible web -i inventory -m shell -a "curl ifconfig.me"
  

        7.    TEST this playbook = go to website, but port is not open so no
            TEST ==  ansible web -i inventory -m shell -a "curl localhost"

                
                go to AWS--> Security group  , open port 8080, so we can opens ite directly.


                Use ansible cmd to get public ip and go to broswer and see
                ansible web -i inventory -m shell -a "curl ifconfig.me" ----> get public ip and surf!
                    1.1.1.1
                    1.1.1.1
        

        8. done

















