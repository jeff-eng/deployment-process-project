# Pipeline

## Diagram of the Pipeline Process
![Pipeline Diagram](/docs/diagrams/udagram_pipeline.jpg)

## Overview of the Pipeline Process
1. **Developer pushes commit to GitHub branch.**
    1. The pipeline process begins when the developer pushes a commit to the project's GitHub repository.
    2. CircleCI is a pipeline-as-a-service which is connected to the 'main' branch of the GitHub repository for this project.
2. **Pipeline triggered on commit push to branch.**
    1. Since CirclCI is connected to the GitHub repository's 'main' branch, the GitHub commit in the previous step triggers the CircleCI pipeline which we have configured in the `config.yml` file.
    2. CircleCI spins up an environment which installs Node.js, AWS CLI, and other processes required for running the pipeline.
    3. The `config.yml` file specifies the CircleCI pipeline to run the build, hold, and deploy jobs (in that order).
        - The *build job* runs the install scripts to install dependencies, then the script to lint the code, then the build scripts to build the front-end and backend.
        - The *hold job* is the next phase in the pipeline which is dependent upon the successful completion of the build job. This step typically requires manual approval before the deploy job can run.
        - The *deploy job* is the last phase in the CircleCI pipeline which runs the deploy script. This job handles running the EB and AWS CLI commands for deployment to AWS.
3. **CircleCI deploys the code to AWS Cloud Services including S3 and Elastic Beanstalk which host the front-end and backend app.**
    1. The deploy job in the pipeline handles running the deploy scripts in the front-end and backend to build and deploy the code to AWS S3 and Elastic Beanstalk.
    2. Code is deployed to AWS S3 and Elastic Beanstalk.
    3. The CI/CD pipeline is complete!