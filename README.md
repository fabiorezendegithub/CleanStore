# CleanStore - Arquitetura Limpa na Prática

[![.NET](https://img.shields.io/badge/.NET-9.0-blue.svg)](https://dotnet.microsoft.com/)
[![C#](https://img.shields.io/badge/C%23-12.0-green.svg)](https://docs.microsoft.com/en-us/dotnet/csharp/)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

## 📋 Sobre o Projeto

O **CleanStore** é um projeto de demonstração prática de **Arquitetura Limpa (Clean Architecture)** utilizando **.NET 9**. O objetivo é criar uma aplicação robusta, testável e maintível seguindo os princípios da Clean Architecture propostos por Robert C. Martin (Uncle Bob).

## 🏗️ Arquitetura

Este projeto implementa a Clean Architecture com as seguintes camadas:

```
CleanStore/
├── src/
│   ├── CleanStore.Domain/          # Camada de Domínio
│   ├── CleanStore.Application/     # Camada de Aplicação
│   ├── CleanStore.Infrastructure/  # Camada de Infraestrutura
│   └── CleanStore.Api/            # Camada de Apresentação (API)
├── tests/
│   ├── CleanStore.Domain.Tests/
│   ├── CleanStore.Application.Tests/
│   └── CleanStore.Api.Tests/
└── docs/                          # Documentação das etapas
```

### 🎯 Princípios da Arquitetura Limpa

- **Independência de Frameworks**: A arquitetura não depende de bibliotecas externas
- **Testabilidade**: Regras de negócio podem ser testadas sem UI, BD, servidor web, etc.
- **Independência de UI**: A UI pode mudar facilmente sem alterar o resto do sistema
- **Independência de Banco de Dados**: Oracle, SQL Server, MongoDB, etc. são detalhes
- **Independência de Agentes Externos**: As regras de negócio não sabem nada sobre o mundo exterior

## 🚀 Tecnologias Utilizadas

- **.NET 9** - Framework principal
- **C# 12** - Linguagem de programação
- **Entity Framework Core** - ORM para acesso a dados
- **MediatR** - Padrão Mediator para CQRS
- **FluentValidation** - Validação de dados
- **xUnit** - Framework de testes
- **Swagger/OpenAPI** - Documentação da API

## 📚 Documentação das Etapas

O desenvolvimento deste projeto está dividido em etapas documentadas:

- **[Etapa 1](docs/etapa-01-estrutura-basica.md)** - Criação da Estrutura Básica do Projeto
- **[Etapa 2](docs/etapa-02-dominios-e-contextos.md)** - Implementação estrutura de pastas de dominio e contexto

## ⚡ Início Rápido

### Pré-requisitos

- [.NET 9 SDK](https://dotnet.microsoft.com/download/dotnet/9.0)
- [Git](https://git-scm.com/)
- [Visual Studio 2022](https://visualstudio.microsoft.com/) ou [VS Code](https://code.visualstudio.com/)

### Instalação

1. **Clone o repositório**
   ```bash
   git clone https://github.com/seu-usuario/cleanstore.git
   cd cleanstore
   ```

2. **Restaure as dependências**
   ```bash
   dotnet restore
   ```

3. **Execute o build**
   ```bash
   dotnet build
   ```

4. **Execute a aplicação**
   ```bash
   cd src/CleanStore.Api
   dotnet run
   ```

5. **Acesse a documentação da API**
   ```
   https://localhost:5001/swagger
   ```

## 🧪 Executando os Testes

Execute todos os testes do projeto:

```bash
dotnet test
```

Execute testes com relatório de cobertura:

```bash
dotnet test --collect:"XPlat Code Coverage"
```

## 🙏 Agradecimentos

- [Andre Baltieri](https://github.com/balta-io/2506) - Pelos conceitos de Clean Architecture
