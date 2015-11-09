# AWS Lambda Cron

An AWS Lambda function and its proper IAM configurations to make 'Cron as a Service' magic happens.

## Global Idea

The main idea of this project is to be able to do administrator and repetitive tasks in your entire infrestructure via tags. With this Lambda function you could, for example, shut down your development instances at a certain hour, writing a tag named "stopTime" with the value "0 18 * * 1-5".

This project is its very early days, there are a lot of work to do yet :)

## Set up a new Lambda Function.

You need to do some manual steps before start.

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

## Usage

You must write a proper tag in resources in order to perform some administrator task, such as stop or start an instance, generate a snapshot from an EBS, etc.

The name of the tag is the action, and the value is a cron expression, including wildcards, numbers, ranges and enumerations. Some examples are:

Tage Name | Tag Value | Description
--- | --- | ---
startTime | 0 9 * * 1-5 | (weekdays at 9AM, start my instances)
stopTime | 0 18 * * * |  (my instances must be stopped at 6PM)
startTime | 0 12 7,14,21 * * | (at 12 AM, the days 7, 14 and 21 of every month, start an instance)


### EC2

Tag your EC2 instances with this tags:

- startTime: Start the instance.
- stopTime: Stop the instance.
- more in progress... for example, rebootTime, terminateTime or createAMITime.

### EBS

Current supported tags for EBS Volumes are:

- createSnapshotTime: Generates a snapshot of the specific EBS Volume.

## Limitations

- Currently it only supports EC2 service. More services coming.
- The HOUR you define in cron, is Ireland Time (usually 1 hour less than Madrid time).
- When you configure the Lambda function, you specify time interval which Lambda function runs. You must match the "current" time (the exact time where Lambda function runs) with the exact time you define in your cron expression. Wildcards and ranges are recommended.
- The resources must be created out of Lambda before using this function.