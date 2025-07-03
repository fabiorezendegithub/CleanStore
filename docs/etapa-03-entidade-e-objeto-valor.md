# Etapa 3 - Entidade e objeto valor

Este documento descreve a criação das classes entidade e objeto valor no SharedContext.

## Criação da Entidade

A entidade será criada para ser chamada pelas outras entidades, ela inicialmente irá tratar apenas do id, que será um guid.
Segue codigo

```csharp
    public bool Equals(Entity? other)
    {
        if(other is null) return false;
        return ReferenceEquals(this, other) || Id.Equals(other.Id);
    }
    
    public bool Equals(Guid other) => Id == other;

    public override bool Equals(object? obj)
    {
        if(obj is null) return false;
        if(ReferenceEquals(this, obj)) return true;
        return obj.GetType() == GetType() && Equals((Entity)obj);
    }
    
    public override int GetHashCode() => Id.GetHashCode();
    
    public static bool operator ==(Entity? left, Entity? right) => Equals(left, right);
    
    public static bool operator !=(Entity? left, Entity? right) => !Equals(left, right);
```
## Criação do ValueObject

O valueObject por hora sera uma classe bem basica, iremos retornar a ele posteriormente

```csharp
    public abstract record ValueObject;
```

Na Etapa 4, vamos atuar nos domain Events

---

[← Voltar ao README](../README.md) | [← Voltar a etapa 2](etapa-02-dominios-e-contextos.md) | [Próxima Etapa →](etapa-04-domain-events.md)