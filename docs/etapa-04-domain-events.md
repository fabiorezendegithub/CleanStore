# Etapa 4 - Domain Events

Este documento descreve a implementação de domain events para disparar eventos de domínio de forma desacoplada, seguindo os princípios do Domain-Driven Design (DDD).

## Visão Geral

Os Domain Events são uma ferramenta poderosa para implementar comunicação assíncrona entre diferentes partes do sistema, permitindo que mudanças em uma entidade disparem ações em outros contextos sem criar acoplamento direto.

## Configurando o MediatR.Contracts

O MediatR.Contracts fornece as abstrações necessárias para implementar o padrão Mediator sem depender da implementação completa do MediatR.

### Instalação

1. Abra o Package Manager Console ou use a interface do NuGet
2. Instale o pacote no projeto **Domain**:
   ```bash
   Install-Package MediatR.Contracts
   ```

> **Nota**: Utilizamos apenas os contracts para manter o domínio livre de dependências de infraestrutura. A implementação completa do MediatR será adicionada nas camadas superiores.

## Implementando Domain Events

### 1. Criando a Interface Base

Crie a interface `IDomainEvent` em `SharedContext/Events/Abstractions/`:

```csharp
using MediatR;

namespace SharedContext.Events.Abstractions;

/// <summary>
/// Representa um evento de domínio que pode ser disparado por entidades
/// </summary>
public interface IDomainEvent : INotification;
```

### 2. Aprimorando a Entidade Base

Atualize a classe `Entity` em `SharedContext/Entities/` para suportar domain events:

```csharp
using SharedContext.Events.Abstractions;

namespace SharedContext.Entities;

public abstract class Entity
{
    private readonly List<IDomainEvent> _domainEvents = new();
    
    /// <summary>
    /// Identificador único da entidade
    /// </summary>
    public Guid Id { get; init; } = Guid.NewGuid();
    
    /// <summary>
    /// Obtém a lista de eventos de domínio pendentes
    /// </summary>
    /// <returns>Lista somente leitura dos eventos</returns>
    public IReadOnlyList<IDomainEvent> GetDomainEvents() => _domainEvents.AsReadOnly();
    
    /// <summary>
    /// Limpa todos os eventos de domínio pendentes
    /// </summary>
    public void ClearDomainEvents() => _domainEvents.Clear();
    
    /// <summary>
    /// Adiciona um evento de domínio à lista de eventos pendentes
    /// </summary>
    /// <param name="domainEvent">Evento a ser adicionado</param>
    public void RaiseDomainEvent(IDomainEvent @event) => _domainEvents.Add(@event);
}
```

## Benefícios dos Domain Events

- **Desacoplamento**: Reduz dependências entre diferentes partes do sistema
- **Flexibilidade**: Permite adicionar novos comportamentos sem modificar código existente
- **Testabilidade**: Facilita o teste de efeitos colaterais das operações de domínio
- **Auditoria**: Possibilita rastreamento de mudanças importantes no sistema

## Próximos Passos

Na próxima etapa, implementaremos o tratamento de erros e exceções personalizadas para tornar o sistema mais robusto e facilitar o debugging.

---

[← Voltar ao README](../README.md) | [← Voltar à etapa 3](etapa-03-entidade-e-objeto-valor.md) | [Próxima Etapa →](etapa-05.md)