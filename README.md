# ASP.NET Core WebAPI - REST

## 1. Conceitos Teóricos

### REST x SOAP

#### SOAP (Simple Object Access Protocol)

SOAP é um protocolo que formata os dados em um padrão XML para serem enviado.

#### REST (Representional State Transfer)

REST é uma arquitetura que envia texto por isso é mais leve e consequente mais interessante de ser usado.

**Arquitetura REST**

É uma abstração capaz de se comunicar em qualquer aplicação. O que permite a implementação em diferentes tecnologias é o fato de ser arquivos de texto.

***

### WebAPI

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

***Rotas***

As rota da classe é definida pelo atributo `Route`:

```C#
// [controller] = Parâmetro que se refere ao nome da classe em a palavra 'Controller'
// Exemplo: api/ExampleWebApi
[Route("api/[controller]")]
[ApiController]
public class ExampleWebApiController : ControllerBase
```
Entretanto quando se trata de métodos existem atributos especiais para definir a rota de acordo com o verbo Http.

```C#
// Com esses atributos torna-se redundante o uso do Route. Exemplos:
[HttpGet]
[HttpPost]
[HttpPut]
[HttpDelete]

// Atributo + Parâmetro:
[HttpGet("{id}")]

// Atributo + Parâmetro + Definição do tipo de dado:
[HttpGet("{id}:int")]
```

***ActionResult***

É o resultado de uma ação. 

Encapsula diversos tipos de retorno, por isso é usado como resultado de um método ao invés de um objeto puro.

```C#
// Exemplos 
ActionResult
ActionResult<string>
ActionResult<IEnumerable<int>>
```
*Atributos nos argumentos*

Os atributoa nos argumetnos ajudam a aplicação a identificar de onde virá o parâmetro esperado 

```C#
[FromBody] // Indica que o argumento vem do body.
[FromForm] // Indica que o argumento vem de um formulário.
[FromQuery] // Indica que o argumento vem de uma query.

// Implemetação
[HttpPut("{id}")]
public void Put(int id, [FromBody] string value)
{
}
```

*Formatadores de resposta*

São os atributos que definem o tipo de retorno que o método pode produzir.

```C#
// namespace
using Microsoft.AspNetCore.Http;

[ProducesResponseType(typeof(ClasssType), StatusCodeStatus201Created)] // Define o código e o tipo do objeto no retorno
[ProducesResponseType(StatusCodes.Status400BadReques] // Define apenas o código do retorno.
public void Post([FromBody] string value)
{
}
```

*Formatador de reposta personalizado*

É possível personalizar as repostas que serão enviadas:

```C#
// Implementação

```

***Analisadores e Convenções***

Anlisadores

Pacote: Microsoft.AspNetCore.Mvc.Api.Analyzers

Tem por objetivo analizar os formatadores de repostas, e avisar caso o código retornado não corresponder ao que foi especificado.

Convenções

As convenções tem a mesma função dos formatadores, define quais tipos de retorno um método deve ter, entretanto não é programável, as regras são de acordo com a documentação do protocolo HTTP, cada verbo tem tipos de retornos específicos.

```C#
//Exemplos

// Declaração para a classe
[ApiConventionType(typeof(DefaultApiConventions))]

// Declaração para método Post
[ApiConventionMethod(typeof(DefaultApiConventions), nameof(DefaultApiConventions.Post))]

// Convenções para Put
[ApiConventionMethod(typeof(DefaultApiConventions), nameof(DefaultApiConventions.Put))]

```

***
