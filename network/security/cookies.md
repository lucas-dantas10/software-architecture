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

## What cookies are used for

Normally, the server uses the contents of HTTP cookies to determine whether 
different requests come from the same browser/user and then sends a 
personalized or generic response, as appropriate. Below is a basic user login system:

- The user sends login credentials to the server, for example, through a form submission.

- If the credentials are correct, the server updates the interface to indicate that the user is logged in and responds with a cookie containing a session ID that records the login status in the browser.

- At a later time, the user navigates to a different page on the same website. The browser sends the cookie containing the session ID along with the corresponding request to indicate that it believes the user is still logged in.

- The server checks the session ID and, if it is still valid, sends the user a personalized version of the new page. If it is not valid, the session ID is removed and the user receives a generic version of the page (or possibly an “access denied” message and is asked to log in again).

## Main uses of cookies

- Session management: User login status, shopping cart contents, game scores, or any other session-related details that the server needs to remember.

- Personalization: User preferences, such as display language and interface theme.

- Tracking: Recording and analyzing user behavior.

## Data storage

In the early days of the web, cookies were often used (there were no other options) 
for client-side data storage. Nowadays, modern storage APIs are recommended, 
such as the Web Storage API. IndexedDB, LocalStorage, and SessionStorage are 
designed specifically for client-side storage without needing to send data to the 
server and do not have the drawbacks of cookies, such as:

- Browsers are usually limited to a maximum number of cookies per domain (which varies by browser, generally in the hundreds) and a maximum size per cookie (usually 4 KB). Storage APIs can store much larger volumes of data.

- Cookies are sent with every request, which can negatively impact performance (for example, on slow mobile connections), especially if you have many cookies set.

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
