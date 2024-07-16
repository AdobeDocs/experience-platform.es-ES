---
keywords: Experience Platform;inicio;temas populares;orígenes;conectores;oracle;
title: (Beta) Crear una conexión de origen de Responsys de Oracle mediante la IU de Platform
description: Obtenga información sobre cómo conectar Adobe Experience Platform a Oracle Responsys mediante la IU de Platform.
hide: true
hidefromtoc: true
exl-id: 9ec5e1c2-3d9e-4729-be81-89a85d5ea782
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 2%

---

# (Beta) Crear una conexión de origen [!DNL Oracle Responsys] mediante la interfaz de usuario de Platform

>[!NOTE]
>
>El origen [!DNL Oracle Responsys] está en la versión beta. Consulte [Resumen de fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Este tutorial proporciona los pasos para crear una conexión de origen [[!DNL Oracle Responsys]](../../../../connectors/marketing-automation/oracle-responsys.md) mediante la interfaz de usuario de Adobe Experience Platform.

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Platform:

* [Fuentes](../../../../home.md): Platform permite la ingesta de datos de varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Si ya tiene una cuenta de [!DNL Oracle Responsys] autenticada en Platform, puede omitir el resto de este documento y continuar con el tutorial sobre [creación de un flujo de datos para llevar los datos de automatización de marketing a Platform](../../dataflow/marketing-automation.md).

### Recopilar credenciales necesarias

Para conectar [!DNL Oracle Responsys] a Platform, debe proporcionar valores para las siguientes propiedades de autenticación:

| Credencial | Descripción |
| --- | --- |
| Punto de conexión | La URL del extremo de autenticación REST de su instancia [!DNL Oracle Responsys]. |
| ID de cliente | Identificador de cliente de su instancia [!DNL Oracle Responsys]. |
| Secreto del cliente | El secreto de cliente de su instancia [!DNL Oracle Responsys]. |

Para obtener más información sobre las credenciales de autenticación de [!DNL Oracle Responsys], consulte la [[!DNL Oracle Responsys] guía de autenticación](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su cuenta de [!DNL Oracle Responsys] a Platform.

## Conectar su cuenta de [!DNL Oracle Responsys]

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al área de trabajo [!UICONTROL Sources]. La pantalla [!UICONTROL Catálogo] muestra una variedad de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría [!UICONTROL Automatización de marketing], seleccione **[!UICONTROL Oracle Responsys]** y, a continuación, seleccione **[!UICONTROL Agregar datos]**.

![El catálogo de orígenes Adobe Experience Platform con el origen Responsys de Oracle resaltado.](../../../../images/tutorials/create/oracle-responsys/catalog.png)

Aparecerá la página **[!UICONTROL Conectar cuenta de Responsys de Oracle]**. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para usar una cuenta existente, seleccione la cuenta de [!DNL Oracle Responsys] con la que desee crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![Pantalla de autenticación de cuenta existente para Responsys de Oracle.](../../../../images/tutorials/create/oracle-responsys/existing.png)

### Nueva cuenta

Para crear una nueva cuenta, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre, una descripción opcional y los valores apropiados para sus credenciales de [!DNL Oracle Responsys]. Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y deje pasar un tiempo para que se establezca la nueva conexión.

![La nueva pantalla de autenticación de cuenta para el Oracle Responsys.](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Pasos siguientes

Al seguir este tutorial, se ha autenticado y creado una conexión de origen entre su cuenta de [!DNL Oracle Responsys] y Platform. Ahora puede continuar con el siguiente tutorial y [crear un flujo de datos para llevar los datos de automatización de marketing a la plataforma](../../dataflow/marketing-automation.md).
