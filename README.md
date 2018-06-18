# Serverless / Node.js / Dynatrace
This is a sample app that shows how to deploy Dynatrace via serverless

## Setup

1. Install Node.js
2. Install serverless `npm install -g serverless`
3. Sett up AWS credentials as described [in the serverless docu](https://serverless.com/framework/docs/providers/aws/guide/credentials/)
3. [Install AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/installing.html)
4. Use `aws configure` to set credentials and zone (us-east-1)
5. Open Dynatrace and make sure that Lambda support is enabled
6. Click on 'Deploy Dynatrace', select 'Set up Serverless integration' and then 'Node.js'
7. Copy the DT_LAMBDA_OPTIONS environment settings
8. Paste the json into a file `.dynatrace-aws.json` - make sure it isn't committed (.gitignore is already set up)
9. Run `aws ssm put-parameter --name "/dynatrace/lambda/serverless-node-js/DT_LAMBDA_OPTIONS" --value "file://.dynatrace-aws.json" --type String --region us-east-1 --overwrite` on tghe terminal.
(The config path is arbitrary - it just needs to be consistent with the setting in serverless.yml, E.g. `DT_LAMBDA_OPTIONS: ${ssm:/dynatrace/lambda/serverless-node-js/DT_LAMBDA_OPTIONS}`)
10. Run `serverless deploy` on the console.