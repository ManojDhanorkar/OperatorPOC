# OperatorPOC

git clone https://github.com/Sushrut-Persistent/OperatorPOC.git

cd OperatorPOC/

git clone https://github.com/talat-shaheen/vmstate-operator.git

cd vmstate-operator

operator-sdk init --domain xyzcompany.com --repo github.com/talat-shaheen/vmstate-operator
- Already initialized

operator-sdk edit --multigroup=true

operator-sdk create api --group=aws --version=v1 --kind=AWSEC2
- Resource already exists

operator-sdk create api --group=awsmanager --version=v1 --kind=AWSManager
- Resource already exists

make generate; 
make manifests; 
make docker-build docker-push IMG="quay.io/manoj_dhanorkar/vmstate-operator-st:v1.0"
make deploy IMG="quay.io/manoj_dhanorkar/vmstate-operator-st:v1.0"

kubectl create secret generic aws-secret --from-literal=aws-default-region=us-east-1 --from-literal=aws-secret-access-key=p4kwKEm8l8ZRi9xDGCNrfq9e6ifpKsC6pePBmZXM --from-literal=aws-access-key-id=AKIAWT4IN5FUDCYE2NMD -n vmstate-operator-st

kubectl apply -f config/samples/aws_v1_sushrutawsmanager.yaml -n vmstate-operator-st

kubectl apply -f config/samples/aws_v1_sushrutawsec2.yaml -n vmstate-operator-st

kubectl get all -n vmstate-operator-st
- No resources found in vmstate-operator-st namespace.