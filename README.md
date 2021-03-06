<p align="center">
  <img alt="Lambda Logo" title="AdonisJS" src="./.github/lambda-logo.png" width="200px" />
</p>

<h1 align="center">
  AWS Lamba (Serverless)
</h1>

This repository contains a simple lamba function to be deployed on AWS. It is responsible to capture events
on S3 then run a function located on `optimize.js` file.

# What the function does

Whenever the user uploads a <b>.JPG</b> or <b>.PNG</b> image on `uploads/` bucket, the lambda function is triggered to get the image and resize it to a new file, that will be placed on `compressed/` bucket.

# Setup

Follow the steps bellow to setup your development and AWS environments.

## AWS

First of all it is mandatory to create a new user to access your AWS environment. Access the <b>IAM</b> service on your AWS console. Select
`Users` then click the button "Add User". Give it a name and <b>Programmatic Access</b> to enable the <b>access key ID</b> and
<b>secret access key</b>.

In the next windows click the box <b>Attach existing policies directly</b> and give your user <b>AdministratorAccess</b>.

** Make sure you save the access key ID and secret access key on a private file.

## Development Environment
- Clone this repository running the `https://github.com/eduardo3g/aws-lambda-sample.git` command.
- Download development dependencies running `yarn install` or `npm install`.
- Add the Serverless dependency globally on your machine running the `yarn global add serverless` command.
- Open the project on VSCode.

You need to authenticate your machine to AWS by typing the command below. "-o" flag will overwrite you credentials if you have already
authenticated to
AWS before.
<br />
<b>IMPORTANT: <i>Do not use double quotes.</i></b>
<br />
`serverless config credentials -o --provider aws --key="ACCESS KEY ID" --secret "SECRET ACCESS KEY"`

### Renaming the S3 bucket name
S3 ia a AWS <b>GLOBAL</b> service, which means each S3 bucket must have a unique name among ALL buckets in the world.
<br />
Open the `serverless.yml` file and rename the bucket that will be created (highlighted fields). Don't forget to choose a unique name.
<br />

<p align="center">
  <img alt="Rename bucket name" title="Rename bucket name" src="./.github/rename-bucket.jpg" width="500px" />
</p>

### Choosing the region
If you don't specify the region you want to place your lambda function, it will be placed by default on <b>US East (N. Virginia) - <small>us-east-1</small></b>
<br />
In this example I chose <b>South America (São Paulo) - <small>sa-east-1</small></b> for a lower ping latency.
<br />

<p align="center">
  <img alt="Set the region" title="Set the region" src="./.github/set-region.jpg" width="496px" />
</p>

## Deploy
Once you've completed all the previous steps, deploy your function running `serverless deploy -v`. If you commited any mistakes, run
`serverless remove` to delete everything you've uploaded to AWS.

## Testing the lambda function
- Open S3 and find the bucket you've created (same name you chose on `serverless.yml` file).
- Create a subfolder called <b>uploads</b> and upload a image inside it.
- Once the upload is done, go back to the root directory and note a new subfolder called <b>compressed</b> has been created.
- The same image you've uploaded will be compressed inside it.
