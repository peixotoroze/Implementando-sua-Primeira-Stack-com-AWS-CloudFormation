DESAFIO 3: IMPLEMENTANDO SUA PRIMEIRA STACK COM AWS CLOUDFORMATION


Este repositório documenta de forma simples, a criação de uma infraestrutura básica na AWS usando AWS CloudFormation.

O objetivo foi criar uma **Stack** (conjunto de recursos) a partir de um arquivo **template declarativo**, mostrando como provisionar infraestrutura como código (IaC).


CloudFormation

O **CloudFormation** funciona como a “planta baixa” da sua infraestrutura na AWS.  
Em vez de criar recursos manualmente pelo console (lento e propenso a erros), declaramos **o que queremos** em um arquivo YAML ou JSON.

**Benefícios:**
- Repetibilidade: a mesma infraestrutura pode ser recriada em qualquer região.  
- Segurança: tudo é auditável e previsível.  
- Automação: um clique para criar ou atualizar a Stack.


Termos importantes:

| Termo | Função no CloudFormation |
|-------|-------------------------|
| **Template** | Arquivo YAML/JSON com a descrição detalhada da infraestrutura |
| **Stack** | Conjunto de recursos (EC2, S3, etc.) gerenciado como uma unidade |
| **Rollback** | “Botão Desfazer”: se algo falhar, a Stack volta ao estado anterior |

Implementação da STACK:

O template principal (`templates/infrastructure-stack.yaml`) criou um ambiente básico para qualquer aplicação na nuvem.

**Recursos Provisionados:**
- **Máquina Virtual (EC2):** instância t2.micro  
- **Segurança de Rede (SecurityGroup):** firewall que permite SSH (porta 22)  
- **Armazenamento de Objetos (S3):** bucket simples  
- **Identidade e Acesso (IAM):** IAMUser e IAMGroup  

Funcionalidades e Aprendizados do Template

| YAML | o que tem | pra que serve|
|---------------|---------------|--------------------|
| **Parameters** | Variáveis de entrada (ex: InstanceType) | Flexibilidade: altera a máquina sem mudar o código base |
| **Mappings** | Tabelas de valores (ex: UbuntuMap) | Permite rodar o template em qualquer região, buscando a AMI correta |
| **!Ref (Referência)** | Conecta recursos (ex: !Ref EC2SecurityGroup) | Garante a criação correta e ordem dos recursos |
| **UserData + Fn::Base64** | Scripts de inicialização | Automatiza comandos no primeiro boot da EC2 (ex: instalar Apache, Python) |

---

EXEMPLO: Servidor Web Rápido

O arquivo `webserver-apache.yaml` cria rapidamente um servidor web:

1. Cria o **Security Group** (firewall)  
2. Cria a **instância EC2**, referenciando o firewall  
3. Executa script de inicialização para instalar e iniciar o Apache  

Se alguma etapa falhar, o CloudFormation tenta **reverter automaticamente** as alterações.

Este desafio me permitiu:

- Transformar a teoria em prática usando **IaC**  
- Entender como criar ambientes **escaláveis, repetíveis e confiáveis**  
- Consolidar conhecimentos sobre AWS e CloudFormation  


Material de apoio: Documentação oficial da AWS: https://docs.aws.amazon.com/cloudformation/index.html)  
