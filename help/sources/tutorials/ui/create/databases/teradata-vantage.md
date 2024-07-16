---
keywords: Experience Platform;inicio;temas populares;Teradata Vantage
title: Creación de una conexión de Teradata Vantage Source en la interfaz de usuario
description: Obtenga información sobre cómo crear una conexión de origen de Teradata Vantage mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 3fdb09fa-128a-477b-9144-d4ef3ed18ea6
source-git-commit: 625a7959f48a0b16c3228d4555e046b5f67c51b7
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 2%

---

# Crear una conexión de origen [!DNL Teradata Vantage] en la interfaz de usuario

Este tutorial proporciona los pasos para crear un conector de origen [!DNL Teradata Vantage] mediante la interfaz de usuario de Adobe Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Platform:

* [Fuentes](../../../../home.md): el Experience Platform permite la ingesta de datos de varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): El Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Recopilar credenciales necesarias

Para acceder a su cuenta de [!DNL Teradata Vantage] en Platform, debe proporcionar el siguiente valor de autenticación:

| Credencial | Descripción |
| ---------- | ----------- |
| Cadena de conexión | Una cadena de conexión es una cadena que proporciona información sobre un origen de datos y cómo puede conectarse a él. El patrón de cadena de conexión de [!DNL Teradata Vantage] es `DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}`. |

Para obtener más información sobre cómo empezar, consulte este [[!DNL Teradata Vantage] documento](https://docs.teradata.com/r/Teradata-VantageTM-Advanced-SQL-Engine-Security-Administration/July-2021/Setting-Up-the-Administrative-Infrastructure/Controlling-Access-to-the-Operating-System/Working-with-OS-Level-Security-Options).

## Conectar su cuenta de [!DNL Teradata Vantage]

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al área de trabajo [!UICONTROL Sources]. Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría [!UICONTROL Bases de datos], seleccione **[!UICONTROL Ventaja de Teradata]** y, a continuación, seleccione **[!UICONTROL Configurar]**.

>[!TIP]
>
>Los orígenes del catálogo de orígenes muestran la opción **[!UICONTROL Set up]** cuando un origen determinado aún no tiene una cuenta autenticada. Una vez que existe una cuenta autenticada, esta opción cambia a **[!UICONTROL Agregar datos]**.

![El catálogo de orígenes con el origen Vantage de Teradata seleccionado.](../../../../images/tutorials/create/teradata/catalog.png)

Aparecerá la página **[!UICONTROL Conectar con Teradata Vantage]**. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de [!DNL Teradata Vantage] con la que desee conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![La página de cuentas existente en el área de trabajo de orígenes.](../../../../images/tutorials/create/teradata/existing.png)

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y sus credenciales de [!DNL Teradata Vantage]. Cuando termine, seleccione **[!UICONTROL Conectar]** y deje pasar un tiempo para que se establezca la nueva conexión.

![La nueva interfaz de creación de cuentas en el área de trabajo de orígenes.](../../../../images/tutorials/create/teradata/new.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de Teradata Vantage. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en la plataforma](../../dataflow/databases.md).
