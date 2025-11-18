


# 🚀 Task 3 — Infrastructure as Code (IaC) with Terraform

## 🎯 Objective

Use **Terraform** to provision a **local Docker container** using the Terraform Docker provider.

---

## 🛠 Tools & Technologies

* **Terraform**
* **Docker Desktop / Docker Engine**
* Terminal (PowerShell, Git Bash, Linux Shell)

---

## 📂 Deliverables

* `main.tf` (Terraform configuration file)
* Terraform execution logs (`init`, `plan`, `apply`, `destroy`)

---

# 📘 Explanation

This task demonstrates how Terraform can automate Docker container provisioning.
You will create infrastructure using code instead of manual docker commands.

---

# 📄 Example `main.tf`

```hcl
terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "~> 3.0.0"
    }
  }
}

provider "docker" {}

# Pull Docker Image
resource "docker_image" "nginx_image" {
  name = "nginx:latest"
}

# Create Container
resource "docker_container" "nginx_container" {
  name  = "my-nginx-container"
  image = docker_image.nginx_image.latest
  ports {
    internal = 80
    external = 8080
  }
}
```

---

# 📌 Steps to Run This Project

## ✅ 1. Install & Start Docker

Ensure Docker is running:

```
docker --version
```

## ✅ 2. Install Terraform

Verify installation:

```
terraform -v
```

## ✅ 3. Initialize Terraform

```
terraform init
```

This downloads the Docker provider plugin.

## ✅ 4. Preview Changes (Plan)

```
terraform plan
```

Shows what Terraform will create.

## ✅ 5. Apply (Create Container)

```
terraform apply
```

Type **yes** when prompted.

Docker container created → open browser:

👉 [http://localhost:8080](http://localhost:8080)

## ✅ 6. Check Terraform State

```
terraform state list
terraform state show docker_container.nginx_container
```

## ✅ 7. Destroy Infrastructure

```
terraform destroy
```

Type **yes** to remove the Docker container.

---

# 📑 Folder Structure

```
/terraform-docker-task/
│── main.tf
│── README.md
│── logs/
│     ├── init-log.txt
│     ├── plan-log.txt
│     ├── apply-log.txt
│     └── destroy-log.txt
```

---

# 📝 Notes

* Must have Docker running before executing Terraform commands.
* Terraform state file `terraform.tfstate` tracks created resources — **do not edit manually**.
* If you change container settings, run:

  ```
  terraform plan
  terraform apply
  ```

