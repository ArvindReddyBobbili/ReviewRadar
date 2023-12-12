# ReviewRadar
Movie Recommendation System
1. Login to AWS, Go to Cloud9 IDE service and create an environment.
2. Open the environment and in the terminal, run the following command -
        ```
        git clone https://github.com/ArvindReddyBobbili/ReviewRadar
        ```
3. Create an s3 bucket named cloudformation-template-store
and  key pair named review-radar

4. In cloud9 terminal, run this command to package the yaml files
    ```
    aws cloudformation package --template-file stacks/main-stack.yaml --output-template packaged.yaml --s3-bucket cloudformation-template-store --region us-east-1
    ```
5. Next, we will deploy the resources -
```
    aws cloudformation deploy --stack-name review-radar --template-file  packaged.yaml \
    --capabilities CAPABILITY_NAMED_IAM --region us-east-1

```

4. Few minutes later, all the infrastructure will be created, code and data files are uploaded to s3. We can cross-verify this by checking the services - VPC, GLue, SageMaker to see if any resources are created.

5. In Sagemaker, go to domain, and in domain settings add the existing execution role to 'Spaces' and Save.
6. We need to shift to SageMaker Domains, and select 'defaultuserprofile'
7. Create a Jupyter Labspace with a name of your choice, and instance type - ml.m5.xlarge
8. To get the code file into the lab -
```
    aws s3 cp s3://movie-recommendation-s3/code/movie-recommendation-system.ipynb .
```
9. Once the file is present in the directory, Open the file, Select Kernel from toolbar and choose 'Restart and Run All'
10. It will take a few minutes for the model to train, once done we can view the predictions in cell 48.
11. The clusters can also be viewed in AWS glue database by querying using Athena.
