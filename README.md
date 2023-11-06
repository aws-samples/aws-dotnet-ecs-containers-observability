# BlogSample-ASPDotNetApp

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Introduction
This sample application is designed to demonstrate how to instrument .NET applications using OpenTelemetry.
It should be used alongside the [.NET Observability with OpenTelemetry blog series](https://aws.amazon.com/blogs/dotnet/net-observability-with-opentelemetry-part-1-metrics-using-amazon-prometheus-and-amazon-grafana/) for optimal
understanding and integration with AWS services.

## Getting Started

Deploy the cloudformation template using the following command:

```shell
$ aws cloudformation deploy --template ./blog-cf-template.yml --stack-name blog-solution-stack --capabilities CAPABILITY_NAMED_IAM --region us-east-1
```

This will deploy the following resources:
-	Amazon ECS cluster to run container images.
-	Application Load Balancer and target group to distribute traffic to the application.
-	Amazon Managed Service for Prometheus workspace to store metrics from the ADOT collector.
-	Amazon OpenSearch Service to store logs from the AWS for Fluent Bit sidecar.
-	Amazon Managed Grafana workspace to aggregate and visualize metrics, traces, and logs.
-	AWS Identity and Access Management (IAM) roles to provide Amazon ECS tasks with write permissions to AWS X-Ray, Amazon Managed Service for Prometheus, and Amazon OpenSearch Service.


## Update and Deploy the ADOT Service.

1. Add the private subnet IDs and the default security group ID from the CloudFormation output to the adot-service.json
2. Run the following command to launch the application service:

```shell
$  aws ecs create-service --cluster BlogCluster --cli-input-json file://adot-service.json --region us-east-1
```
## Update and Deploy the Application Service

1. Add the "targetGroupArn" from the CloudFormation output to the sample-app-service.json.
2. Run the following command to launch the application service:

```zsh
$   aws ecs create-service --cluster BlogCluster --cli-input-json file://sample-app-service.json --region us-east-1
```

## Monitoring Observability Signals
See the [.NET Observability with OpenTelemetry blog series.](https://aws.amazon.com/blogs/dotnet/net-observability-with-opentelemetry-part-1-metrics-using-amazon-prometheus-and-amazon-grafana/) blog series to learn 
how to monitor observability signals from the sample application.

## License

This library is licensed under the MIT-0 License. See the LICENSE file.


