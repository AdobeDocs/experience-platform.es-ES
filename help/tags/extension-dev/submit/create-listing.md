---
title: Crear un listado de intercambio para una extensión
description: Obtenga información sobre cómo añadir la extensión al catálogo público en Adobe Experience Platform.
exl-id: 0395fc99-5e2b-46d6-a067-f8f167733e02
source-git-commit: 0d98183838125fac66768b94bc1993bde9a374b5
workflow-type: tm+mt
source-wordcount: '1193'
ht-degree: 69%

---

# Crear un listado de intercambio para una extensión

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un grupo de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Adobe Experience Platform tiene un único catálogo en el que los usuarios pueden ver las extensiones de etiquetas disponibles para la instalación. Este catálogo está disponible dentro del producto y contiene extensiones de tres tipos:

1. **Extensiones públicas**: Se trata de extensiones completas diseñadas para su uso en producción por cualquier usuario.
1. **Extensiones privadas**: Se trata de extensiones completas y diseñadas para la producción, pero que fueron desarrolladas por otros usuarios de su empresa y solo están disponibles para los usuarios de su empresa.
1. **Extensiones de desarrollo**: Estas extensiones están en desarrollo activo y solo están disponibles dentro de su empresa y solo en una propiedad que está específicamente designada como propiedad de desarrollo.

Independientemente de las extensiones del catálogo de productos, las extensiones públicas también tienen listas en [Experience Cloud Exchange App Marketplace](https://exchange.adobe.com/apps/browse/ec).

Estas listas permiten a los desarrolladores de extensiones publicar descripciones de la funcionalidad, proporcionar vínculos a documentación o asistencia adicional y comercializar extensiones a posibles usuarios que pueden no conocer su empresa o la funcionalidad de su extensión. En este mercado, su extensión tendrá un anuncio público que se podrá consultar sin que el usuario tenga que autenticarse en Platform. Para las extensiones públicas, la creación de esta lista de Exchange es un paso obligatorio.

>[!TIP]
>
>Cuando se publique su anuncio de Exchange, se agregará automáticamente un vínculo al contenido del anuncio que permitirá a sus clientes y clientes potenciales hacer clic en y `Connect with publisher` para obtener más información sobre sus productos y servicios. No se muestra su dirección de correo electrónico de contacto, ya que el sistema de Exchange le reenviará estos mensajes.

Si no tiene una empresa donde cargar y probar el paquete de extensión, debe registrarse en el programa Exchange y comenzar una lista. Esto almacenará en déclencheur la creación de una cuenta de empresa (este proceso tarda un poco; recibirá un correo electrónico cuando se complete) que puede utilizar para cargar y probar la extensión. De nuevo, los listados de Exchange solo son necesarios para extensiones públicas.

Si ya tiene una cuenta de empresa o si no necesita un listado de Exchange (solo extensiones privadas), puede omitir el resto de este paso y continuar [cargando y probando la extensión](./upload-and-test.md).

## Crear un anuncio

>[!NOTE]
>
>El siguiente proceso detalla la creación de una lista de aplicaciones en el programa de Adobe Exchange. Este es el término que se utiliza para las distintas integraciones y extensiones de Adobe Experience Platform.

![Ubicación del vínculo del Administrador de aplicaciones de Experience Cloud](../images/getting-started/app-mgr-link.png)

1. Inicie sesión en el [sitio de socios de Exchange](https://partners.adobe.com/exchangeprogram/experiencecloud). Cuando haya iniciado sesión, seleccione el vínculo del **Administrador de aplicaciones** junto a su nombre.
1. Seleccione la pestaña **Crear nueva aplicación** y, a continuación, seleccione **Crear nueva aplicación** para una solución personalizada, o seleccione una plantilla.
1. Proporcione la información de su anuncio. Para obtener información detallada sobre App Manager, consulta el [artículo](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360024197931) completo. La información de la lista debería aclarar qué hace la extensión y por qué resulta útil. La lista funciona como un espacio de marketing para la aplicación. Promocione la extensión aquí con descripciones claras, vínculos a páginas de destino del sitio, vínculos a documentos de ayuda o direcciones de correo electrónico de asistencia, etc. Aunque el espacio en las vistas de extensión es limitado, la lista de Exchange ofrece la oportunidad de promocionar tanto la extensión como la compañía. A continuación, se presentan sugerencias para mejorar la promoción de la extensión:
   - **Icono de la aplicación** - Asegúrese de que el icono de la lista de Exchange tenga las dimensiones adecuadas de 512 x 512 para archivos png o una relación de aspecto de 1:1 para jpg.

     >[!NOTE]
     >
     >Nota: Este es un formato de archivo diferente del que utilizará en el código de la extensión. La extensión contendrá un archivo svg como [icono](../manifest.md).

   - **Imagen destacada**: obtenga atención con una imagen independiente que mostrará su marca y resaltará su aplicación. La imagen destacada es la que se muestra cuando alguien comparte un vínculo a su anuncio de Exchange o publica contenido sobre él en medios sociales. Por lo tanto, debe ser una representación modelo de su marca.
   - **Logotipo del editor de la aplicación**: se trata del logotipo de su empresa. Asegúrese de que el icono tenga las dimensiones adecuadas de 1280 x 720 o de 2560 x 1440 (16:9) en formato png o jpg, respectivamente.
   - **Instrucciones de configuración**: Informe a los clientes sobre cómo configurar la extensión de Adobe Experience Platform. Asegúrese de que comprendan la configuración que deben realizar, así como los pasos siguientes que deben seguir cuando la [vista de configuración](../configuration.md) aparezca inmediatamente después de instalar la extensión en una propiedad.
   - **Etiquetas**: en la primera página de edición del anuncio, asegúrese de incluir la palabra &quot;Launch&quot; en el campo &quot;Etiquetas personalizadas&quot;. Esto hará que su anuncio aparezca en las búsquedas de etiquetas en Exchange Marketplace:
     ![](../images/getting-started/custom-tags.jpg)
   - **Zonas protegidas**: Su acceso a las soluciones de Adobe se realiza a través de una cuenta de zona protegida en la que tiene acceso a una versión de Adobe Experience Platform que funciona completamente. Estas cuentas de zona protegida se solicitan a medida que crea su anuncio de aplicaciones. En la sección **Conexiones**, seleccione las conexiones específicas aplicables a la aplicación que ha creado (su extensión de la etiqueta) y, cuando pulse **Guardar**, se generará la solicitud de zona protegida si es necesario.
1. Envíe su anuncio. El equipo de Adobe Exchange revisará su aplicación y proporcionará comentarios si es necesario hacer algún cambio. Si marca la casilla **Publicar inmediatamente** al enviar el anuncio, este se publicará inmediatamente después de su aprobación. Si desea publicar la aplicación más adelante, deje la casilla de verificación sin marcar. Cuando se apruebe el anuncio de la extensión, aparecerá el botón azul **Publicar** junto al anuncio en la página de anuncios de la aplicación (extensión).

### Crear un anuncio eficaz

Consulte nuestras [Directrices de envío de aplicaciones](https://partners.adobe.com/exchangeprogram/experiencecloud/build/ec-exchange.html) para obtener información detallada sobre cómo crear listados atractivos.

#### Pasos a seguir tras el envío del anuncio de Exchange

Tras el envío, el equipo de Adobe Exchange revisará la aplicación y la aprobará o le responderá con comentarios sobre los cambios que necesita. Este proceso se detalla en las Directrices de envío de aplicaciones.

Si no tiene dispone de credenciales para iniciar sesión en el sitio de Exchange, asegúrese de que su correo electrónico esté registrado en el programa de Exchange siguiendo las instrucciones que se detallan en la [Guía de registro del programa](https://partners.adobe.com/content/mcp/us/en/home/reg-guide.html). Cada usuario debe asociar su correo electrónico con la cuenta de socio de su compañía. Las preguntas sobre este proceso se pueden dirigir por correo electrónico a <ExchangeHelpEC@adobe.com>.

#### Actualizar el listado de Exchange tras la aprobación inicial

Cuando actualice la extensión o solo necesite actualizar el listado de Exchange, inicie sesión en el [Portal de socios](https://partners.adobe.com/exchangeprogram/experiencecloud) y seleccione el botón App Manager que aparece junto a su nombre. A continuación, seleccione la aplicación y siga el flujo anterior que se utilizó inicialmente para crear el listado. Una vez reenviado, el equipo de Adobe Exchange revisará los cambios y los aprobará, o bien le responderá con comentarios sobre los cambios.

## Vinculación del paquete de extensión al listado

Una vez aprobado el listado y disponible públicamente, le recomendamos que proporcione un enlace al listado público en el campo `exchange_url` del archivo `extension.json` dentro del paquete de extensión.  Esto creará un vínculo de Más información dentro del catálogo de extensiones de etiquetas para que los usuarios dentro del producto puedan encontrar el anuncio y su información adicional.
