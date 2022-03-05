Node Express application deployment to kubernetes cluster using helm.
Steps to follow
1) Create image using dockerfile and upload to dockerhub.
# docker build -n 03314839765/node:latest .
# docker login
# docker push 03314839765/node:latest
2) Create EKS cluster using terraform scripts in folder 'terraform-eks'.
# cd terraform-eks/
# aws configure
# terraform init
# terraform apply
3) Change image name in node-helm-demo/values.yaml as name of image in your dockerhub.
4) Deploy helm chart to that cluster.
# helm install node-helm-demo/ --generate-name

Following packages should be installed before starting this task. This installation is based on ubuntu 20.04.
......Helm Installation..........
curl https://baltocdn.com/helm/signing.asc | sudo apt-key add -
sudo apt-get install apt-transport-https --yes
echo "deb https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get update
sudo apt-get install helm

....Install AWS CLI.....
sudo apt install unzip -y
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
which aws

....Install kubectl....
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl
sudo curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg
echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
sudo apt-get install -y kubectl

....Install Terraform....
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
sudo apt-add-repository "deb [arch=$(dpkg --print-architecture)] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
sudo apt install terraform

....Install Docker....
sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
sudo apt install docker-ce -y
sudo systemctl status docker