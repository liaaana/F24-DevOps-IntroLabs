
# Task 2: Terraform Installation and Nginx Deployment

Terraform is HashiCorp's infrastructure as code (IaC) tool. It lets you define resources and infrastructure in human-readable, declarative configuration files, and manages your infrastructure's lifecycle.

IaC tools allow you to manage infrastructure with configuration files rather than through a graphical user interface. IaC allows you to build, change, and manage your infrastructure in a safe, consistent, and repeatable way by defining resource configurations that you can version, reuse, and share. ([Information from official website](https://developer.hashicorp.com/terraform/tutorials/docker-get-started/infrastructure-as-code))

### Steps followed to install Terraform
I followed steps from this [tutorial](https://developer.hashicorp.com/terraform/tutorials/docker-get-started/install-cli)

1) Ensured that the system is up to date and that the `gnupg`, `software-properties-common`, and `curl` packages are installed
```
sudo apt-get update && sudo apt-get install -y gnupg software-properties-common
```
2) Installed the HashiCorp GPG key
Faced problems at this step and had to enable the VPN to proceed
```
wget -O- https://apt.releases.hashicorp.com/gpg | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg > /dev/null
```
3) Verified the key's fingerprint
```
gpg --no-default-keyring \
--keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg \
--fingerprint
```
4) Added the official HashiCorp repository to system
```
`echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/hashicorp.list
```
5) Downloaded the package information from HashiCorp
```
sudo apt update
```
6) Install Terraform from the new repository
```
sudo apt-get install terraform
```

7) Checking Terraform version 
```
terraform  -version
```

Output: 
```
Terraform v1.9.6
on linux_arm64
```

8) Created a directory and file to store the Terraform configuration and copied it from the tutorial
```
mkdir learn-terraform-docker-container
cd learn-terraform-docker-container
gedit main1.tf 
```

9) Initialized the project, which downloads a plugin called a provider that lets Terraform interact with Docker
```
terraform init
```

10) Applied the configuration and created infrastructure (Added `sudo` to resolve errors)
```
sudo terraform apply
```

11) Verified the existence of the NGINX container by visiting `localhost:8000`
![Output](img3.png)


### Steps followed to build Terraform
I followed steps from this [tutorial](https://developer.hashicorp.com/terraform/tutorials/docker-get-started/docker-build)

1) Deleted previos directory `learn-terraform-docker-container` and created it again
```
mkdir learn-terraform-docker-container
```

2) Changed into the directory

```
cd learn-terraform-docker-container
```

3) Created a file to store the Terraform configuration and copied it from the tutorial
```
touch main2.tf
```

4) Initialized the directory 
```
terraform init
```

5) Formatted configuration
```
terraform fmt
```

Output:
```
main2.tf
```

6) Validated configuration
```
terraform validate
```

Output:
```
Success! The configuration is valid.
```

7) Applied the configuration and created infrastructure (Added `sudo` to resolve errors)
```
sudo terraform apply
```

8) Inspected the current state 
```
terraform show
```

Output:
```
# docker_container.nginx:
resource "docker_container" "nginx" {
    attach                                      = false
    bridge                                      = null
    command                                     = [
        "nginx",
        "-g",
        "daemon off;",
    ]
    container_read_refresh_timeout_milliseconds = 15000
    cpu_set                                     = null
    cpu_shares                                  = 0
    domainname                                  = null
    entrypoint                                  = [
        "/docker-entrypoint.sh",
    ]
    env                                         = []
    hostname                                    = "4f49cf78e7ea"
    id                                          = "4f49cf78e7eace9e9170f71ec741098ef42f12aa0d7f0366db9147dedc3accdd"
    image                                       = "sha256:195245f0c79279e8b8e012efa02c91dad4cf7d0e44c0f4382fea68cd93088e6c"
    init                                        = false
    ipc_mode                                    = "private"
    log_driver                                  = "json-file"
    logs                                        = false
    max_retry_count                             = 0
    memory                                      = 0
    memory_swap                                 = 0
    must_run                                    = true
    name                                        = "tutorial"
    network_data                                = [
        {
            gateway                   = "172.17.0.1"
            global_ipv6_address       = null
            global_ipv6_prefix_length = 0
            ip_address                = "172.17.0.2"
            ip_prefix_length          = 16
            ipv6_gateway              = null
            mac_address               = "02:42:ac:11:00:02"
            network_name              = "bridge"
        },
    ]
    network_mode                                = "bridge"
    pid_mode                                    = null
    privileged                                  = false
    publish_all_ports                           = false
    read_only                                   = false
    remove_volumes                              = true
    restart                                     = "no"
    rm                                          = false
    runtime                                     = "runc"
    security_opts                               = []
    shm_size                                    = 64
    start                                       = true
    stdin_open                                  = false
    stop_signal                                 = "SIGQUIT"
    stop_timeout                                = 0
    tty                                         = false
    user                                        = null
    userns_mode                                 = null
    wait                                        = false
    wait_timeout                                = 60
    working_dir                                 = null

    ports {
        external = 8000
        internal = 80
        ip       = "0.0.0.0"
        protocol = "tcp"
    }
}

# docker_image.nginx:
resource "docker_image" "nginx" {
    id           = "sha256:195245f0c79279e8b8e012efa02c91dad4cf7d0e44c0f4382fea68cd93088e6cnginx:latest"
    image_id     = "sha256:195245f0c79279e8b8e012efa02c91dad4cf7d0e44c0f4382fea68cd93088e6c"
    keep_locally = false
    name         = "nginx:latest"
    repo_digest  = "nginx@sha256:04ba374043ccd2fc5c593885c0eacddebabd5ca375f9323666f28dfd5a9710e3"
}
```

### Steps followed to change infrastructure
I followed steps from this [tutorial](https://developer.hashicorp.com/terraform/tutorials/docker-get-started/docker-change)

1) Skipped the steps up to `terraform apply` since I have already completed them

2) Changed the docker_container.nginx resource in main2.tf by replacing the ports.external value of 8000 with 8080

3) Applied changes
```
sudo terraform apply
```
`docker_container.nginx` was replaced

### Steps followed to destroy infrastructure
I followed steps from this [tutorial](https://developer.hashicorp.com/terraform/tutorials/docker-get-started/docker-destroy)


1) Destroyed the infrastructure using the command that terminates all resources managed by the Terraform project
```
sudo terraform destroy
```
`docker_container.nginx` and `docker_image.nginx` were destroyed



### Steps followed to define input variables

I followed steps from this [tutorial](https://developer.hashicorp.com/terraform/tutorials/docker-get-started/docker-variables)

1) Create a new file `variables.tf` with a block defining a new `container_name` variable
```
gedit variables.tf
```

variables.tf:
```
variable "container_name" {
  description = "Value of the name for the Docker container"
  type        = string
  default     = "ExampleNginxContainer"
}
```
2) In main2.tf, updated the docker_container resource block to use the new variable
```
gedit main2.tf
```
 
main2.tf:
```
resource "docker_container" "nginx" {
  image = docker_image.nginx.image_id
- name  = "tutorial"
+ name  = var.container_name
  ports {
    internal = 80
    external = 8080
  }
}

```

3) Applied changes
```
sudo terraform apply
```

4) Applied the configuration again by overriding the default container name by passing in a variable using the -var flag
```
sudo terraform apply -var "container_name=Container23238562369"
```

Output:
```
docker_image.nginx: Refreshing state... [id=sha256:195245f0c79279e8b8e012efa02c91dad4cf7d0e44c0f4382fea68cd93088e6cnginx:latest]
docker_container.nginx: Refreshing state... [id=6a367e7653754c37e5eeb137ee8f68cb66d8010c3a0fb3d14f81ba9450d7462c]

Terraform used the selected providers to generate the following execution plan.
Resource actions are indicated with the following symbols:
-/+ destroy and then create replacement

Terraform will perform the following actions:

  # docker_container.nginx must be replaced
-/+ resource "docker_container" "nginx" {
      + bridge                                      = (known after apply)
      ~ command                                     = [
          - "nginx",
          - "-g",
          - "daemon off;",
        ] -> (known after apply)
      + container_logs                              = (known after apply)
      - cpu_shares                                  = 0 -> null
      - dns                                         = [] -> null
      - dns_opts                                    = [] -> null
      - dns_search                                  = [] -> null
      ~ entrypoint                                  = [
          - "/docker-entrypoint.sh",
        ] -> (known after apply)
      ~ env                                         = [] -> (known after apply)
      + exit_code                                   = (known after apply)
      - group_add                                   = [] -> null
      ~ hostname                                    = "6a367e765375" -> (known after apply)
      ~ id                                          = "6a367e7653754c37e5eeb137ee8f68cb66d8010c3a0fb3d14f81ba9450d7462c" -> (known after apply)
      ~ init                                        = false -> (known after apply)
      ~ ipc_mode                                    = "private" -> (known after apply)
      ~ log_driver                                  = "json-file" -> (known after apply)
      - log_opts                                    = {} -> null
      - max_retry_count                             = 0 -> null
      - memory                                      = 0 -> null
      - memory_swap                                 = 0 -> null
      ~ name                                        = "ExampleNginxContainer" -> "Container23238562369" # forces replacement
      ~ network_data                                = [
          - {
              - gateway                   = "172.17.0.1"
              - global_ipv6_prefix_length = 0
              - ip_address                = "172.17.0.2"
              - ip_prefix_length          = 16
              - mac_address               = "02:42:ac:11:00:02"
              - network_name              = "bridge"
                # (2 unchanged attributes hidden)
            },
        ] -> (known after apply)
      - network_mode                                = "bridge" -> null # forces replacement
      - privileged                                  = false -> null
      - publish_all_ports                           = false -> null
      ~ runtime                                     = "runc" -> (known after apply)
      ~ security_opts                               = [] -> (known after apply)
      ~ shm_size                                    = 64 -> (known after apply)
      ~ stop_signal                                 = "SIGQUIT" -> (known after apply)
      ~ stop_timeout                                = 0 -> (known after apply)
      - storage_opts                                = {} -> null
      - sysctls                                     = {} -> null
      - tmpfs                                       = {} -> null
        # (20 unchanged attributes hidden)

      ~ healthcheck (known after apply)

      ~ labels (known after apply)

        # (1 unchanged block hidden)
    }

Plan: 1 to add, 0 to change, 1 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

docker_container.nginx: Destroying... [id=6a367e7653754c37e5eeb137ee8f68cb66d8010c3a0fb3d14f81ba9450d7462c]
docker_container.nginx: Destruction complete after 0s
docker_container.nginx: Creating...
docker_container.nginx: Creation complete after 1s [id=e11aa4c89ba5ab3b863a2e01dbb86c946b4a4f8c7000da1dbfce9d6ed2f2663d]

Apply complete! Resources: 1 added, 0 changed, 1 destroyed.

```

### Steps followed to query data with outputs
I followed steps from this [tutorial](https://developer.hashicorp.com/terraform/tutorials/docker-get-started/docker-outputs)

1) Created a file `outputs.tf` and added the configuration below to outputs.tf to define outputs for container's ID and the image ID.

```
gedit outputs.tf
```

`outputs.tf`:
```
output "container_id" {
  description = "ID of the Docker container"
  value       = docker_container.nginx.id
}

output "image_id" {
  description = "ID of the Docker image"
  value       = docker_image.nginx.id
}
```

2) Applied changes
```
sudo terraform apply
```

Output:
```
...
docker_container.nginx: Destroying... [id=e11aa4c89ba5ab3b863a2e01dbb86c946b4a4f8c7000da1dbfce9d6ed2f2663d]
docker_container.nginx: Destruction complete after 1s
docker_container.nginx: Creating...
docker_container.nginx: Creation complete after 0s [id=8d1af210e55396e8c87b9db670b21645a35ee5fa82349d86bb93d7f26ef94da7]

Apply complete! Resources: 1 added, 0 changed, 1 destroyed.

Outputs:

container_id = "8d1af210e55396e8c87b9db670b21645a35ee5fa82349d86bb93d7f26ef94da7"
image_id = "sha256:195245f0c79279e8b8e012efa02c91dad4cf7d0e44c0f4382fea68cd93088e6cnginx:latest"
```

3) Query the outputs

```
terraform output
```

Output:
```
container_id = "8d1af210e55396e8c87b9db670b21645a35ee5fa82349d86bb93d7f26ef94da7"
image_id = "sha256:195245f0c79279e8b8e012efa02c91dad4cf7d0e44c0f4382fea68cd93088e6cnginx:latest"
```

4) Destroyed infrastructure
```
sudo terraform destroy
```

Output:
```
...
docker_container.nginx: Destroying... [id=8d1af210e55396e8c87b9db670b21645a35ee5fa82349d86bb93d7f26ef94da7]
docker_container.nginx: Destruction complete after 1s
docker_image.nginx: Destroying... [id=sha256:195245f0c79279e8b8e012efa02c91dad4cf7d0e44c0f4382fea68cd93088e6cnginx:latest]
docker_image.nginx: Destruction complete after 0s

Destroy complete! Resources: 2 destroyed.
```