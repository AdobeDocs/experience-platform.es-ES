---
title: Cifrado de valores
description: Aprenda a cifrar valores confidenciales al utilizar la API de Reactor.
exl-id: d89e7f43-3bdb-40a5-a302-bad6fd1f4596
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 100%

---

# Cifrado de valores

Al utilizar etiquetas en Adobe Experience Platform, algunos flujos de trabajo requieren la provisión de valores confidenciales (por ejemplo, la provisión de una clave privada al enviar bibliotecas a entornos mediante hosts). El carácter delicado de esas credenciales requiere
transferencia y almacenamiento seguros.

Este documento describe cómo cifrar valores confidenciales utilizando [GnuPG encryption](https://www.gnupg.org/gph/en/manual/x110.html) (también conocido como GPG) para que solo el sistema de etiquetas pueda leerlos.

## Obtención de la clave GPG pública y suma de comprobación

Después de [descargar](https://gnupg.org/download/) e instalar la última versión de GPG, debe obtener la clave GPG pública para el entorno de producción de etiquetas:

* [Clave GPG](https://github.com/adobe/reactor-developer-docs/blob/master/files/launch%40adobe.com_pub.gpg)
* [Suma de comprobación](https://github.com/adobe/reactor-developer-docs/blob/master/files/launch%40adobe.com_pub.gpg.sum)

## Importación de la clave al llavero

Una vez guardada la clave en el equipo, el siguiente paso es agregarla al llavero GPG.

**Sintaxis**

```shell
gpg --import {KEY_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{KEY_NAME}` | Nombre del archivo de clave pública. |

{style="table-layout:auto"}

**Ejemplo**

```shell
gpg --import launch@adobe.com_pub.gpg
```

## Cifrado de valores

Después de agregar la clave al llavero, puede empezar a cifrar valores utilizando el indicador `--encrypt`. La siguiente secuencia de scripts muestra cómo funciona este comando:

```shell
echo -n 'Example value' | gpg --armor --encrypt -r "Tags Data Encryption <launch@adobe.com>"
```

Este comando se puede desglosar de la siguiente manera:

* La entrada se suministra al comando `gpg`.
* `--armor` crea resultados blindados con ASCII en lugar de binarios. Esto simplifica la transferencia del valor a través de JSON.
* `--encrypt` indica a GPG que cifre los datos.
* `-r` establece el destinatario de los datos. Solo el destinatario (el titular de la clave privada que corresponde a la clave pública) puede descifrar los datos. El nombre del destinatario de la clave deseada se puede encontrar examinando el resultado de `gpg --list-keys`.

El comando anterior utiliza la clave pública para `Tags Data Encryption <launch@adobe.com>` cifrar el valor, `Example value`, en formato ASCII blindado.

El resultado del comando sería similar al siguiente:

```shell
-----BEGIN PGP MESSAGE-----

hQIMAxJHCI6fydT/ARAAwQ0Y0k7eSAbd0T9seoaWX75G70O2gxAF20KY5FWiZ9/m
/RkgJwhJusZyEdazC/CmAdfXi9bsVxQT0i06ErUxXfQF0VtweRlcyRBsxzLz6Hr+
BpYGnq+cCCzGAT73Gg1CM4UWmaPKLLyWKGkXtDBAqVBRAIQT/8JhnkbyWIohHkWV
I/Uf7NrPXuaSmrqZ1SZQgwjIM3qNMR02qtqg59dncKoCQBji8Oeb8lqRLskRT0Jq
gVgbJYwSe2n6KpJkELJ6QtF9lCRl1+yU4mvM4jBHgkM1+vb1WmbFRIR40dDpg85N
0J9hVj4bg//eLRDfAdEC9kgq9Atph0WqJ5EpehdS7yVO9lO8mpbpqZ4BCGjTi/VS
isEPr6eZ2mxRbk8f9Z4csRZnkErY8ep5+cqC5CZVdmguWvC9PKzXqEsPFd0PSYk3
Qp3UIW2/JMf16E5CKmntm+gKdl6kggZOOvNQuyJYa9yNbzySPerHXsknTOxV+QP/
WXwrAL52g5+gpMib7Ve/KBz5/OViDhDqkmHzlGad73W74d+CYjf0AnuXuWRRlUMT
s8ORw1eplInldhXk2mgkGPZS/gWDs3zpKUu4GSO9AaeWldynLG/Bgh78XhumQ58h
ekGD+p3PyyvxjfS5G/wf9HQZ085+mnjpKFa7fuFBQPbg4WpBadhWrhobthC+hN3S
SAE9yWU11Y3xpoxqg4y7iYZ6rnX+qP2oUNYxC2/hdhsFbbZtUh4s51qaoLbe0iWB
OUoIPf4KxTaboHZOEy32ZBng5heVrn4i9w==
=jrfE
-----END PGP MESSAGE-----
```

Este resultado solo puede ser descifrado por sistemas que tengan la clave privada que
corresponde a la clave pública `Tags Data Encryption <launch@adobe.com>`.

Este resultado es el valor que debe suministrarse en un al enviar datos a la API de Reactor. El sistema almacena este resultado cifrado y lo descifra temporalmente según sea necesario. Por ejemplo, el sistema descifra las credenciales del host el tiempo suficiente para iniciar una conexión con el servidor y, a continuación, elimina inmediatamente todos los rastros del valor descifrado.

>[!NOTE]
>
>El formato del valor cifrado blindado es importante. Asegúrese de que los retornos de línea se escapen correctamente en el valor proporcionado en la solicitud.
