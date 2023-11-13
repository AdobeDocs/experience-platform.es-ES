---
keywords: Experience Platform;inicio;temas populares;Teradata Vantage
title: Creación de una conexión de origen de Teradata Vantage en la interfaz de usuario
description: Obtenga información sobre cómo crear una conexión de origen de Teradata Vantage mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 3fdb09fa-128a-477b-9144-d4ef3ed18ea6
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 1%

---

# (Beta) Cree una [!DNL Teradata Vantage] conexión de origen en la interfaz de usuario

>[!NOTE]
>
> El [!DNL Teradata Vantage] el origen está en versión beta. Consulte la [Resumen de orígenes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes etiquetadas como beta.

Este tutorial proporciona los pasos para crear una [!DNL Teradata Vantage] conector de origen mediante la interfaz de usuario de Adobe Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): El Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Recopilar credenciales necesarias

Para acceder a su [!DNL Teradata Vantage] en Platform, debe proporcionar el siguiente valor de autenticación:

| Credencial | Descripción |
| ---------- | ----------- |
| Cadena de conexión | Una cadena de conexión es una cadena que proporciona información sobre un origen de datos y cómo puede conectarse a él. El patrón de cadena de conexión para [!DNL Teradata Vantage] es `DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}`. |

Para obtener más información sobre cómo empezar, consulte esta [[!DNL Teradata Vantage] documento](https://docs.teradata.com/r/Teradata-VantageTM-Advanced-SQL-Engine-Security-Administration/July-2021/Setting-Up-the-Administrative-Infrastructure/Controlling-Access-to-the-Operating-System/Working-with-OS-Level-Security-Options).

## Conecte su [!DNL Teradata Vantage] account

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. El [!UICONTROL Catálogo] La pantalla muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar en la barra de búsqueda.

En el [!UICONTROL Bases de datos] categoría, seleccionar **[!UICONTROL Teradata Vantage]** y luego seleccione **[!UICONTROL Añadir datos]**.

![](../../../../images/tutorials/create/teradata/catalog.png)

El **[!UICONTROL Conectar con Teradata Vantage]** página. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para conectar una cuenta existente, seleccione la [!DNL Teradata Vantage] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![](../../../../images/tutorials/create/teradata/existing.png)

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y su [!DNL Teradata Vantage] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![](../../../../images/tutorials/create/teradata/new.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de Teradata Vantage. Ahora puede continuar con el siguiente tutorial y [configuración de un flujo de datos para introducir datos en Platform](../../dataflow/databases.md).
