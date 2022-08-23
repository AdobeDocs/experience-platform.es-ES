---
keywords: Experience Platform;inicio;temas populares;Vantage de Teradata
title: Crear una conexión de origen de la ventaja de Teradata en la interfaz de usuario
description: Obtenga información sobre cómo crear una conexión de origen de Vantage de Teradata mediante la interfaz de usuario de Adobe Experience Platform.
source-git-commit: f140dac67ccd09ec1e6cab794f53e0090af55442
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 1%

---

# (Beta) Cree un [!DNL Teradata Vantage] conexión de origen en la interfaz de usuario

>[!NOTE]
>
> La variable [!DNL Teradata Vantage] el origen está en versión beta. Consulte la [Resumen de fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes con etiquetas beta.

Este tutorial proporciona los pasos para crear un [!DNL Teradata Vantage] conector de origen mediante la interfaz de usuario de Adobe Experience Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

### Recopilar las credenciales necesarias

Para acceder a su [!DNL Teradata Vantage] en Platform, debe proporcionar el siguiente valor de autenticación:

| Credencial | Descripción |
| ---------- | ----------- |
| Cadena de conexión | Una cadena de conexión es una cadena que proporciona información sobre un origen de datos y cómo puede conectarse a él. El patrón de cadena de conexión para [!DNL Teradata Vantage] es `DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}`. |

Para obtener más información sobre cómo empezar, consulte esta [[!DNL Teradata Vantage] documento](https://docs.teradata.com/r/Teradata-VantageTM-Advanced-SQL-Engine-Security-Administration/July-2021/Setting-Up-the-Administrative-Infrastructure/Controlling-Access-to-the-Operating-System/Working-with-OS-Level-Security-Options).

## Conecte su [!DNL Teradata Vantage] account

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** desde el panel de navegación izquierdo para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable [!UICONTROL Catálogo] muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la barra de búsqueda.

En el [!UICONTROL Bases de datos] categoría, seleccione **[!UICONTROL Teradata Vantage]** y, a continuación, seleccione **[!UICONTROL Añadir datos]**.

![](../../../../images/tutorials/create/teradata/catalog.png)

La variable **[!UICONTROL Conectarse al Teradata Vantage]** se abre. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para conectar una cuenta existente, seleccione la opción [!DNL Teradata Vantage] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![](../../../../images/tutorials/create/teradata/existing.png)

### Nueva cuenta

Si está utilizando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, indique un nombre, una descripción opcional y su [!DNL Teradata Vantage] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, permita que la nueva conexión se establezca durante algún tiempo.

![](../../../../images/tutorials/create/teradata/new.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de Vantage de Teradata. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en Platform](../../dataflow/databases.md).
