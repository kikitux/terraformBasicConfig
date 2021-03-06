## This reposistory is created with learning purposes for Terraform.

## Purpose :

- It provides a simple example of how to create AWS instance using terraform.

## How to install terraform : 

- The information about installing terraform can be found on the HashiCorp website 
[here](https://learn.hashicorp.com/terraform/getting-started/install.html)

## How to use it :

- In a directory of your choice, clone the github repository with `git clone https://github.com/martinhristov90/terraformBasicConfig.git`
- Change into the directory using : `cd terraformBasicConfig`
- It is good practice to have a separate user that Terraform is going to perform actions with, more information how to create a user in AWS,(here)[https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users.html]
- Use your favorite text editor to modify the file `main.tf`. Set the following values : 
    - `access_key` - This would be your access key provided by AWS.
    - `secret_key` - This would be your secret key provided by AWS.
    - `region`     - This is the region where the instance is going to be deployed.
    - `subnet_id`  - Sets the subnet in which the instance is going to be attaced.
    - `vpc_security_group_ids` - Sets the ID of the security group.
- After all the values of the variables are set correctly, go ahead and execute `terraform init`. The output should look like this :
    ```shell
        --- SNIP ---

        * provider.aws: version = "~> 2.11"

        Terraform has been successfully initialized!

        --- SNIP ---
    ```
- Now, Terraform has downloded the AWS provider for you automatically.
- To preview what is going to happen without actually performing any actions, execute `terraform plan`. The output should look like this :
    ```shell
            Refreshing Terraform state in-memory prior to plan...
        The refreshed state will be used to calculate this plan, but will not be
        persisted to local or remote state storage.
        
        
        ------------------------------------------------------------------------
        
        An execution plan has been generated and is shown below.
        Resource actions are indicated with the following symbols:
          + create
        
        Terraform will perform the following actions:
        
          + aws_instance.web
              --- SNIP ---
              ami:                               "ami-0444fa3496fb4fab2"
              --- SNIP ---
              get_password_data:                 "false"
              instance_type:                     "t2.micro"
              source_dest_check:                 "true"
              --- SNIP ---
              subnet_id:                         "subnet-2f591701"
              tags.%:                            "2"
              tags.name:                         "MYMACHINE"
              tags.ping:                         "pong"
              vpc_security_group_ids.#:          "1"
              vpc_security_group_ids.2189854857: "sg-3ddbcb64"
        
        
        Plan: 1 to add, 0 to change, 0 to destroy.
        
        ------------------------------------------------------------------------
        
        Note: You didn't specify an "-out" parameter to save this plan, so Terraform
        can't guarantee that exactly these actions will be performed if
        "terraform apply" is subsequently run.
        
    ```
- If everything looks good, execute `terraform apply` to actually provision the resources defined in `main.tf`.
- Now you should have a running instance in AWS.

- In order to destroy whatever resources have been created by Terraform, execute `terraform destroy`. 


