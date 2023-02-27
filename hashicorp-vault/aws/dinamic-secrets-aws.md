## Enable aws secret
vault secrets enable aws

## List all secrets enable
vault secrets list

## get aws credentials
head ~/.aws/credentials

## set aws credentials in new aws secret
vault write aws/config/root access_key=AKIAXXXXXXXXXX secret_key=XXXXXXXXXXXXXX region=us-east-1

## read new data in aws secret
vault read aws/config/root

## Create a json file with a policy

```bash
$ cat policy_example_vault.json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "ec2:*",
      "Resource": "*"
    }
  ]
}
```

## Create a role in aws secret
vault write aws/roles/my-role credential_type=iam_user policy_document=@policy_example_vault.json

## Generate a temporary aws credential 
vault read aws/reds/my-role
