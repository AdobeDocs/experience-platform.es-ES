---
title: Conectar Azure Databricks A Experience Platform Mediante La IU
description: Obtenga información sobre cómo conectar Azure Databricks a Experience Platform mediante la interfaz de usuario.
badgeUltimate: label="Ultimate" type="Positive"
badgeBeta: label="Beta" type="Informative"
source-git-commit: 2bd16d5a55c5bbeedbc6a6012d9f0229eee8433a
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 4%

---

# Conectar [!DNL Azure Databricks] a Experience Platform en la interfaz de usuario

>[!AVAILABILITY]
>
>* El origen [!DNL Azure Databricks] está disponible en el catálogo de orígenes para los usuarios que han adquirido Real-Time CDP Ultimate.
>
>* El origen [!DNL Azure Databricks] está en la versión beta. Lea los [términos y condiciones](../../../../home.md#terms-and-conditions) en la descripción general de orígenes para obtener más información sobre el uso de orígenes etiquetados como beta.

Lea esta guía para obtener información sobre cómo conectar su cuenta de [!DNL Azure Databricks] a Adobe Experience Platform mediante el área de trabajo de orígenes en la interfaz de usuario.

## Introducción 

Esta guía requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Recopilar credenciales necesarias

Proporcione valores para las siguientes credenciales a fin de conectar [!DNL Azure Databricks] a Experience Platform.

| Credencial | Descripción |
| --- | --- |
| Dominio | La URL de su área de trabajo [!DNL Azure Databricks]. Por ejemplo, `https://adb-1234567890123456.7.azuredatabricks.net`. |
| ID de clúster | El identificador de su clúster en [!DNL Azure Databricks]. Este clúster ya debe ser un clúster existente y debe ser un clúster interactivo. |
| Token de acceso | El token de acceso que autentica su cuenta de [!DNL Azure Databricks]. Puede generar el token de acceso mediante el área de trabajo [!DNL Azure Databricks]. |
| Base de datos | Nombre de la base de datos en el lago delta. |

Para obtener más información, lea la [[!DNL Azure Databricks] información general](../../../../connectors/databases/databricks.md).

## Navegar por el catálogo de fuentes

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Fuentes]** en el panel de navegación izquierdo para acceder al área de trabajo *[!UICONTROL Fuentes]*. Elija una categoría o utilice la barra de búsqueda para encontrar el origen.

Para conectarse a [!DNL Azure Databricks], vaya a la categoría *[!UICONTROL Bases de datos]*, seleccione la tarjeta de origen de **[!UICONTROL Azure Databricks]** y, a continuación, seleccione **[!UICONTROL Configurar]**.

>[!TIP]
>
>Los orígenes del catálogo de orígenes muestran la opción **[!UICONTROL Set up]** cuando un origen determinado aún no tiene una cuenta autenticada. Una vez creada una cuenta autenticada, esta opción cambia a **[!UICONTROL Agregar datos]**.

![El catálogo de orígenes con la tarjeta de origen de Azure Databricks seleccionada.](../../../../images/tutorials/create/databricks/catalog.png)

### Usar una cuenta existente

Para usar una cuenta existente, seleccione **[!UICONTROL Cuenta existente]** y luego seleccione la cuenta [!DNL Azure Databricks] que desee usar.

![Interfaz de cuentas existentes en el flujo de trabajo de orígenes con la opción Cuenta existente seleccionada.](../../../../images/tutorials/create/databricks/existing.png)

### Crear una nueva cuenta

Para crear una cuenta nueva, selecciona **[!UICONTROL Cuenta nueva]**, proporciona un nombre y, opcionalmente, agrega una descripción para tu cuenta. A continuación, proporcione valores para las siguientes credenciales de autenticación:

* Dominio
* ID de clúster
* Token de acceso
* Base de datos

![La nueva interfaz de cuenta en el flujo de trabajo de orígenes con un nombre de cuenta y una descripción opcional proporcionados.](../../../../images/tutorials/create/databricks/new.png)

Además, debe copiar y pegar sus credenciales de [!UICONTROL URI SAS de ensayo] en su entorno [!DNL Azure Databricks]. Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y espere unos momentos para que se establezca la conexión.

![Credenciales de ensayo de URI de SAS.](../../../../images/tutorials/create/databricks/sas-uri.png)

## Crear un flujo de datos para [!DNL Azure Databricks] datos

Ahora que ha conectado correctamente su cuenta de [!DNL Azure Databricks], puede [crear un flujo de datos e introducir datos de su base de datos en Experience Platform](../../dataflow/databases.md).
