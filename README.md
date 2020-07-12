# Deploying NextCloud on EKS ,Used MySQL as database for nextCloud,and integrated various aws services with EKS cluster.

![nextcloud + eks banner](https://raw.githubusercontent.com/krrajpurohit/nextCloudOnEKS/master/banner.jpeg)

## Getting started
- create an aws user with adminaccess<br>
- install awscli2<br>
- configure awscli with access key and secret key<br>
- install eksctl<br>

### Step1: Create EKS cluster and configure the kubectl config files
```bash
eksctl create cluster -f cluster.yaml
aws eks update-kubeconfig --name nextcluster
```
### Step2: Install Amazon EFS Utilities on every node in the cluster using following command:
```bash
yum install amazon-efs-utils
```
### Step3: Create namespace for easy management of resources,and set it as default
```bash
kubectl create namespace nextns
kubectl --set-context --current --namespace=nextns
```
### Step4: Create an EFS file system using aws console
### Step5: In *create-efs-provisioner.yaml* file, replace the <Strong>FILE_SYSTEM_ID</strong> and <strong>nfs server</strong> with the values of your EFS file system
### Step6: Run the *kustomization.yaml* file to setup the environment and deploy the nextcloud with other resources on the EKS. Run the following command:
```bash
kubectl create -k . -n nextns
```
### Step7: Now our nextcloud is deployed to the EKS and can be accessed using the <strong>EXTERNAL-IP</strong> provided by nextcloud service.
```bash
kubectl get all
```
### copy <strong>EXTERNAL-IP</strong> provided by the <strong>service/nextcloud</strong> in the browser to login to nextcloud.

## You can find a detailed article about this project at:

[Deploying NextCloud on EKS and Integrating with AWS EFS , ELB](https://medium.com/@kuldeep.rajpurohit/deploying-nextcloud-on-eks-and-integrating-aws-efs-and-elb-8941486c63d9
)


