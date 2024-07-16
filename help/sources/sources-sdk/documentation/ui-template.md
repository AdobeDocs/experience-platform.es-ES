---
keywords: Experience Platform;inicio;temas populares;fuentes;conectores;conectores de origen;sdk de fuentes;sdk;SDK
title: Plantilla de documentación de autoservicio para la interfaz de usuario
description: Obtenga información sobre cómo crear una conexión de origen YOURSOURCE mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 6471c0a2-22e8-4133-a76f-ee3c5c669ef8
source-git-commit: 1ed82798125f32fe392f2a06a12280ac61f225c6
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 1%

---

# Crear una conexión de origen *YOURSOURCE* en la interfaz de usuario

*A medida que revise esta plantilla, reemplace o elimine todos los párrafos en cursiva (comenzando por este párrafo).*

*Comience por actualizar los metadatos (título y descripción) en la parte superior de la página. Ignore todas las instancias de UICONTROL en esta página. Esta es una etiqueta que ayuda a nuestros procesos de traducción automática a traducir correctamente la página a los múltiples idiomas que admitimos. Agregaremos etiquetas a su documentación después de que la envíe.*

Este tutorial proporciona los pasos para crear un conector de origen *YOURSOURCE* mediante la interfaz de usuario de Platform.

## Información general

*Proporcione una breve descripción general de su compañía, incluido el valor que proporciona a los clientes. Incluya un vínculo a la página principal de la documentación del producto para obtener más información.*

>[!IMPORTANT]
>
>El equipo *YourSource* crea y mantiene este conector de origen y esta página de documentación. Para cualquier consulta o solicitud de actualización, comuníquese directamente con ellos en *Inserte un enlace o una dirección de correo electrónico donde pueda obtener información sobre actualizaciones*.

## Requisitos previos

*Agregue información en esta sección acerca de todo lo que los clientes deban tener en cuenta antes de comenzar a configurar el origen en la interfaz de usuario de Adobe Experience Platform. Puede ser aproximadamente:*

* *es necesario agregarlo a una lista de permitidos*
* *requisitos para el hash de correo electrónico*
* *cualquier detalle de la cuenta a su lado*
* *cómo obtener las credenciales de autenticación para conectarse a su plataforma*

### Recopilar credenciales necesarias

Para conectar *YOURSOURCE* a Platform, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| *credencial uno* | *Agregue una breve descripción a la credencial de autenticación de origen aquí* | *Agregue un ejemplo de la credencial de autenticación de origen aquí* |
| *credencial dos* | *Agregue una breve descripción a la credencial de autenticación de origen aquí* | *Agregue un ejemplo de la credencial de autenticación de origen aquí* |
| *credencial tres* | *Agregue una breve descripción a la credencial de autenticación de origen aquí* | *Agregue un ejemplo de la credencial de autenticación de origen aquí* |

Para obtener más información sobre estas credenciales, consulte la documentación de autenticación *YOURSOURCE*. *Agregue un vínculo a la documentación de autenticación de su plataforma aquí*.

## Conecta tu cuenta de *YOURSOURCE*

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en la barra de navegación izquierda para acceder al área de trabajo [!UICONTROL Sources]. La pantalla [!UICONTROL Catálogo] muestra una variedad de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría *CATEGORÍA DE TU FUENTE*, selecciona *TU FUENTE* y, a continuación, selecciona **[!UICONTROL Agregar datos]**.

>[!TIP]
>
>Las capturas de pantalla utilizadas a continuación son ejemplos. Al crear su documentación, reemplace las imágenes por capturas de pantalla de su origen real. Puede utilizar la misma trama de marcado y el mismo color, así como los mismos nombres de archivo. Asegúrese de que la captura de pantalla capture toda la pantalla de la interfaz de usuario de Platform. Para obtener información sobre cómo cargar tus capturas de pantalla, consulta la guía sobre [enviar tu documentación para revisión](./github.md).

![catálogo](../assets/ui/catalog.png)

Aparecerá la página **[!UICONTROL Conectar su cuenta de origen]**. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para usar una cuenta existente, selecciona la cuenta de *YOURSOURCE* con la que deseas crear un nuevo flujo de datos y luego selecciona **[!UICONTROL Siguiente]** para continuar.

![existente](../assets/ui/existing.png)

### Nueva cuenta

Si va a crear una cuenta nueva, seleccione **[!UICONTROL Cuenta nueva]** y, a continuación, proporcione un nombre, una descripción opcional y sus credenciales. Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y deje pasar un tiempo para que se establezca la nueva conexión.

![nuevo](../assets/ui/new.png)

## Pasos siguientes

*Los flujos de trabajo para los pasos restantes de la creación de un flujo de datos están modularizados. Si desea realizar alguna llamada específica con respecto a su origen, consulte la sección de recursos adicionales a continuación.*

Siguiendo este tutorial, ha establecido una conexión con su cuenta de *YOURSOURCE*. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en la plataforma](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/dataflow/crm.html).

## Recursos adicionales

*Esta es una sección opcional donde puede proporcionar más vínculos a la documentación del producto o a cualquier otro paso, captura de pantalla o matiz que considere importante para que el cliente tenga éxito. Puede utilizar esta sección para agregar información o sugerencias sobre todo el flujo de trabajo del origen, especialmente si hay problemas específicos que podría encontrar un usuario final.*
