<br/>
<div align="center">
<h1 align="center">Smart Classroom Face Detection Using AWS Lambda</h1>
</div>
Our cloud app will include an assistant for a smart classroom setup. This assistant collects videos from the user's classroom, performs face recognition on the collected videos, searches the database for the recognized students, and returns the relevant academic information for each student to the user. 

### The Architecture

The smart classroom application uses Amazon Lambda functions triggered by new videos uploaded to an S3 bucket. The Lambda functions perform face recognition on the video frames using a Python library. Matches are searched for in a DynamoDB database containing student records. The Lambda function outputs a CSV file with academic information for recognized students. This serverless architecture allows the system to scale automatically based on usage. Key components are Lambda, S3 for storage, DynamoDB for the database, and Docker containers for packaging dependencies. The overall flow is uploading videos to S3 triggers Lambda functions to process the videos, lookup student info, and output results.

<!-- GETTING STARTED -->

![visualization](https://github.com/dhanrajbhosale/PaaS-AWS-smart-classroom/blob/59e6354fec99b948900e520f2c4f48c83771dbf5/architecture.png?raw=true)

## Getting Started

To get a local copy up and running follow these simple steps.

### Prerequisites

* [Install Python](https://www.python.org/downloads/)
* [Install AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
* [Install Docker](https://docs.docker.com/engine/install/)

### Installation

1. Clone the repo

```sh
git clone https://github.com/dhanrajbhosale/PaaS-AWS-smart-classroom.git
```

2. Configure AWS

```sh
aws configure
```

When you enter this command, the AWS CLI prompts you for four pieces of information:

    * Access key ID
    * Secret access key
    * AWS Region
    * Output format

3. Add your S3 Bucket and DynamoDB table name here at (S3 bucket name should be unique globally)

   `my_constants.py`: [configurations](https://github.com/dhanrajbhosale/PaaS-AWS-smart-classroom/blob/af49ecf6b780c556c72fcdfb1f58fde12129a86e/configurations/my_constants.py)

4. Running AWS CDK Project

The `cdk.json` file tells the CDK Toolkit how to execute your app.

This project is set up like a standard Python project. The initialization
process also creates a virtualenv within this project, stored under the `.venv`
directory.  To create the virtualenv it assumes that there is a `python3`
(or `python` for Windows) executable in your path with access to the `venv`
package. If for any reason the automatic creation of the virtualenv fails,
you can create the virtualenv manually.

To manually create a virtualenv on MacOS and Linux:

```sh
$ python -m venv .venv
```

After the init process completes and the virtualenv is created, you can use the following
step to activate your virtualenv.

```sh
$ source .venv/bin/activate
```

If you are a Windows platform, you would activate the virtualenv like this:

```sh
% .venv\Scripts\activate.bat
```

Once the virtualenv is activated, you can install the required dependencies.

```sh
$ pip install -r requirements.txt
```

Do bootstrap once

```sh
$ cdk bootstrap
```

Bootstrapping is the process of provisioning resources for the AWS CDK before you can deploy AWS CDK apps into an AWS environment. (An AWS environment is a combination of an AWS account and Region).

These resources include an Amazon S3 bucket for storing files and IAM roles that grant permissions needed to perform deployments.

The required resources are defined in an AWS CloudFormation stack, called the bootstrap stack, which is usually named CDKToolkit. Like any AWS CloudFormation stack, it appears in the AWS CloudFormation console once it has been deployed.

At this point you can now synthesize the CloudFormation template for this code.

```sh
$ cdk synth
```

Deploy this stack to your default AWS account/region

```sh
$ cdk deploy
```

To add additional dependencies, for example other CDK libraries, just add
them to your `setup.py` file and rerun the `pip install -r requirements.txt`
command.

## Useful commands

* `cdk ls`          list all stacks in the app
* `cdk synth`       emits the synthesized CloudFormation template
* `cdk deploy`      deploy this stack to your default AWS account/region
* `cdk diff`        compare deployed stack with current state
* `cdk docs`        open CDK documentation

### Running the project

Run the [Workload Generator](https://github.com/dhanrajbhosale/PaaS-AWS-smart-classroom/blob/af49ecf6b780c556c72fcdfb1f58fde12129a86e/workload.py)

```sh
$ python workload.py
```

<!-- USAGE EXAMPLES -->

## Usage

Users submit videos to your S3 input bucket. When a new video is added to the input bucket, the Lambda function is triggered to process it. When a new video is added to the input bucket, the Lambda function is triggered to process it. The Lambda function then employs the Python face recognition library to recognize faces in the frames. The Lambda function searches DynamoDB for the academic information of the first recognized face.
