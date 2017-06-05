### terraform-scheduled-batch-job

A [Terraform](https://www.terraform.io/) module representing a scheduled [Batch job](https://aws.amazon.com/batch/).  Uses a Cloud Watch Event Rule and a Lambda function to submit the Batch job on a cron schedule.  Use of the Batch service overcomes two of Lambda's current limitations:

- jobs can run longer than five minutes
- jobs run as containers so they can be written in any language

TODO: Consider including the Batch infrastructure setup inside this module once the Batch Terraform provider is available.

### usage example

```terraform
provider "aws" {
  region  = "us-east-1"
}

module "scheduled-batch-job" {
  source = "github.com/turnerlabs/terraform-scheduled-batch-job?ref=v0.1.0"

  name                 = "my-scheduled-job"
  batch_job_definition = "my-job-definition"
  batch_job_queue      = "my-job-queue"
  schedule_expression  = "rate(1 hour)"
  
  tags = "${map("team", "my-team", "contact-email", "my-team@my-company.com", "application", "my-app", "environment", "dev", "customer", "my-customer")}"  
}
```

### outputs

- cloudwatch_event_rule_arn
- aws_lambda_function_arn
