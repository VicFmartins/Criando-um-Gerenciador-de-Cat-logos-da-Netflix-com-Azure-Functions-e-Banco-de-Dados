# Criando-um-Gerenciador-de-Cat-logos-da-Netflix-com-Azure-Functions-e-Banco-de-Dados

## Descrição do Projeto

Este projeto implementa um gerenciador de catálogos da Netflix utilizando Azure Functions e banco de dados em nuvem (Cosmos DB). O sistema disponibiliza operações de cadastro, consulta, atualização, exclusão e filtragem de títulos (filmes e séries), além de armazenamento de arquivos (imagens de capa, documentos) associado ao catálogo.

## Objetivo

Desenvolver uma API serverless moderna, escalável e econômica para manipulação do catálogo da Netflix, integrando Cosmos DB para dados estruturados e Storage Account para gerenciamento dos arquivos dos títulos.

## Funcionalidades

- Cadastro de títulos no catálogo
- Consulta individual e listagem completa dos títulos
- Atualização e exclusão de títulos (CRUD)
- Filtro avançado de títulos por gênero, ano, classificação, etc.
- Armazenamento e recuperação de arquivos (ex: imagens de capa)
- Controle de usuários e interações (assistidos, favoritados, etc.) opcional

## Arquitetura

- Azure Functions (HTTP Trigger) para os endpoints REST
- Azure Cosmos DB (NoSQL) para armazenar os dados dos títulos, gêneros, avaliações e usuários
- Azure Storage Account para arquivos binários vinculados aos registros
- Application Insights para monitoramento (opcional)
- Ferramentas de desenvolvimento: Visual Studio ou VS Code

## Estrutura do Banco de Dados (Cosmos DB)

- Títulos: id, tipo (filme/série), título, gêneros, ano de lançamento, duração, classificação, descrição, URL da capa
- Usuários: id, username, email, plano de assinatura
- Interações: userId, titleId, tipo de interação (assistido, favoritado, etc.), timestamp
- Watchlist: userId, titleId, data de inclusão

## Estrutura do Projeto

```
NetflixCatalogManager/
│
├── Functions/
│   ├── CreateTitleFunction.cs
│   ├── GetTitleFunction.cs
│   ├── ListTitlesFunction.cs
│   ├── UpdateTitleFunction.cs
│   ├── DeleteTitleFunction.cs
│   ├── FilterTitlesFunction.cs
│   └── FileUploadFunction.cs
│
├── Models/
│   ├── Title.cs
│   ├── User.cs
│   ├── Interaction.cs
│   └── Watchlist.cs
│
├── Services/
│   ├── CosmosDbService.cs
│   └── StorageService.cs
│
├── Program.cs
├── host.json
├── local.settings.json
└── NetflixCatalogManager.csproj
```

## Passo a Passo de Implementação

1. Provisionar recursos na Azure: Resource Group, Cosmos DB, Storage Account, Function App (.NET)
2. Configurar strings de conexão no local.settings.json do projeto
3. Criar a solução no Visual Studio/VS Code e inicializar com Azure Functions (.NET 8)
4. Modelar os dados (Title, User, Interaction, Watchlist) seguindo a estrutura proposta
5. Implementar funções HTTP para cadastro, consulta, listagem, atualização, exclusão, filtro e upload/download de arquivos
6. Testar localmente com Azure Functions Core Tools
7. Fazer o deploy com Azure CLI ou Visual Studio
8. Validar endpoints via Swagger, Postman ou curl
9. Integrar Application Insights para logs e métricas
10. Configurar autenticação/autorização, CORS, rate limiting e boas práticas de segurança

## Exemplos de Endpoints REST

- POST /catalog/titles: cria um novo título
- GET /catalog/titles/{id}: detalha um título
- GET /catalog/titles: lista todos os títulos
- PUT /catalog/titles/{id}: atualiza detalhes de um título
- DELETE /catalog/titles/{id}: remove título
- GET /catalog/titles/filter?genre=Drama&year=2023: filtra títulos por parâmetros
- POST /catalog/titles/{id}/cover: faz upload da imagem de capa
- GET /catalog/titles/{id}/cover: recupera imagem de capa

## Boas Práticas de Arquitetura

- Separar funções por contexto de negócio
- Encapsular acesso a dados e Storage Account em services dedicados
- Centralizar configurações sensíveis em variáveis/secretos de ambiente
- Estruturar dados no Cosmos DB aproveitando flexibilidade do NoSQL
- Integrar logs e métricas via Application Insights
- Utilizar Storage Account para arquivos e URLs no registro do Cosmos DB

## Recursos Úteis

- SDK do Azure para .NET: CosmosDB
- Azure Storage para .NET
- Boas práticas para Azure Functions


Este projeto oferece uma base robusta para o gerenciamento de catálogo de conteúdos como Netflix, com alta escalabilidade, flexibilidade e custos otimizados. Permite fácil extensão para novas funcionalidades e serviços integrados, aproveitando o melhor da arquitetura serverless e dos recursos da Microsoft Azure.
