# Question 7.
Which of the following sequences describes the Terraform workflow for:
- Downloading plugins and setting up backend
- Generating and executing changes
- Removing all resources? (1 point)

1. terraform import, terraform apply -y, terraform destroy
2. teraform init, terraform plan -auto-apply, terraform rm
3. terraform init, terraform run -auto-approve, terraform destroy
4. terraform init, terraform apply -auto-approve, terraform destroy
5. terraform import, terraform apply -y, terraform rm


## Answer
Check the Terraform module in this GitHub repo:
https://github.com/DataTalksClub/data-engineering-zoomcamp/blob/main/01-docker-terraform/terraform/1_terraform_overview.md#execution-steps

From this guideline, we can see that:
1. `terraform init` is used to initialize the backend, install plugins, and check the configuration.
2. `terraform apply` is used to apply the plan in the cloud, with the `-auto-approve` flag.
3. Lastly, we can use `terraform destroy` to remove all resources and stacks from the cloud.

So the answer is **4**.

## Answer
`4. terraform init, terraform apply -auto-approve, terraform destroy`