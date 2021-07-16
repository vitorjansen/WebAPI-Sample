# ASP.NET Core WebAPI - REST


## REST x SOAP

### SOAP (Simple Object Access Protocol)

SOAP é um protocolo que formata os dados em um padrão XML para serem enviado.

### REST (Representional State Transfer)

REST é uma arquitetura que envia texto por isso é mais leve e consequente mais interessante de ser usado.

**Arquitetura REST**

É uma abstração capaz de se comunicar em qualquer aplicação. O que permite a implementação em diferentes tecnologias é o fato de ser arquivos de texto.

***

## WebAPI

#### Convenções

    - Os nomes dos métodos são os verbos HTTP (GET, POST, PUT, DELETE etc.)


#### Controller

É a estrutura da aplicação, todos os `requests` e `reponses` são manipulados pela `Controller`.

***ControllerBase***

A classe `ControllerBase` é a base para todas as `Controllers` independente da arquitetura.

> Info: A classe `Controller` no MVC é uma especialização da `ControllerBase` com o adicional de ter suporte às Views. Em uma WebAPI as Views não são necessárias, por isso herda-se da classe mais genérica possível.

Atributos complementares

Para complementar os métodos necessários no suporte a uma WebAPI às controllers possuem um atributo exclusiso chamado: `[ApiController]`.

```C#
// Exemplo
[ApiController]
public class ExampleWebApiController : ControllerBase
```
