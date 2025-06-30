# aws-lambda-injection
#🧠Inspiration

Modern cloud-native systems rely heavily on microservices and serverless architecture like AWS Lambda. While convenient, they are also vulnerable to unpredictable failures and cascading issues. Inspired by the principles of Chaos Engineering—popularized by Netflix’s Chaos Monkey—we wanted to intentionally inject failures into Lambda functions to make systems more resilient, fault-tolerant, and observable. The goal was to empower developers to test their assumptions and prepare for real-world failures before they happen in production.

##⚙️What it does
chaos_lambda is a Python library that lets you inject controlled failures into AWS Lambda functions using simple decorators. It supports:
Latency Injection: Add artificial delays (fault_type: "latency").
Exception Injection: Throw custom exceptions (fault_type: "exception").
HTTP Error Code Injection: Return specific error codes (fault_type: "status_code").
The configuration is pulled dynamically from AWS SSM Parameter Store, making it controllable in real-time—without code changes or redeployments. It also supports rate-based injection and per-function toggling via environment variables.

🛠️ How we built it
Used Python decorators to intercept Lambda execution and inject faults.
Stored fault configurations (like delay, error codes, exception message, etc.) in AWS Systems Manager Parameter Store.
Used boto3 to fetch configurations during Lambda runtime.
Enabled selective injection using the CHAOS_PARAM environment variable.
Added rate-limiting support to randomly inject faults based on defined probability.
Tested locally and deployed on AWS Lambda with IAM permissions for ssm:GetParameter.

🧗 Challenges we ran into
Managing fine-grained IAM permissions for accessing SSM parameters securely.
Ensuring fault injection logic doesn't break the Lambda's core functionality when disabled.
Implementing rate control accurately to reflect randomized behavior.
Simulating production-like behavior in a hackathon timeframe without full-scale infrastructure.

🏆 Accomplishments that we're proud of
Developed a working, deployable solution that brings Chaos Engineering to AWS Lambda, which is often underexplored.
Created a lightweight and easily pluggable decorator-based approach—minimal intrusion, maximum control.
Demonstrated real-world scenarios like latency spikes, thrown exceptions, and 5xx errors—all configurable remotely.

📚 What we learned
Gained deep insights into serverless observability and fault modeling.
Understood the importance of feature toggles via SSM to control experiments safely.
Practiced infrastructure as code principles while working with AWS IAM, Lambda, and SSM.
Explored chaos testing strategies and their impact on system resilience.

🚀 What's next for Chaos Injection for AWS Lambda - chaos_lambda
Add support for network-level faults, resource exhaustion, and cold-start simulation.
Build a Chaos Dashboard with real-time toggles and metrics.
Integrate with AWS CloudWatch and X-Ray for deeper observability.
Extend the library for Step Functions, Fargate, and other serverless components.
Contribute it as an open-source tool for DevOps teams practicing Chaos Engineering.
