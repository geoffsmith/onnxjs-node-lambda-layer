### Description

Files needed to build a lambda layer containing the onnxjs-node library including binaries compiled to run on lambda. Note: this will only work on the AWS node 10.x environment.

### Instructions

* Run a docker image to build the node packages

`docker run -ti --rm -v (pwd)/code:/var/task -v (pwd)/layer:/opt lambci/lambda:build-nodejs10.x /bin/bash`

* `npm i` to build the packages
* Copy `/lib64/libgomp*` to `package/lib64/`
* Package and deploy using SAM

```
sam package --template-file template.yaml  --s3-bucket <YOUR_BUCKET> --output-template-file out.yaml
sam deploy --template-file out.yaml --stack-name <YOUR_STACK_NAME> --capabilities CAPABILITY_IAM --region <YOUR_REGION>
```

* Get the ARN from the AWS console for the layer
* Use the layer in your lambda

