### Codebuild scripting
* Boilerplate scripts for building github or codecommit code build setups




* to run:
```bash
 aws cloudformation create-stack --stack-name TestCodeBuild --template-body file://build.yaml --parameters file://parameters.json --capabilities CAPABILITY_IAM
```