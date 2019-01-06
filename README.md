# PPTP Server - CloudFormation

Deploying a Private VPN to AWS EC2 using CloudFormation

[![https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=pptp-vpn&templateURL=https://s3.amazonaws.com/devopstar/resources/aws-pptp-cloudformation/pptp-server.yaml)

## Quickstart

Make the neccessary changes to the `pptp-server-params.json` file, being sure to define new username & password parameters

```json
{
    "ParameterKey": "VPNUsername",
    "ParameterValue": "nathan"
},
{
    "ParameterKey": "VPNPassword",
    "ParameterValue": "passw0rd1"
},
{
    "ParameterKey": "VPNPhrase",
    "ParameterValue": "passw0rd1"
},
```

The template **can be deployed** using the AWS cli by running the following:

```bash
aws cloudformation create-stack --stack-name "pptp-vpn" \
    --template-body file://pptp-server.yaml \
    --parameters file://pptp-server-params.json \
    --region us-east-1
```

**Note:** The `--region` parameter is used to define which region the VPN should be deployed to.

Get details, including the Server address for your VPN:

```bash
aws cloudformation describe-stacks --stack-name "pptp-vpn" \
    --region us-east-1 \
    --query 'Stacks[0].Outputs[?OutputKey==`VPNServerAddress`].OutputValue' \
    --output text
```

## Attribution

This configuration is based on the work done by [webdigi](https://github.com/webdigi) who's work can be founds below:

- [How to setup your own private, secure, free* VPN on the Amazon AWS Cloud in 10 minutes](https://www.webdigi.co.uk/blog/2015/how-to-setup-your-own-private-secure-free-vpn-on-the-amazon-aws-cloud-in-10-minutes/)
- [AWS-VPN-Server-Setup](https://github.com/webdigi/AWS-VPN-Server-Setup)
