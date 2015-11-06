# AWS Lambda Cron

An AWS Lambda function and its proper IAM configurations to make 'Cron as a Service' magic happens.

## Global Idea

The main idea of this project is to be able to do administrator and repetitive tasks in your entire infrestructure via tags. With this Lambda function you could, for example, shut down your development instances at a certain hour, writing a tag named "stopTime" with the value "0 18 * * 1-5".

This project is its very early days, there are a lot of work to do yet :)

## Set up a new Lambda Function.

- Access to Lambda service in your AWS console.
- Click on "Create a Lambda function".
- Select "lambda-canary" template. This template say that you are going to use python as programming languaje, .and you are also using Lambda as a scheduling event.
- Choose a name for your scheduled event.
- Write a [relevant] description.
- Select the time which your function will be executed (1 hour is enough for most of the cases).
- Click Next.

- Select a Name for your function. Something like 'LambdaCron', to be original :)
- Write a [relevant] description.
- The Runtime must be python2.7
- Copy&Paste the code in lambdaCron.py in the textarea below.
- Create a Role with lambdaCronIAM.json permissions and associate to this function.
- Default values for the advanced settings should fit. Maybe increment timeout to 30 secs...

