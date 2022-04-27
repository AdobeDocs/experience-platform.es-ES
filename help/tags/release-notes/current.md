---
title: Notas de la versión para etiquetas
description: Las notas de la versión más recientes para etiquetas de Adobe Experience Platform.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: a15b5525d3a2fa034715803c83dc22a94915347e
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 58%

---

# Notas de la versión para etiquetas en Adobe Experience Platform

>[!NOTE]
>
>Adobe Experience Platform Launch se está convirtiendo en un conjunto de tecnologías de recopilación de datos en Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

## 15 de noviembre de 2021

**Aceptar código ES6 en etiquetas** - Las extensiones y el código personalizado que contienen código ES6 ahora se pueden utilizar en etiquetas. En el catálogo de extensiones verá una etiqueta ES6+ dentro de la tarjeta de cada extensión que contenga código ES6. IE10 e IE11 no admiten código ES6. Antes de usar código ES6 en sus bibliotecas de etiquetas, siga con la debida diligencia.

**Uso de Terser como compresor de JavaScript** - Uglifier fue reemplazado por Terser. A partir de esta versión, Terser minifica todas las bibliotecas de etiquetas.

## 21 de octubre de 2021

**Enviar datos a puntos de conexión autenticados en el reenvío de eventos** - Utilizando secretos, puede enviar datos a puntos finales que requieran los siguientes protocolos de autenticación:

* **[!UICONTROL Token]**: Una cadena única de caracteres que representan un valor de token de autenticación.
* **[!UICONTROL HTTP simple]**: Contiene dos atributos de cadena para un nombre de usuario y una contraseña.
* **[!UICONTROL OAuth2]**: Contiene varios atributos para admitir la variable [OAuth2](https://datatracker.ietf.org/doc/html/rfc6749) especificación.

Para obtener más información, consulte las guías de [administración de secretos en la interfaz de usuario de recopilación de datos](../ui/event-forwarding/secrets.md) o [administración de secretos en la API de Reactor](../api/guides/secrets.md).

## 19 de julio de 2021

**Ajustes a la derecha &quot;Administrar propiedades&quot;** - El derecho de gestión de propiedades encontró un problema en el que un usuario tenía el permiso para crear una nueva propiedad, pero no podía verla después de crearla (como se describe en el subproceso de comunidad) [here](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/technical-advisory-adjustments-to-the-manage-properties/ba-p/399176)). Una corrección ya está activa y los permisos se aplican tal como se describe en el artículo.

>[!NOTE]
>
>Si asigna el nuevo derecho &quot;Editar propiedad&quot; a un grupo de usuarios, la interfaz de usuario no se actualizará para habilitar los campos en la pantalla de configuración de propiedades. En una próxima versión se implementará una solución para este problema.

## 17 de mayo de 2021

**Mejor gestión de los cambios no guardados**: Antes, cada vez que se alejaba de una vista de configuración (extensiones, elementos de datos y componentes de regla), se le preguntaba si quería descartar los cambios. Pero la lógica para determinar eso no era la mejor, así que la mayor parte del tiempo se le pedía que guardara los cambios aunque no hubiera ninguno. Se ha solucionado. A partir de ahora, solo debería ver ese mensaje cuando haya realizado cambios.

## 10 de mayo de 2021

**Publicación simplificada**: Ya no es necesario compilar en el entorno de ensayo. Si tiene los derechos adecuados, puede omitir completamente el estado Enviado y publicar directamente desde Desarrollo, siempre y cuando la compilación se haya hecho correctamente y no haya otras bibliotecas en orden ascendente.

## 22 de abril de 2021

**Recopilación de datos de Adobe Experience Platform**: El envío de datos a Adobe no se trata solo de implementar etiquetas en el sitio o de configurar en la aplicación.  El uso de los SDK de Experience Platform y de la red perimetral requiere acceso a otras funcionalidades de Platform. Esto requería iniciar sesión en varias herramientas diferentes, pero ahora están juntas en un solo lugar.

La recopilación de datos en Platform consta de seis funciones, y la navegación recién optimizada solo contendrá los elementos a los que tienen acceso su compañía y su cuenta de usuario.  Algunos de los nombres de las capacidades también se han actualizado para que coincidan con los patrones de nomenclatura de Experience Platform.

* Cliente (anteriormente conocido como &quot;lado del cliente&quot;)
* Datastreams (anteriormente conocido como &quot;Configuración de Edge&quot;)
* Servidor (anteriormente conocido como &quot;lado del servidor&quot;)
* Configuraciones de aplicaciones
* Esquemas
* Identidades

Esperamos recibir más actualizaciones a medida que Experience Platform y la recopilación de datos sigan evolucionando.

## 18 de febrero de 2021

* Se ha actualizado la interfaz de usuario de Recopilación de datos a react-spectrum v3
* Se han actualizado las tarjetas de extensión a los últimos patrones de espectro
* Se ha aumentado el tamaño de los campos de nombre en toda la aplicación

## 13 de enero de 2021

**Disponibilidad general: Reenvío de eventos** Envíe datos de nivel de evento a Adobe Experience Platform Edge Network y, a continuación, utilice el reenvío de eventos para transformar, enriquecer y enviar dichos datos a un punto final que no sea de Adobe mediante los servidores de Adobe, no del cliente, con baja latencia.

Consulte la [información general sobre el reenvío de eventos](../ui/event-forwarding/overview.md) y [guía de introducción](../ui/event-forwarding/getting-started.md) para obtener más información.
