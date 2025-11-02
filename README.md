# AWS CloudFormation – Primeira Stack na AWS

## Introdução
Este repositório documenta a criação e gerenciamento de uma **Stack AWS CloudFormation**, com foco em compreender a infraestrutura como código (IaC) na AWS.  
Durante o processo, também são abordados os conceitos de **monitoramento (CloudWatch)** e **auditoria (CloudTrail)**.

---

## Objetivos do Laboratório
- Implementar uma Stack simples utilizando **AWS CloudFormation**.  
- Compreender o ciclo de vida de uma Stack (criação, atualização e exclusão).  
- Integrar ferramentas de observabilidade da AWS para monitorar e auditar recursos.  
- Documentar o processo técnico de forma clara e reprodutível.  

---

## Conceitos Fundamentais

### AWS CloudFormation
Serviço de **Infraestrutura como Código (IaC)** que permite criar e gerenciar recursos AWS por meio de templates em **YAML** ou **JSON**.  
Principais vantagens:
- Padronização de ambientes.  
- Automação do provisionamento.  
- Controle de versionamento e reprodutibilidade.

**Exemplo simples de Template:**
```yaml
AWSTemplateFormatVersion: '2010-09-09'
Description: Criação de um bucket S3 com CloudFormation

Resources:
  S3BucketExemplo:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: meu-bucket-exemplo-cloudformation
```

## AWS CloudWatch

Serviço de monitoramento e observabilidade que coleta métricas, logs e eventos dos recursos AWS.

Aplicações no laboratório:

Monitorar status da Stack.

Configurar alarmes para falhas de deploy.

Registrar logs de aplicações e infraestrutura.

## AWS CloudTrail

Serviço de auditoria e governança, responsável por registrar todas as chamadas de API feitas na conta AWS.

Aplicações no laboratório:

Rastrear alterações na Stack.

Auditar ações de usuários e serviços.

Integrar com CloudWatch para alertas de segurança.

## Etapas de Implementação

1. Criação do Template CloudFormation

Desenvolver um arquivo template.yaml contendo a definição dos recursos desejados (ex: S3, EC2, Lambda).

Validar o template localmente:

```
aws cloudformation validate-template --template-body file://template.yaml
```

2. Deploy da Stack

Executar a criação da Stack via CLI:

```
aws cloudformation create-stack \
  --stack-name primeira-stack \
  --template-body file://template.yaml \
  --capabilities CAPABILITY_IAM
```

Acompanhar o progresso no Console AWS > CloudFormation > Events.

3. Monitoramento e Logs

CloudWatch: criar um dashboard para monitorar métricas dos recursos provisionados.

CloudTrail: garantir que os logs de ações estejam sendo gravados e armazenados em um bucket S3 designado.

## Boas Práticas e Considerações

Utilizar parâmetros e saídas (Outputs) no template para torná-lo reutilizável.

Aplicar versionamento do template no GitHub.

Configurar CloudWatch Alarms para falhas de stack.

Garantir políticas de segurança no CloudTrail (criptografia e retenção de logs).
