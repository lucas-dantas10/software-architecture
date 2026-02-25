# Cookies

### [Study link](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Cookies)

## What is Cookie? (Technical Text)

A cookie (also known as a web cookie or browser cookie) is a small piece of data a server 
sends to a user's web browser. The browser may store cookies, 
create new cookies, modify existing ones, 
and send them back to the same server with later requests. 
Cookies enable web applications to store limited amounts of data and remember 
state information; by default the HTTP protocol is stateless.


##  What is Cookie? (My Version)

Imagine you buy a cookie biscuit from a store.
The store gives you the cookie and puts it inside a box with your name on it.
When you come back later, you just show who you are and the store finds 
the cookie saved for you. If someone else tries to take it, they can’t, 
because the box only opens with your identification.

In HTTP, a cookie works the same way: the website stores a small piece of information 
in your browser to recognize you later, keeping your session or preferences, 
and preventing others from using it.

## Para que os cookies são usados

Normalmente, o servidor usa o conteúdo dos cookies HTTP para determinar se diferentes requisições vêm do mesmo navegador/usuário e então emite uma resposta personalizada ou genérica, conforme apropriado. A seguir descreve um sistema básico de login do usuário:

- O usuário envia credenciais de login para o servidor, por exemplo, por meio de um envio de formulário.
- Se as credenciais estiverem corretas, o servidor atualiza a interface para indicar que o usuário está logado, e responde com um cookie contendo um ID de sessão que registra o status de login no navegador.
- Em um momento posterior, o usuário se move para uma página diferente no mesmo site. O navegador envia o cookie contendo o ID da sessão junto com a solicitação correspondente para indicar que acredita que o usuário ainda está logado.
- O servidor verifica o ID da sessão e, se ainda estiver válido, envia ao usuário uma versão personalizada da nova página. Se não for válido, o ID da sessão é excluído e o usuário recebe uma versão genérica da página (ou talvez uma mensagem de "acesso negado" e solicitado a fazer login novamente).

## Principais usos dos cookies

- Gerenciamento de sessões: Status de login do usuário, conteúdo do carrinho de compras, pontuações dos jogos ou quaisquer outros detalhes relacionados à sessão do usuário que o servidor precise lembrar.
- Personalização: Preferências do usuário, como linguagem de exibição e tema da interface.
- Rastreamento: Registro e análise do comportamento do usuário.

## Armazenamento de dados

Nos primeiros dias da web, os cookies eram usados frequentemente(não havia outras opções) 
para armazenamento de dados do lado do cliente. Hoje em dia são recomendadas as API's modernas
de armazenamento, como por exemplo, a Web Storage API. o IndexedDB, LocalStorage e SessionStorage.
Eles são projetados justamente para o armazenamento do lado do cliente sem precisar enviar dados
para o servidor e não trazem as desvantagens que possui no cookie, que são:

- Os navegadores geralmente são limitados a um número máximo de cookies por domínio (varia conforme o navegador, geralmente em centenas), e um tamanho máximo por cookie (geralmente 4KB). APIs de armazenamento podem armazenar volumes maiores de dados.
- Cookies são enviados a cada solicitação, então podem piorar o desempenho (por exemplo, em conexões móveis lentas), especialmente se você tiver muitos cookies configurados.

## Creating, removing, and updating cookies

After receiving an HTTP request, a server can send one or more Set-Cookie headers 
with the response, each one of which will set a separate cookie. 
A cookie is set by specifying a name-value pair like this:

```http
Set-Cookie: <cookie-name>=<cookie-value>
```

The following HTTP response instructs the receiving browser to store a pair of cookies:

```http
HTTP/2.0 200 OK
Content-Type: text/html
Set-Cookie: yummy_cookie=chocolate
Set-Cookie: tasty_cookie=strawberry

[page content]
```

Example setting Cookie in `Java`:

```java
Cookie cookie = new Cookie("sessionToken", "abc123xyz");
cookie.setMaxAge(60 * 60 * 24);  // 1 day
cookie.setHttpOnly(true);
cookie.setSecure(true);
cookie.setPath("/");
response.addCookie(cookie);
```

## Removal: defining the lifetime of a cookie

You can specify an expiration date or time period after which the cookie should be 
deleted and no longer sent. Depending on the attributes set within the Set-Cookie 
header when the cookies are created, they can be either permanent or session cookies:

- Permanent cookies are deleted after the date specified in the Expires attribute:
```http
Set-Cookie: id=a3fWa; Expires=Thu, 31 Oct 2021 07:28:00 GMT;
```

or after the period specified in the Max-Age attribute:

```http
Set-Cookie: id=a3fWa; Max-Age=2592000
```

- Session cookies — cookies without a Max-Age or Expires attribute – are deleted 
when the current session ends. The browser defines when the "current session" ends, 
and some browsers use session restoring when restarting. This can cause session 
cookies to last indefinitely.
  - Note: If your site authenticates users, it should regenerate and resend 
  session cookies, even ones that already exist, whenever a user authenticates. 
  This approach helps prevent [session fixation](https://owasp.org/www-community/attacks/Session_fixation) attacks, 
  where a third-party can reuse a user's session.

To immediately remove a cookie, set the cookie again with the same name, path, 
and domain (if specified), and set its Expires attribute to a date in the past 
or its Max-Age attribute to 0 or negative. This instructs the browser to delete 
the cookie right away. For example:

```http
Set-Cookie: id=a3fWa; Max-Age=0
```

You can also clear all cookies associated with a registrable domain using the 
Clear-Site-Data response header. For example, the following header 
sent from https://foo.example.com/ would clear all cookies sent by 
example.com and all of its subdomains, such as all.bar.example.com.

```http
Clear-Site-Data: "cookies"
```

## Updating cookie values

In the browser, you can create new cookies via JavaScript using the Document.cookie 
property, or the asynchronous Cookie Store API. Note that all examples 
below use Document.cookie, as it is the most widely supported/established option.

```javascript
document.cookie = "yummy_cookie=chocolate";
document.cookie = "tasty_cookie=strawberry";
```

You can also access existing cookies and set new values for them:

```javascript
console.log(document.cookie);
// logs "yummy_cookie=chocolate; tasty_cookie=strawberry"

document.cookie = "yummy_cookie=blueberry";

console.log(document.cookie);
// logs "tasty_cookie=strawberry; yummy_cookie=blueberry"
```

For security purposes, you can't change cookie values by sending an updated Cookie 
header directly when initiating a request, for example, via fetch() or XMLHttpRequest.

There are good reasons why you shouldn't allow JavaScript to modify cookies at all. 
You can prevent JavaScript from accessing a cookie by specifying the HttpOnly 
attribute during its creation.
