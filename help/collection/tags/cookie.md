---
title: cookie
description: Escriba, edite o elimine manualmente las cookies de la propiedad de etiquetas.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 7%

---

# `cookie`

El objeto `_satellite.cookie` contiene métodos que permiten escribir, editar o eliminar cookies a las que las reglas de etiquetas pueden hacer referencia. Es una copia parcial de [`js-cookie`](https://github.com/js-cookie/js-cookie), que contiene muchas características principales de esa biblioteca.

## `cookie.set()`

El método `set()` escribe una cookie a la que la propiedad de etiqueta puede hacer referencia.

```ts
_satellite.cookie.set(name: string, value: string, attributes?: {
  expires?: number | Date;
  path?: string;
  domain?: string;
  secure?: boolean;
  sameSite?: 'Strict' | 'Lax' | 'None';
}): string
```

Los siguientes parámetros de método están disponibles:

| Nombre | Tipo | Requerido | Descripción |
|---|---|---|---|
| **`name`** | `string` | Sí | Nombre de la cookie. |
| **`value`** | `string` | Sí | El valor de la cookie |
| **`attributes`** | `object` | No | Atributos adicionales que desea que tenga la cookie. |

El objeto `attributes` admite las siguientes propiedades:

| Nombre de atributo | Tipo | Requerido | Predeterminado | Descripción |
|---|---|---|---|---|
| **`expires`** | `number` o [`Date`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) | No | La cookie caduca al final de la sesión del explorador | El número de días durante los cuales desea que caduque la cookie. |
| **`path`** | `string` | No | Cookie visible en todo el sitio | Lugar del dominio donde la cookie es visible. |
| **`domain`** | `string` | No | Cookie visible para el dominio en el que se creó | Dominio válido (con o sin subdominio) donde la cookie es visible. Si se incluye un dominio sin un subdominio, la cookie es visible para todos los subdominios de ese dominio. |
| **`secure`** | `boolean` | No | No hay ningún atributo establecido | Determina si la cookie requiere un protocolo seguro (`https://`). Si se omite, no hay ningún requisito de protocolo seguro. |
| **`sameSite`** | `'Strict' \| 'Lax' \| 'None'` | No | No hay ningún atributo establecido | Le permite establecer el atributo [`sameSite`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Set-Cookie#samesitesamesite-value) de una cookie. Si establece `sameSite` en `None`, también debe establecer `secure` en `true`. |

```js
// Sets a cookie valid across the entire site, expires on session close
_satellite.cookie.set('simple_session_cookie', 'value');

// Sets a cookie that expires 7 days from now, valid across the entire site
_satellite.cookie.set('seven_day_cookie', 'value', { expires: 7 });

// Sets a cookie that expires 14 days from now, valid only on the current page
_satellite.cookie.set('page_specific_cookie', 'value', { expires: 14, path: '/' });

// Cross-site compatible cookie (requires HTTPS)
_satellite.cookie.set('cross_site_cookie', 'value', { secure: true, sameSite: 'None' });
```

Al invocar este método, se escribe la cookie deseada y se devuelve la cadena de cookie serializada que se escribió. Esta cadena se utiliza principalmente con fines de depuración o registro.

```text
'written_cookie=value; path=/'
```

>[!TIP]
>
>Las versiones anteriores del objeto de etiqueta usaban `_satellite.setCookie()`. El método `setCookie()` está obsoleto en favor de `_satellite.cookie.set()`.

## `cookie.get()`

El método `get()` devuelve un valor de cookie.

```ts
_satellite.cookie.get(name: string): string | undefined;
```

| Nombre | Tipo | Requerido | Descripción |
|---|---|---|---|
| **`name`** | `string` | Sí | El nombre de la cookie desde la que desea recuperar el valor (distingue entre mayúsculas y minúsculas). |

Si el nombre de la cookie existe, devuelve el valor de la cookie. Si el nombre de la cookie no existe, devuelve `undefined`.

>[!TIP]
>
>Las versiones anteriores del objeto de etiqueta usaban `_satellite.getCookie()`. El método `getCookie()` está obsoleto en favor de `_satellite.cookie.get()`.

## `cookie.remove()`

El método `remove()` elimina una cookie que usted haya establecido.

```ts
_satellite.cookie.remove(name: string, attributes?: {
  path?: string;
  domain?: string;
}): void
```

| Nombre | Tipo | Requerido | Descripción |
|---|---|---|---|
| **`name`** | `string` | Sí | El nombre de la cookie que desea eliminar. |
| **`attributes`** | `object` | No | Los atributos asociados con la cookie que desea eliminar. Si establece una cookie mediante los atributos `path` o `domain`, incluya esos mismos atributos al eliminar la cookie. Si no se incluyen estos atributos, no se elimina la cookie. |

```js
// Creates a session cookie
_satellite.cookie.set('session_cookie', 'Cookie value');

// Removes the above cookie
_satellite.cookie.remove('session_cookie');

// Creates a cookie that is only visible on the current page
_satellite.cookie.set('page_specific_cookie', 'value', { path: '/' });

// This remove method does nothing because it does not match the path and domain attributes of the cookie set
_satellite.cookie.remove('page_specific_cookie');

// This remove method works correctly for the page-specific cookie
_satellite.cookie.remove('page_specific_cookie', { path: '/' });
```

>[!TIP]
>
>Las versiones anteriores del objeto de etiqueta usaban `_satellite.removeCookie()`. El método `removeCookie()` está obsoleto en favor de `_satellite.cookie.remove()`.
