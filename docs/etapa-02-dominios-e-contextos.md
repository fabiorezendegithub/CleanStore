# Etapa 2 - Domínios e Contextos

Este documento descreve como configurar a estrutura inicial do projeto CleanStore seguindo os princípios de Clean Architecture.

## Criação da Solução PWA

1. Clique com o botão direito na solução
2. Selecione **Add** > **New Project**
3. Escolha **Blazor WebAssembly**
4. Nomeie como `CleanStore.Pwa`

## Estrutura de Pastas por Projeto

### CleanStore.Domain

```
📁 AccountContext/
  📁 Entities/
  📁 ValueObjects/
📁 SharedContext/
  📁 Entities/
  📁 ValueObjects/
```

### CleanStore.Application

```
📁 AccountContext/
📁 SharedContext/
```

### CleanStore.Infrastructure

```
📁 AccountContext/
📁 SharedContext/
```

### CleanStore.Pwa

```
📁 AccountContext/
  📁 UseCases/
    📁 Create/
    📄 CreatePage.razor
```

## Responsabilidades dos Contextos

### SharedContext
- **Entities**: Classes base de entidades utilizadas por todos os contextos
- **ValueObjects**: Classes base de value objects compartilhadas entre contextos

### AccountContext
- **Entities**: Entidades específicas do domínio de contas/usuários
- **ValueObjects**: Value objects específicos do contexto de contas

## Observações Importantes

> **Consistência de Estrutura**: O aspecto mais importante não é o nome específico das pastas, mas manter a mesma estrutura organizacional em todos os projetos da solução.

Esta padronização facilita:
- Navegação entre projetos
- Manutenção do código
- Onboarding de novos desenvolvedores
- Aplicação consistente dos princípios de Clean Architecture

Na [Etapa 3](etapa-03-entidade-e-objeto-valor.md), vamos atuar nas entidades e objetos de valor.

---

[← Voltar ao README](../README.md) | [← Voltar a etapa 1](etapa-01-estrutura-basica.md) | [Próxima Etapa →](etapa-03-entidade-e-objeto-valor.md)