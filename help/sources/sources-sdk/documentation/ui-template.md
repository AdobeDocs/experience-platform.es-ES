---
keywords: Experience Platform;inicio;temas populares;orígenes;conectores;conectores de origen;sdk de fuentes;sdk;SDK
title: Plantilla de documentación de autoservicio para la interfaz de usuario
description: Aprenda a crear una conexión de origen de YOURSOURCE mediante la interfaz de usuario de Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: 39accd28edc388c6444910f9a2ea6d2f01acfdaf
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 1%

---

# Cree un *YOURSOURCE* conexión de origen en la interfaz de usuario

*A medida que recorre esta plantilla, reemplace o elimine todos los párrafos en cursiva (a partir de este).*

*Comience por actualizar los metadatos (título y descripción) en la parte superior de la página. Ignore todas las instancias de UICONTROL en esta página. Esta es una etiqueta que ayuda a nuestros procesos de traducción automática a traducir correctamente la página a los múltiples idiomas compatibles. Añadiremos etiquetas a su documentación después de enviarla.*

Este tutorial proporciona los pasos para crear un *YOURSOURCE* conector de origen mediante la interfaz de usuario de Platform.

## Información general

*Proporcione una breve descripción general de su empresa, incluido el valor que proporciona a los clientes. Incluya un vínculo a la página de inicio de la documentación del producto para obtener más información.*

>[!IMPORTANT]
>
>Esta página de documentación la creó el *YOURSOURCE* equipo. Para cualquier consulta o solicitud de actualización, póngase en contacto con ellos directamente en *Inserte un vínculo o una dirección de correo electrónico donde pueda acceder a las actualizaciones*.

## Requisitos previos

*Agregue información en esta sección sobre cualquier cosa que los clientes deban tener en cuenta antes de comenzar a configurar el origen en la interfaz de usuario de Adobe Experience Platform. Esto puede tratarse de:*

* *necesidad de añadirlo a una lista de permitidos*
* *requisitos para el hash de correo electrónico*
* *cualquier información específica de la cuenta de su parte*
* *cómo obtener las credenciales de autenticación para conectarse a la plataforma*

### Recopilar las credenciales necesarias

Para conectarse *YOURSOURCE* en Platform, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| *credencial uno* | *Añada una breve descripción a la credencial de autenticación de la fuente aquí* | *Añada aquí un ejemplo de la credencial de autenticación de la fuente* |
| *credencial dos* | *Añada una breve descripción a la credencial de autenticación de la fuente aquí* | *Añada aquí un ejemplo de la credencial de autenticación de la fuente* |
| *credencial tres* | *Añada una breve descripción a la credencial de autenticación de la fuente aquí* | *Añada aquí un ejemplo de la credencial de autenticación de la fuente* |

Para obtener más información sobre estas credenciales, consulte la *YOURSOURCE* documentación de autenticación. *Añada el enlace a la documentación de autenticación de su plataforma aquí*.

## Conecte su *YOURSOURCE* account

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable [!UICONTROL Catálogo] muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En el *CATEGORÍA DE SU ORIGEN* categoría, seleccione *YOURSOURCE* y, a continuación, seleccione **[!UICONTROL Añadir datos]**.

>[!TIP]
>
>Las capturas de pantalla utilizadas a continuación son ejemplos. Al crear la documentación, reemplace las imágenes con capturas de pantalla de su fuente real. Puede utilizar el mismo patrón y color de marca, así como los mismos nombres de archivo. Asegúrese de que la captura de pantalla captura toda la pantalla de la interfaz de usuario de Platform. Para obtener información sobre cómo cargar las capturas de pantalla, consulte la guía de [enviar su documentación para su revisión](./github.md).

![catálogo](../assets/ui/catalog.png)

La variable **[!UICONTROL Conectar su cuenta de ORIGEN]** se abre. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para usar una cuenta existente, seleccione la opción *YOURSOURCE* cuenta con la que desee crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../assets/ui/existing.png)

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre, una descripción opcional y sus credenciales. Cuando termine, seleccione **[!UICONTROL Conectar a origen]** y, a continuación, permita que la nueva conexión se establezca durante algún tiempo.

![new](../assets/ui/new.png)

## Pasos siguientes

*Los flujos de trabajo para los pasos restantes de creación de un flujo de datos se modularizan. Si desea realizar alguna llamada específica con respecto a su origen, consulte la sección de recursos adicionales a continuación.*

Al seguir este tutorial, ha establecido una conexión con su *YOURSOURCE* cuenta. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en Platform](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/dataflow/crm.html).

## Recursos adicionales

*Esta es una sección opcional en la que puede proporcionar más vínculos a la documentación del producto o a cualquier otro paso, capturas de pantalla o matices que considere importantes para que el cliente tenga éxito. Puede utilizar esta sección para agregar información o sugerencias sobre todo el flujo de trabajo de su fuente, especialmente si hay problemas particulares que un usuario final podría encontrar.*
