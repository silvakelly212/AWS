# AWS - RobotFramework

Guia Passo a Passo  - Criar uma automação na AWS com Robot Framework

Automatizar tarefas na AWS (Amazon Web Services) usando o Robot Framework pode otimizar processos e melhorar a eficiência operacional. Abaixo, segue um guia passo a passo para ajudá-lo a configurar e executar automações na AWS com o Robot Framework.

## O que é o Robot Framework?

O Robot Framework é uma ferramenta de automação de testes de código aberto, baseada em Python, que utiliza uma sintaxe simples e legível. Ele é amplamente utilizado para testes de aceitação e desenvolvimento orientado a comportamentos.

## Pré-requisitos

Antes de começar, certifique-se de que você tem:

- **Uma Conta AWS**: Certifique-se de que você tem uma conta ativa na AWS.
- **Ambiente de Desenvolvimento Python**: Instale Python na sua máquina.
- **AWS CLI Configurado**: Instale e configure a AWS Command Line Interface (CLI) com suas credenciais de acesso.
- **Robot Framework**: Instale o Robot Framework em seu ambiente Python.

## Passo a Passo

### 1. Instalar o Robot Framework

Para instalar o Robot Framework, use o seguinte comando pip em seu terminal:

```bash
pip install robotframework
```

### 2. Configurar o plugin Robot Framework VSCode

- Clicar no botão de Configurações do plugin > Extension Settings
- Selecionar ```Robot Framework (Language Server)```

<img width="703" height="897" alt="Screen Shot 2025-08-01 at 10 46 28" src="https://github.com/user-attachments/assets/83eee76d-0a15-461e-9546-d48205685377" />

### 3. Configurar o plugin Python executable
- Na tela de configurações do plugin, adicionar o path do executável do python no campo ```Robot > Languagem-server: Python```
- Atenção selecione o executável do python que esta na pasta (do projeto)
- Exemplo: ```c:\User\user\VSCodeProjects\projeto-robotframework-aws\venv\Script\python.exe```
  
  <img width="1236" height="874" alt="Screen Shot 2025-08-01 at 11 39 12" src="https://github.com/user-attachments/assets/f361b439-afdc-4fe7-a97b-8ee8dff04bac" />

### 4. Configurar o plugin Idioma pt-BR
- Na tela de configuração do plugin, procure pelo campo Robot: ```Language```
- Clicar no botão ```Edit in settings.json```
- Adicionar a propriedade abaixo no sttings.json
  "robot.language":["pt-BR"]
  
<img width="1163" height="544" alt="Screen Shot 2025-08-01 at 11 50 26" src="https://github.com/user-attachments/assets/03f1ea2c-d4b6-4fa2-88bb-55ed036f384e" />

## Finalizar
- Após a configuração salvar e fechar os arquivos e renicie o VSCode

### 5. Instalar Bibliotecas Necessárias

Além do Robot Framework, você precisará instalar bibliotecas específicas para interagir com a AWS. Uma das bibliotecas mais utilizadas é a `robotframework-requests` para fazer chamadas HTTP.

```bash
pip install robotframework-requests
```

Para interagir diretamente com AWS, você pode usar a biblioteca `Boto3`, a qual permite acesso programático aos serviços AWS.
## Documentação Boto3 
(https://boto3.amazonaws.com/v1/documentation/api/latest/guide/credentials.html)

```bash
pip install boto3
```

### 6. Configurar a AWS CLI

Certifique-se de ter configurado a AWS CLI com suas credenciais de usuário, usando o seguinte comando:

```bash
aws configure
```

Você será solicitado a inserir suas credenciais de acesso, região padrão e formato de saída.

### 7. Estrutura de Projeto

## Pré-requisito
- Estrutura de pasta (Projeto) - basico
- .github \app \infra \tests \integration-tests
- Estrutura de pasta (Testes)
- .github \app \infra \tests \integration-tests \api \docs \scripts \steps \tests
  ```dentro da pasta tests deve conter os testes.robot e os arquivos de logs como log.html output.xml e report.html```
  
## Construção  
- api    # Diretório de arquivos para mapeamento dos contratatos (APIs)
- scripts   #Diretório de arquivos reponsável por mocks externos
- setups    #Diretório de arquivos responsável pela configuração dos serviços (DynamoDB, API Gateway, etc) utlizados
- tests     #Suítes de testes com as especificações em BDD


### 8. Criar o Arquivo de Teste do Robot Framework

Crie um arquivo de teste com extensão `.robot`. Por exemplo, `aws_automation.robot`.

```plaintext
*** Settings ***
Library           RequestsLibrary
Library           Boto3Library

*** Variables ***
${AWS_KEY}        sua_chave_aws_aqui
${AWS_SECRET}     seu_segredo_aws_aqui
${REGION}         us-east-1

*** Test Cases ***
Criar Nova Instância EC2
    [Documentation]    Teste de criação de instância EC2 na AWS
    Criar Instância EC2

*** Keywords ***
Criar Instância EC2
    [Arguments]    ${InstanceType}=t2.micro
    Create Instance    instance_type=${InstanceType}    region=${REGION}

OU
*** Settings ***
Library RequestsLibrary
Library Collections
Library Process
Library OperatingSystem
Library Boto3Library

*** Variables ***
${API_URL} https://seuserviço.aws.com.br
${AWS_ACCESS_KEY} sua_chave_de_acesso
${AWS_SECRET_KEY} sua_chave_secreta

*** Test Cases ***
Validar Serviço AWS
[Documentation] Este caso de teste valida um serviço AWS específico
Criar Sessão AWS ${AWS_ACCESS_KEY} ${AWS_SECRET_KEY}
${response}= GET ${API_URL}
Should Be Equal As Strings ${response.status_code} 200

```

### 9. Executar o Script de Automação

No terminal, execute o script do Robot Framework usando o seguinte comando:

```bash
robot aws_automation.robot
```

Este comando executará o arquivo de teste, que interage com a AWS para realizar a automação especificada.

### 10. Verificar Resultados

Após a execução, o Robot Framework gera relatórios e logs que podem ser usados para revisar os resultados dos testes e identificar quaisquer problemas.

```bash
output.xml
log.html
report.html
```

### Testes Manuais 


# Teste do Buckets S3 na AWS

O Amazon S3 (Simple Storage Service) é um serviço de armazenamento em nuvem altamente escalável, oferecido pela Amazon Web Services (AWS). Testar um Bucket S3 envolve criar um bucket, realizar operações básicas de upload e download, e configurar permissões e políticas. Abaixo está um guia passo a passo para ajudá-lo a testar o Buckets S3 na AWS.

## Criando um Bucket S3

1. **Acessar o Console AWS:**
   - Faça login na sua conta AWS e navegue até o console do Amazon S3.

2. **Criar um Novo Bucket:**
   - Clique em "Create bucket".
   - Insira um nome único para o bucket.
   - Escolha a região onde o bucket será armazenado. É importante escolher a região mais próxima dos seus usuários para otimizar a latência.
   - Configure as opções adicionais conforme necessário, como controle de versão e criptografia.
   - Clique em "Create bucket" para finalizar.

## Realizando Operações Básicas

### Upload de Arquivos

1. **Acessar o Bucket:**
   - No console do S3, clique no nome do bucket que você criou.

2. **Fazer Upload de um Arquivo:**
   - Clique no botão "Upload".
   - Arraste e solte os arquivos que deseja enviar ou clique em "Add files" para selecionar os arquivos do seu computador.
   - Clique em "Upload" para começar o envio.

### Download de Arquivos

1. **Selecionar o Arquivo:**
   - Navegue até o bucket e selecione o arquivo que deseja baixar.

2. **Baixar o Arquivo:**
   - Clique no botão "Download" para iniciar o download do arquivo para o seu computador.

## Configurando Permissões e Políticas

### Gerenciar Permissões do Bucket

1. **Acessar a Aba de Permissões:**
   - No bucket, clique em "Permissions".

2. **Configurar Permissões:**
   - Gerencie as permissões do bucket para controlar o acesso aos dados. Você pode adicionar políticas de bucket personalizadas para conceder ou restringir o acesso.

### Configurar Políticas de Bucket

1. **Adicionar uma Política de Bucket:**
   - Na aba "Permissions", clique em "Bucket Policy".
   - Insira uma política JSON para definir as permissões de acesso. Por exemplo, você pode permitir que todos os usuários da AWS tenham acesso de leitura ao bucket.

2. **Salvar as Alterações:**
   - Após inserir a política desejada, clique em "Save" para aplicar as alterações.

## Monitoramento e Testes Adicionais

- **Configurar Logs de Acesso:**
  - Habilite o logging de acesso para monitorar as solicitações feitas ao seu bucket.

- **Testar o Acesso:**
  - Use o AWS CLI ou SDKs para realizar operações de teste, como upload e download programáticos, para verificar se as permissões estão configuradas corretamente.

Seguindo estas etapas, você poderá testar e verificar a funcionalidade do Amazon S3 para garantir que ele atenda às suas necessidades de armazenamento e acessibilidade.


# Testar as Filas do SQS 

O Amazon Simple Queue Service (SQS) é um serviço de filas de mensagens que permite o desacoplamento e a escalabilidade de microsserviços, sistemas distribuídos e aplicações serverless. Testar as filas do SQS é uma parte essencial do desenvolvimento de sistemas que utilizam esse serviço. A seguir, apresentamos um guia sobre como realizar testes nas filas do SQS na AWS.

## Pré-requisitos

Antes de começar, certifique-se de que possui:

- Uma conta ativa na AWS.
- Configuração do AWS CLI em seu ambiente local.
- Permissões adequadas para acessar e manipular filas do SQS.

## Criando uma Fila SQS

1. **Acessar o Console AWS**: Entre no console da AWS e navegue até o serviço SQS.
2. **Criar uma nova fila**:
   - Clique em "Criar fila".
   - Escolha o tipo de fila (Standard ou FIFO).
   - Configure as opções da fila, como nome e tempo de visibilidade.
   - Clique em "Criar fila".

## Enviando Mensagens para a Fila

Para testar, você precisa enviar mensagens para a fila criada. Isso pode ser feito de várias maneiras:

### Usando o Console da AWS

1. Selecione a fila que você criou.
2. Clique em "Enviar e receber mensagens".
3. Insira uma mensagem no campo fornecido.
4. Clique em "Enviar mensagem".

### Usando o AWS CLI

```bash
aws sqs send-message --queue-url <URL_DA_SUA_FILA> --message-body "Mensagem de teste"
```

Substitua `<URL_DA_SUA_FILA>` pela URL da fila que você deseja testar.

## Recebendo Mensagens da Fila

### Usando o Console da AWS

1. Na mesma seção onde enviou mensagens, clique em "Receber mensagem".
2. As mensagens disponíveis serão exibidas.

### Usando o AWS CLI

```bash
aws sqs receive-message --queue-url <URL_DA_SUA_FILA>
```

Isso retornará mensagens atualmente disponíveis na fila.

## Excluindo Mensagens

Após processar as mensagens, é importante excluí-las para evitar processamento duplicado.

### Usando o AWS CLI

```bash
aws sqs delete-message --queue-url <URL_DA_SUA_FILA> --receipt-handle <RECEIPT_HANDLE>
```

Substitua `<RECEIPT_HANDLE>` pelo identificador de recebimento da mensagem.

## Considerações Finais

- **Testes Automatizados**: Considere usar frameworks de teste para automatizar esses processos em seus pipelines de CI/CD.
- **Monitoramento e Logs**: Ative o CloudWatch para monitorar e registrar a atividade das filas.
- **Permissões**: Assegure-se de que as credenciais usadas possuam as permissões necessárias para todas as operações SQS executadas.

Testar corretamente as filas do SQS é um passo crucial para garantir que seu sistema de mensagens funcione de forma eficaz e confiável. Cumprindo esses passos, você poderá validar e depurar suas filas SQS de maneira eficiente.
