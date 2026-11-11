# TaskFlow AI

**Uma aplicação Full Stack para gerenciamento inteligente de tarefas**

Projeto prático de estudos em **desenvolvimento de software,
Inteligência Artificial e DevOps**, utilizando C#, JavaScript, Docker,
Kubernetes e CI/CD.

------------------------------------------------------------------------

## Sobre o projeto

O **TaskFlow AI** é uma aplicação de gerenciamento de tarefas que
combina recursos tradicionais de produtividade com funcionalidades
baseadas em Inteligência Artificial.

A proposta é permitir que usuários cadastrem, organizem e acompanhem
tarefas, enquanto um serviço baseado em LLM (*Large Language Model*)
auxilia na interpretação de descrições, sugestão de categorias,
definição de prioridades e geração de resumos.

Além das funcionalidades da aplicação, o projeto será utilizado para
praticar um fluxo moderno de desenvolvimento e entrega de software:
construção de uma API, integração com banco de dados, containerização,
orquestração e automação de processos CI/CD.

> **Objetivo principal:** integrar desenvolvimento Full Stack,
> Inteligência Artificial e práticas DevOps em um projeto real,
> evolutivo e documentado.

## Objetivos do projeto

-   Desenvolver uma API REST com C# e ASP.NET Core.
-   Construir uma interface web com HTML5, CSS3 e JavaScript Vanilla.
-   Persistir os dados utilizando SQL Server.
-   Integrar um modelo de linguagem para auxiliar na organização das
    tarefas.
-   Executar os componentes em containers Docker.
-   Orquestrar a aplicação utilizando Kubernetes.
-   Automatizar build, testes e publicação com GitHub Actions.
-   Aplicar boas práticas de segurança, configuração e documentação.

## Funcionalidades planejadas

  -----------------------------------------------------------------------
  Funcionalidade                      Descrição
  ----------------------------------- -----------------------------------
  Gerenciamento de tarefas            Criar, consultar, editar e excluir
                                      tarefas.

  Classificação com IA                Interpretar descrições e sugerir
                                      categorias.

  Priorização assistida               Recomendar prioridades com base no
                                      contexto informado.

  Resumos inteligentes                Gerar resumos de tarefas e
                                      atividades.

  API REST                            Disponibilizar operações para
                                      integração com o frontend.

  Autenticação                        Proteger endpoints utilizando JWT.
  -----------------------------------------------------------------------

*As funcionalidades serão implementadas progressivamente durante a
evolução do projeto.*

## Tecnologias utilizadas

### Backend

-   **C#** --- linguagem principal da API.
-   **ASP.NET Core Web API (.NET 10)** --- construção dos endpoints
    REST.
-   **Entity Framework Core** --- acesso e persistência de dados.
-   **JWT** --- autenticação e autorização.

### Frontend

-   **HTML5** --- estrutura das páginas.
-   **CSS3** --- estilos e layout responsivo.
-   **JavaScript Vanilla** --- interação com a API e comportamento da
    interface.

### Banco de dados

-   **Microsoft SQL Server** --- armazenamento das tarefas e demais
    dados.

### Inteligência Artificial

-   **LLMs (Large Language Models)** --- interpretação de texto e
    geração de sugestões.
-   **API de provedor de IA** --- comunicação entre o backend e o modelo
    de linguagem.
-   **JSON estruturado** --- formato de resposta para integração
    controlada com a aplicação.

A integração com IA será realizada pelo backend. Chaves de API e
credenciais não devem ser expostas no frontend, no repositório ou nas
imagens Docker.

### Containers e orquestração

-   **Docker** --- criação e execução de imagens e containers.
-   **Docker Compose** --- execução local dos serviços integrados.
-   **Kubernetes** --- gerenciamento de Pods, Deployments, Services e
    configurações.
-   **Minikube** --- ambiente Kubernetes local.
-   **kubectl** --- ferramenta de linha de comando para administrar o
    cluster.

### CI/CD e versionamento

-   **Git** --- controle de versão.
-   **GitHub** --- hospedagem do código-fonte.
-   **GitHub Actions** --- automação de build, testes e publicação.
-   **GitHub Container Registry (GHCR)** --- armazenamento das imagens
    Docker.

## Arquitetura proposta

``` text
                  FRONTEND WEB
             HTML + CSS + JavaScript
                         |
                      HTTP/REST
                         |
                         v
                ASP.NET CORE WEB API
                    C# / JWT
                    /       \
                   /         \
                  v           v
           SQL SERVER      SERVIÇO DE IA
                          API DE UM LLM

        CONTAINERIZAÇÃO: DOCKER / COMPOSE
        ORQUESTRAÇÃO: KUBERNETES / MINIKUBE
        AUTOMAÇÃO: GITHUB ACTIONS -> GHCR -> KUBERNETES
```

O frontend se comunica com a API por HTTP. A API concentra as regras de
negócio, valida os dados, persiste as informações no SQL Server e
consulta o serviço de IA quando necessário.

Docker padroniza a execução dos componentes. Kubernetes será utilizado
para praticar implantação e gerenciamento da aplicação. O pipeline CI/CD
automatiza as etapas de validação e publicação.

## Fluxo CI/CD

O fluxo de automação planejado será:

1.  O desenvolvedor envia alterações para o repositório GitHub.
2.  O GitHub Actions obtém o código-fonte.
3.  O pipeline restaura as dependências e compila a aplicação.
4.  Os testes automatizados são executados.
5.  Uma imagem Docker é construída.
6.  A imagem é publicada no GitHub Container Registry.
7.  Uma etapa de implantação atualiza a aplicação no Kubernetes.

A publicação e a implantação serão configuradas progressivamente. Um
deploy em cluster remoto exige credenciais e permissões específicas, que
deverão ser armazenadas com segurança.

## Estrutura de diretórios prevista

``` text
TaskFlowAI/
|
|-- TaskFlow.Api/
|   |-- Controllers/
|   |-- Services/
|   |-- Models/
|   |-- Data/
|   |-- Dockerfile
|
|-- TaskFlow.Tests/
|
|-- frontend/
|   |-- index.html
|   |-- css/
|   |-- js/
|
|-- k8s/
|   |-- deployment.yaml
|   |-- service.yaml
|   |-- configmap.yaml
|   |-- secret.yaml
|
|-- .github/
|   |-- workflows/
|       |-- pipeline.yml
|
|-- compose.yaml
|-- .gitignore
|-- README.md
```

*A estrutura poderá ser ajustada conforme a implementação evoluir.*

## Como executar

Os comandos abaixo representam o fluxo inicial de execução local. Os
arquivos de configuração e os serviços necessários devem estar
preparados antes de executar cada etapa.

### Pré-requisitos

-   Git
-   .NET 10 SDK
-   Docker Desktop com WSL2 (Windows)
-   Visual Studio Code ou Visual Studio
-   Minikube e kubectl (para os exercícios de Kubernetes)

### Executar a API localmente

``` bash
cd TaskFlow.Api
dotnet restore
dotnet run
```

### Construir e executar com Docker

Na pasta que contém o Dockerfile:

``` bash
docker build -t taskflow-api:1.0 .
docker run --rm -p 8080:8080 taskflow-api:1.0
```

### Executar com Docker Compose

Na raiz do projeto, após configurar as variáveis de ambiente
necessárias:

``` bash
docker compose up -d --build
```

Para acompanhar os serviços:

``` bash
docker compose ps
docker compose logs -f
```

Para encerrar:

``` bash
docker compose down
```

### Aplicar manifests no Kubernetes local

Depois de iniciar o Minikube e disponibilizar a imagem ao cluster:

``` bash
minikube start --driver=docker
minikube image load taskflow-api:1.0
kubectl apply -f k8s/
kubectl get pods
kubectl get services
```

*Os comandos pressupõem que os manifests Kubernetes e as imagens
correspondentes já estejam configurados.*

## Segurança e boas práticas

-   Não versionar arquivos `.env`, tokens, senhas ou chaves de API.
-   Utilizar variáveis de ambiente e Secrets para configurações
    sensíveis.
-   Validar e tratar as respostas produzidas pelo modelo de IA.
-   Aplicar autenticação e autorização nos endpoints protegidos.
-   Configurar limites de recursos e verificações de saúde nos workloads
    Kubernetes.
-   Utilizar imagens versionadas e evitar depender exclusivamente da tag
    `latest`.
-   Executar testes e verificações antes de publicar uma nova versão.

## Aprendizados esperados

Durante o desenvolvimento do TaskFlow AI, serão praticados:

-   Desenvolvimento e organização de APIs REST com ASP.NET Core.
-   Integração entre frontend, backend, banco de dados e serviços
    externos.
-   Consumo de APIs de IA e engenharia de prompts.
-   Containerização e otimização de imagens Docker.
-   Orquestração de aplicações com Kubernetes.
-   Automação de build, testes e publicação com CI/CD.
-   Configuração segura de ambientes e diagnóstico por logs.

## Status do projeto

**Em desenvolvimento --- projeto educacional e experimental.**

As funcionalidades, a infraestrutura e o pipeline serão construídos
progressivamente. Este README descreve os objetivos e a arquitetura
planejada; os recursos efetivamente disponíveis devem ser conferidos no
código-fonte e nos arquivos de configuração do repositório.

## Contribuição

Sugestões, melhorias e apontamentos são bem-vindos.

1.  Faça um fork do repositório.
2.  Crie uma branch para sua alteração.
3.  Faça commits claros e objetivos.
4.  Abra um Pull Request descrevendo as alterações.

## Licença

A licença ainda não foi definida. Consulte o responsável pelo
repositório antes de reutilizar ou distribuir este projeto.
