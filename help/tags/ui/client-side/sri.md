---
title: Ayuda sobre Integridad de los subrecursos (SRI)
description: Conozca cómo se admite la Integridad de los subrecursos (SRI) en Adobe Experience Platform.
exl-id: bd8bc3f7-9a85-44e2-ae07-f0664179b51c
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 97%

---

# Ayuda sobre Integridad de los subrecursos (SRI)

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Este documento cubre cómo se admite la Integridad de los subrecursos (SRI) en Adobe Experience Platform.

Los sitios web modernos se crean haciendo referencia a imágenes, contenido y secuencias de comandos de diversas ubicaciones de la web. La Integridad de subrecursos (SRI) permite que un explorador verifique que el contenido de un archivo solicitado no se haya modificado inesperadamente.

Aunque sus casos de uso se complementan entre sí, la SRI es diferente de una Política de seguridad de contenido (CSP), que garantiza que solo se permitan en el sitio web los archivos de fuentes de confianza. La SRI va un paso más allá al garantizar que el contenido de estos archivos se ajusta a sus expectativas.

>[!NOTE]
>
>Para obtener información más detallada sobre la SRI, consulte los [documentos web de MDN](https://developer.mozilla.org/es-ES/docs/Web/Security/Subresource_Integrity).

El proceso de validación de la SRI se puede resumir de la siguiente manera:

1. Puede generar un hash criptográfico del recurso que desea validar.
1. En el sitio web, el hash se coloca en el atributo `integrity` del elemento HTML que carga el archivo.
1. Cuando el navegador ve el atributo `integrity`, solicita el recurso y genera de forma independiente su propia versión del hash criptográfico.
1. El explorador compara el hash de `integrity` con el que generó. Si coinciden, se permite el recurso. Si no coinciden, el recurso se bloqueará.

## Limitaciones en los sistemas de administración de etiquetas

Como sistema de administración de etiquetas (TMS), las etiquetas de Adobe Experience Platform proporcionan una compilación de biblioteca JavaScript que se carga en las páginas con un solo elemento `<script>` (código incrustado). La funcionalidad dinámica que ofrece el sistema de administración de etiquetas se logra intercambiando el contenido de ese script dinámicamente sin que sea necesario cambiar nada más.

Sin embargo, cuando cambia el contenido de la secuencia de comandos, también cambia el hash criptográfico de dicho contenido. Por lo tanto, la única manera de hacer que la SRI funcione con un sistema de administración de etiquetas es actualizar el código incrustado al mismo tiempo que se publica una nueva compilación. Para muchos, esto es contrario al objetivo principal de usar un sistema de administración de etiquetas.

La siguiente mejor opción de seguridad para las etiquetas es implementar una política de seguridad de contenido. Para obtener más información, consulte la guía de [CSP y etiquetas](./content-security-policy.md).

## Integración de la SRI en la implementación de la compilación

Si aún desea utilizar la SRI para las compilaciones de su biblioteca, debe utilizar un alojamiento propio. Si utiliza un alojamiento administrado por Adobe, no hay forma de utilizar la SRI sin tener que pasar algún tiempo en el que el nuevo contenido de la compilación no coincida con el atributo `integrity` del código incrustado.

La automatización del proceso de actualización del código incrustado variará en complejidad según la estructura del sitio, pero los pasos generales se pueden resumir de la siguiente manera:

1. Recupere la compilación de la biblioteca de producción, ya sea a través del envío SFTP o descargando el archivo desde la interfaz de usuario.
1. Genere el hash criptográfico de la compilación principal.
1. Asegúrese de que el atributo `integrity` del código incrustado se actualiza al nuevo hash y de que la compilación a la que se hace referencia se actualiza como parte de la misma implementación.

>[!IMPORTANT]
>
>Esta estrategia solo cubre la compilación principal. No incluye ninguno de los archivos más pequeños que puedan existir.

## Pasos siguientes

Este documento abarcaba las limitaciones de usar la SRI con etiquetas y los pasos necesarios para integrarla en las implementaciones de la compilación de la biblioteca a pesar de esas limitaciones. Si aún no lo ha hecho, se recomienda que lea la guía de [CSP y etiquetas](./content-security-policy.md) para ver una opción de seguridad alternativa.
