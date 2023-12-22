# terraform-sshkey-aws
- [x] Status:  Ainda em desenvolvimento.
###
### Módulo para criar uma chave Key Pairs . 
Para utilizar este módulo é necessário os seguintes arquivos especificados logo abaixo:

   <summary>versions.tf - Arquivo com as versões dos providers.</summary>

```hcl
terraform {
  required_providers {
    aws = {
      source = "hashicorp/aws"
      version = "5.31.0"
    }
  }
}
```
#
<summary>main.tf - Arquivo que irá consumir o módulo para criar a infraestrutura.</summary>

```hcl
provider "aws" {
  region  = var.region
}

module "ssh-key" {
  source    = "git::https://github.com/israeldoamaral/terraform-sshkey-aws"
  namespace = "Nome_da_chave"
}

```

#
<summary>outputs.tf - Outputs de recursos que serão utilizados em outros módulos.</summary>

```hcl
output "ssh_keypair" {
  value = module.ssh-key.ssh_keypair
  sensitive = true
}


output "key_name" {
  value = module.ssh-key.key_name
}
```

## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 0.15.4 |
| <a name="requirement_aws"></a> [aws](#requirement\_aws) | >= 3.0 |

## Providers

No providers.

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_network"></a> [network](#module\_network) | github.com/israeldoamaral/terraform-sshkey-aws | n/a |

## Resources

No resources.

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_namespace"></a> [cidr](#input\_namespace) | Nome da chave de acesso Ex: "terraform" | `string` | `" "` | yes |

## Outputs

No outputs.
#
## Como usar.
  - Para utilizar localmente crie os arquivos descritos no começo deste tutorial, main.tf, versions.tf, variables.tf e outputs.tf.
  - Após criar os arquivos, atente-se ao valor default da variável "namespace", pois pode ser alterado de acordo com sua necessidade. 
  - Certifique-se que possua as credenciais da AWS - **`AWS_ACCESS_KEY_ID`** e **`AWS_SECRET_ACCESS_KEY`**.

### Comandos
Para consumir os módulos deste repositório é necessário ter o terraform instalado ou utilizar o container do terraform dentro da pasta do seu projeto da seguinte forma:

* `docker run -it --rm -v $PWD:/app -w /app --entrypoint "" hashicorp/terraform:light sh` 
    
Em seguida exporte as credenciais da AWS:

* `export AWS_ACCESS_KEY_ID=sua_access_key_id`
* `export AWS_SECRET_ACCESS_KEY=sua_secret_access_key`
    
Agora é só executar os comandos do terraform:

* `terraform init` - Comando irá baixar todos os modulos e plugins necessários.
* `terraform fmt` - Para verificar e formatar a identação dos arquivos.
* `terraform validate` - Para verificar e validar se o código esta correto.
* `terraform plan` - Para criar um plano de todos os recursos que serão utilizados.
* `terraform apply` - Para aplicar a criação/alteração dos recursos. 
* `terraform destroy` - Para destruir todos os recursos que foram criados pelo terraform. 
