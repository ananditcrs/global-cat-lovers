This is Global Cat lovers serverless Project setup.

Lets setup some ENV variables

$ export profile="catlovers"

$ export region="us-east-1"

$ export bucket="global-cat-lovers-bucket"

It is now time to deploy the api. Replace these with values that match your setup.

First, we create the bucket on aws to store our cloudformation template. If you already have a bucket for that, you can skip this.

$ aws s3api create-bucket --bucket ${bucket} --create-bucket-configuration LocationConstraint=${region} --profile ${profile}

## Steps for Setup

Edit the config.json file and change the name of the bucket, you could rename the project by editing the service name in serverless.yml as you wish

## Deployment Steps

Use Serverless Framework for deployment. Install the dependecies with `npm install` and then run `sls deploy` in the project root to start the deployment.

Lambda@Edge functions deployed to the North Virginia (us-east-1) region. From there the functions are replicated to edge locations.

## How to Test
go to command primpt and presumed your AWS CLI installed and configured to your account

aws cloudfront list-distributions --query DistributionList.Items[*][DomainName,Comment] --region ${region}

Pick the domain name from the list and run curl https://DOMAIN_NAME/url. Copy the response and then run following snippet.

curl --request PUT \
     --url "URL_FROM_RESPONSE" \
     --verbose \
     --data "My data"
You should be seeing some response from Lambda function w/ all required Pre-signed stuffs.

Note: Tracking What all presigned url used and which all not used we could trigger lamda functions on s3 bucket event object and store it into dynmodb.




