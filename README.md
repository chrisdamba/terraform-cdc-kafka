# Terraform Project: AWS RDS Integration with Confluent Kafka (Community Edition) using Debezium for CDC

This Terraform project provides a modular and reproducible way to provision the infrastructure required for robust Kafka streaming with Change Data Capture (CDC) from an AWS RDS PostgreSQL database to a self-managed Confluent Kafka cluster.

## Project Structure

* **modules/**
    * **rds/** - Terraform module to create and configure the AWS RDS PostgreSQL database.
    * **kafka/** - Terraform module to deploy and configure the Confluent Kafka cluster (self-managed).
    * **debezium/** - Terraform module to deploy and configure the Debezium CDC connector.
    * **networking/** - Terraform module to establish networking connectivity (e.g., VPC peering, security groups) between AWS and your Kafka deployment environment.
* **main.tf** - The main Terraform file that calls the individual modules and defines input variables.
* **outputs.tf** - Defines important outputs from the deployment for easy access.

## Requirements

* Terraform (installation instructions: [https://learn.hashicorp.com/tutorials/terraform/install-cli](https://learn.hashicorp.com/tutorials/terraform/install-cli))
* AWS credentials with permissions to create the required resources
* Confluent Terraform Provider ([https://registry.terraform.io/providers/confluentinc/confluent/latest/docs](https://registry.terraform.io/providers/confluentinc/confluent/latest/docs))
* A deployment environment for your Confluent Kafka cluster (e.g., AWS EC2, Kubernetes)

## Usage

1. **Clone the repository:**
  ```bash
  git clone https://github.com/chrisdamba/terraform-cdc-kafka.git
  ```
2. **Configure variables:**  Edit variables in the `variables.tf` file within each module and in the `main.tf`. 
3. **Initialize Terraform:**
   ```bash
   terraform init
   ```
4. **Plan the deployment:**
   ```bash
   terraform plan
   ```
5. **Apply the changes:**
  Example run configuration
    ```shell
    terraform apply \
      -var="db_password=somesuperdupersecret" \
      -var="db_username=dbadmin" \
      -var="my_ip=$(curl -4 ifconfig.me)" \
      -var="my_ipv6=$(curl -6 ifconfig.me)" \
    ```

## Outputs

The `outputs.tf` file will expose important values after deployment, such as:

* RDS database endpoint
* Confluent Kafka cluster bootstrap servers
* Debezium connector configuration details
* (Potentially) Links to monitoring dashboards

## Notes

- Ensure you review and modify variables, such as region-specific configurations or security settings, before applying the Terraform configurations.
- Double-check the IAM roles and permissions for AWS and Confluent Cloud resources to ensure smooth connectivity and data transfer.
- For any issues or additional configurations needed, refer to the respective Terraform file and adjust accordingly.


