### Codebuild scripting
* Boilerplate scripts for building github or codecommit code build setups




* to run:
```bash
 aws cloudformation create-stack --profile staging-us-west-1 --stack-name TestCodeBuild --template-body file://github_build.yaml --parameters file://parameters.json --capabilities CAPABILITY_IAM
```