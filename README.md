# TaskFlow AI

```{=html}
<p align="center">
```
`<strong>`{=html}Uma aplicação Full Stack para gerenciamento inteligente
de tarefas`</strong>`{=html}`<br>`{=html} `<em>`{=html}Projeto de
estudos práticos em desenvolvimento de software, Inteligência Artificial
e DevOps`</em>`{=html}
```{=html}
</p>
```

------------------------------------------------------------------------

## Sobre o projeto

O **TaskFlow AI** é um projeto de aprendizado e demonstração técnica que
propõe uma plataforma para gerenciamento de tarefas com recursos de
Inteligência Artificial.

A aplicação permitirá cadastrar, organizar e acompanhar tarefas,
utilizando um serviço baseado em LLM (*Large Language Model*) para
interpretar descrições em linguagem natural, sugerir categorias, indicar
prioridades e produzir resumos.

Além das funcionalidades de negócio, o projeto tem como objetivo
demonstrar um fluxo moderno de desenvolvimento e entrega de software:
desenvolvimento de uma API, integração com banco de dados,
containerização com Docker, orquestração com Kubernetes e automação de
integração e entrega contínuas (CI/CD).

> **Propósito:** unir desenvolvimento Full Stack, integração de IA e
> práticas de DevOps em uma aplicação prática, evolutiva e documentada.

## Objetivos

-   Desenvolver uma API REST utilizando C# e ASP.NET Core.
-   Construir uma interface web com HTML, CSS e JavaScript puro
    (*Vanilla JavaScript*).
-   Persistir os dados em SQL Server.
-   Integrar um modelo de linguagem para apoiar a organização das
    tarefas.
-   Executar os componentes em containers Docker.
-   Orquestrar a aplicação com Kubernetes.
-   Automatizar compilação, testes e publicação por meio do GitHub
    Actions.
-   Aplicar boas práticas de configuração, segurança, observabilidade e
    documentação.

## Funcionalidades planejadas

  -----------------------------------------------------------------------
  Funcionalidade                      Descrição
  ----------------------------------- -----------------------------------
  Gerenciamento de tarefas            Criar, consultar, atualizar e
                                      excluir tarefas.

  Classificação com IA                Interpretar descrições e sugerir
                                      categorias.

  Priorização assistida               Recomendar níveis de prioridade com
                                      base no contexto informado.

  Resumos                             Gerar resumos de tarefas ou
                                      conjuntos de atividades.

  API REST                            Disponibilizar operações para
                                      integração com o frontend.

  Autenticação                        Proteger endpoints com autenticação
                                      baseada em JWT.
  -----------------------------------------------------------------------

*As funcionalidades serão implementadas gradualmente durante a evolução
do projeto.*

## Tecnologias e ferramentas

### Backend

-   **C#** --- linguagem principal da API.
-   **ASP.NET Core Web API (.NET 10)** --- construção dos endpoints
    REST.
-   **Entity Framework Core** --- acesso e persistência de dados.
-   **JWT (JSON Web Token)** --- autenticação e autorização.

### Frontend

-   **HTML5** --- estrutura das páginas.
-   **CSS3** --- estilos e layout responsivo.
-   **JavaScript (Vanilla)** --- interação com a API e comportamento da
    interface.

### Banco de dados

-   **Microsoft SQL Server** --- armazenamento das tarefas e demais
    dados da aplicação.

### Inteligência Artificial

-   **LLMs (Large Language Models)** --- interpretação de texto e
    geração de sugestões.
-   **API de provedor de IA** --- comunicação entre o backend e o modelo
    de linguagem.
-   **Saídas estruturadas em JSON** --- integração controlada entre as
    respostas da IA e as regras da aplicação.

A integração será feita pelo backend. Chaves de API e demais credenciais
não devem ser expostas no frontend, no repositório ou nas imagens
Docker.

### Containers e orquestração

-   **Docker** --- criação e execução de imagens e containers.
-   **Docker Compose** --- execução local dos serviços integrados.
-   **Kubernetes** --- gerenciamento de Pods, Deployments, Services e
    configurações.
-   **Minikube** --- ambiente Kubernetes local para desenvolvimento e
    experimentação.
-   **kubectl** --- interface de linha de comando para administrar o
    cluster.

### CI/CD e versionamento

-   **Git** --- controle de versão.
-   **GitHub** --- hospedagem do código-fonte.
-   **GitHub Actions** --- automação de build, testes e publicação de
    imagens.
-   **GitHub Container Registry (GHCR)** --- armazenamento das imagens
    Docker.

## Arquitetura proposta

``` text
                    ┌─────────────────────────┐
                    │      Frontend Web       │
                    │ HTML + CSS + JavaScript │
                    └────────────┬────────────┘
                                 │ HTTP / REST
                                 ▼
                    ┌─────────────────────────┐
                    │   ASP.NET Core Web API  │
                    │       C# / JWT          │
                    └────────┬─────────┬──────┘
                             │         │
                    ┌────────▼───┐  ┌──▼────────────────┐
                    │ SQL Server │  │ Serviço de IA     │
                    │            │  │ API de um LLM     │
                    └────────────┘  └───────────────────┘

             Empacotamento e execução: Docker / Compose
             Orquestração: Kubernetes / Minikube
             Automação: GitHub Actions → GHCR → Kubernetes
```

O frontend acessa a API por HTTP. A API concentra as regras de negócio,
valida os dados, persiste as informações no SQL Server e, quando
necessário, consulta o serviço de IA. Docker padroniza a execução dos
componentes; Kubernetes será utilizado para praticar implantação e
gerenciamento; e o pipeline CI/CD automatiza as etapas de validação e
publicação.

## Fluxo de CI/CD

O fluxo de automação planejado é:

1.  O desenvolvedor envia alterações para o repositório GitHub.
2.  O GitHub Actions obtém o código-fonte.
3.  O pipeline restaura dependências e compila a solução.
4.  Os testes automatizados são executados.
5.  Uma imagem Docker é construída.
6.  A imagem é publicada no GitHub Container Registry.
7.  Uma etapa de implantação atualiza a aplicação no ambiente
    Kubernetes.

A publicação e a implantação serão configuradas em etapas. O deploy em
cluster remoto exige credenciais e permissões específicas, armazenadas
de forma segura nos recursos de configuração do GitHub Actions.

## Estrutura de diretórios prevista

``` text
TaskFlowAI/
├── TaskFlow.Api/
│   ├── Controllers/
│   ├── Services/
│   ├── Models/
│   ├── Data/
│   └── Dockerfile
│
├── TaskFlow.Tests/
│
├── frontend/
│   ├── index.html
│   ├── css/
│   └── js/
│
├── k8s/
│   ├── deployment.yaml
│   ├── service.yaml
│   ├── configmap.yaml
│   └── secret.yaml
│
├── .github/
│   └── workflows/
│       └── pipeline.yml
│
├── compose.yaml
├── .gitignore
└── README.md
```

A estrutura poderá ser ajustada conforme a implementação evoluir.

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

### Executar os serviços com Docker Compose

Na raiz do projeto, após configurar as variáveis de ambiente exigidas:

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

Depois de iniciar o Minikube, construir a imagem e disponibilizá-la ao
cluster:

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
-   Validar e tratar as respostas produzidas pelo modelo de IA antes de
    utilizá-las.
-   Aplicar autenticação e autorização nos endpoints protegidos.
-   Configurar limites de recursos e verificações de saúde nos workloads
    Kubernetes.
-   Utilizar imagens versionadas e evitar depender exclusivamente da tag
    `latest`.
-   Executar testes e verificações antes de publicar uma nova versão.

## Aprendizados esperados

Ao desenvolver o TaskFlow AI, a proposta é praticar:

-   Desenvolvimento e organização de APIs REST com ASP.NET Core.
-   Integração entre frontend, backend, banco de dados e serviços
    externos.
-   Consumo de APIs de IA e engenharia de prompts.
-   Containerização e otimização de imagens Docker.
-   Orquestração de aplicações com Kubernetes.
-   Automação de build, testes e publicação com CI/CD.
-   Configuração segura de ambientes e diagnóstico de problemas por
    logs.

## Status do projeto

**Em desenvolvimento --- projeto educacional e experimental.**

As funcionalidades, a infraestrutura e o pipeline serão construídos
progressivamente. Este README descreve a arquitetura e os objetivos
previstos; os recursos efetivamente disponíveis devem ser conferidos no
código-fonte e nos arquivos de configuração do repositório.

## Contribuição

Sugestões, melhorias e apontamentos são bem-vindos. Para contribuir:

1.  Faça um fork do repositório.
2.  Crie uma branch para sua alteração.
3.  Faça commits claros e objetivos.
4.  Abra um Pull Request descrevendo o que foi alterado.

## Licença

A licença ainda não foi definida. Antes de reutilizar ou distribuir este
projeto, consulte o responsável pelo repositório.
