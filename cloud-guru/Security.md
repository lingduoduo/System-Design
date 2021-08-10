**Security**

![Screen Shot 2021-08-06 at 8.36.44 PM](/Users/ling/Desktop/Screen Shot 2021-08-06 at 8.36.44 PM.png)

![Screen Shot 2021-08-06 at 8.38.54 PM](/Users/ling/Desktop/Screen Shot 2021-08-06 at 8.38.54 PM.png)

![Screen Shot 2021-08-06 at 8.39.30 PM](/Users/ling/Desktop/Screen Shot 2021-08-06 at 8.39.30 PM.png)

![Screen Shot 2021-08-06 at 8.50.27 PM](/Users/ling/Desktop/Screen Shot 2021-08-06 at 8.50.27 PM.png)

![Screen Shot 2021-08-06 at 8.51.04 PM](/Users/ling/Desktop/Screen Shot 2021-08-06 at 8.51.04 PM.png)

![Screen Shot 2021-08-06 at 8.51.35 PM](/Users/ling/Desktop/Screen Shot 2021-08-06 at 8.51.35 PM.png)

![Screen Shot 2021-08-06 at 8.52.05 PM](/Users/ling/Desktop/Screen Shot 2021-08-06 at 8.52.05 PM.png)

![Screen Shot 2021-08-06 at 8.52.51 PM](/Users/ling/Desktop/Screen Shot 2021-08-06 at 8.52.51 PM.png)

**CloudHSM**

![Screen Shot 2021-08-06 at 8.56.46 PM](/Users/ling/Desktop/Screen Shot 2021-08-06 at 8.56.46 PM.png)

![Screen Shot 2021-08-06 at 8.57.10 PM](/Users/ling/Desktop/Screen Shot 2021-08-06 at 8.57.10 PM.png)

![Screen Shot 2021-08-06 at 8.57.59 PM](/Users/ling/Desktop/Screen Shot 2021-08-06 at 8.57.59 PM.png)

**Systems Manager Parameter Store**

![Screen Shot 2021-08-06 at 9.05.16 PM](/Users/ling/Desktop/Screen Shot 2021-08-06 at 9.05.16 PM.png)

![Screen Shot 2021-08-06 at 9.05.32 PM](/Users/ling/Desktop/Screen Shot 2021-08-06 at 9.05.32 PM.png)

![Screen Shot 2021-08-06 at 9.06.50 PM](/Users/ling/Desktop/Screen Shot 2021-08-06 at 9.06.50 PM.png)

![Screen Shot 2021-08-06 at 9.07.39 PM](/Users/ling/Desktop/Screen Shot 2021-08-06 at 9.07.39 PM.png)

```
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow",
    "Action": [
      "logs:CreateLogGroup",
      "logs:CreateLogStream",
      "logs:PutLogEvents",
      "ssm:GetParameter*",
      "ssm:GetParametersByPath"
    ],
    "Resource": "*"
  }]
}
```

```
import json
import os
import boto3

client = boto3.client("ssm")
env = os.environ["ENV"]
app_config_path = os.environ["APP_CONFIG_PATH"]
full_config_path = "/" + env + "/" + app_config_path


def lambda_handler(event, context):

    print("Config Path: " + full_config_path)

    param_details = client.get_parameters_by_path(
        Path=full_config_path, Recursive=True, WithDecryption=True
    )

    print(json.dumps(param_details, default=str))
```

![Screen Shot 2021-08-09 at 9.32.17 PM](/Users/ling/Desktop/Screen Shot 2021-08-09 at 9.32.17 PM.png)

