# AWS - EKS Cluster

## Setting up AWS EKS (Hosted Kubernetes)

Documentação completa em https://www.terraform.io/docs/providers/aws/guides/eks-getting-started.html


### Download kubectl
```
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
chmod +x kubectl
sudo mv kubectl /usr/local/bin
```

### Download the aws-iam-authenticator
```
wget https://github.com/kubernetes-sigs/aws-iam-authenticator/releases/download/v0.3.0/heptio-authenticator-aws_0.3.0_linux_amd64
chmod +x heptio-authenticator-aws_0.3.0_linux_amd64
sudo mv heptio-authenticator-aws_0.3.0_linux_amd64 /usr/local/bin/heptio-authenticator-aws
```

### Modificar providers.tf para escolher sua região (Default - São Paulo)

Escolha sua região. EKS não está disponível em todas as regiões, Use a tabela de regiões para verificar se sua região suporta o EKS: https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/

Faća as alterações em `providers.tf`

### Terraform apply
```
terrafomr init
terrafomr plan
terraform apply
```

### Configure kubectl
```
terraform output kubeconfig # save output in ~/.kube/config
terraform output kubeconfig > ~/.kube/config
```

### See nodes coming up
```
kubectl get nodes
```

### Destroy
Para garantir que todos os recursos criados sejam removidos para não haver cobrança excessiva pela POC, execute o comando abaixo:
```
terraform destroy
```
