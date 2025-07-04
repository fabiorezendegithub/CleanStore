# Etapa 5 - Lidando com erros

Este documento descreve a implementação dos erros e finalizamos a classe value objects

## Visão Geral

Os erros podem ser tratados de diversas maneiras. Nessa etapa trataremos as throw exceptions de uma maneira diferente da tradicional.

## Criando o Erro Messages

Demos um inflada nessa etapa pois já deixamos preparado para receber por exemplo uma internacionalização se necessário.

Criar Exceptions > ErrorMessages

```csharp
public class ErrorMessages
{
    #region Properties

    public static EmailErrorMessages Email { get; } = new();

    #endregion

    public class EmailErrorMessages
    {
        public string Invalid { get; } = "E-mail inválido";
        
        public string NullOrEmpty { get; } = "E-mail não pode ser nulo ou vazio.";
    }
}
```

### Adicionando um Extensions para a string

Extension methods são uma ótima ferramenta no csharp, iremos criar uma para a string, podendo assim ser usado em qualquer parte do domain

Criar em SharedContext > Extensions > StringExtension

```csharp
public static class StringExtension
{
    public static string ToBase64(this string text)
        => Convert.ToBase64String(Encoding.ASCII.GetBytes(text));
    
}
```

## Finalizando ValueObjects

Agora podemos finalizar o valueobjects removendo todos os erros faltantes.

Atualizar AccountContext > ValueObjects > Email
```csharp
public partial record Email : ValueObject
{
    #region Constants
    
    public const int MinLength = 6;
    public const int MaxLength = 160;
    public const string Pattern = @"^\w+([-+.']\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$";

    #endregion
    
    #region Constructors
    
    private Email()
    {
    }

    private Email(string address, string hash)
    {
        Address = address;
        Hash = hash;
    }
    
    #endregion
    
    #region Factories
    
    public static Email Create(string address)
    {
        if (string.IsNullOrEmpty(address) || string.IsNullOrWhiteSpace(address))
            throw new EmailNullOrEmptyException(ErrorMessages.Email.NullOrEmpty);
        
        address = address.Trim();
        address = address.ToLower();
        
        if (!EmailRegex().IsMatch(address))
            throw new InvalidEmailException(ErrorMessages.Email.Invalid);

        return new Email(address, address.ToBase64());
    }

    #endregion
    
    #region Properties
    
    public string Address { get; private set; } = string.Empty;
    public string Hash { get; private set; } = string.Empty;
    
    #endregion
    
    #region Operators
    
    public static implicit operator string(Email email) 
        => email.ToString();
    
    #endregion
    
    #region Overrides
    
    public override string ToString() 
        => Address;
    
    #endregion
    
    #region Others
    
    [GeneratedRegex(Pattern)]
    private static partial Regex EmailRegex();
    
    #endregion
}
```

## Próximos Passos

Na próxima etapa, iremos atuar na nossa entidade.

---

[← Voltar ao README](../README.md) | [← Voltar à etapa 4](etapa-04-domain-events.md) | [Próxima Etapa →](etapa-06.md)