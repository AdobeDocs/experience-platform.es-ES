---
keywords: Experience Platform;inicio;temas populares;orígenes;conectores;oracle;
title: (Beta) Crear una conexión de origen de Oracle Responsys mediante la interfaz de usuario de Experience Platform
description: Obtenga información sobre cómo conectar Adobe Experience Platform a Oracle Responsys mediante la interfaz de usuario de Experience Platform.
hide: true
hidefromtoc: true
exl-id: 9ec5e1c2-3d9e-4729-be81-89a85d5ea782
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 2%

---

# (Beta) Crear una conexión de origen [!DNL Oracle Responsys] mediante la interfaz de usuario de Experience Platform

>[!NOTE]
>
>El origen [!DNL Oracle Responsys] está en la versión beta. Consulte [Resumen de fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Este tutorial proporciona los pasos para crear una conexión de origen [[!DNL Oracle Responsys]](../../../../connectors/marketing-automation/oracle-responsys.md) mediante la interfaz de usuario de Adobe Experience Platform.

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Si ya tiene una cuenta de [!DNL Oracle Responsys] autenticada en Experience Platform, puede omitir el resto de este documento y continuar con el tutorial sobre [creación de un flujo de datos para llevar los datos de automatización de marketing a Experience Platform](../../dataflow/marketing-automation.md).

### Recopilar credenciales necesarias

Para conectar [!DNL Oracle Responsys] a Experience Platform, debe proporcionar valores para las siguientes propiedades de autenticación:

| Credencial | Descripción |
| --- | --- |
| Punto de conexión | La URL del extremo de autenticación REST de su instancia [!DNL Oracle Responsys]. |
| ID de cliente | Identificador de cliente de su instancia [!DNL Oracle Responsys]. |
| Secreto del cliente | El secreto de cliente de su instancia [!DNL Oracle Responsys]. |

Para obtener más información sobre las credenciales de autenticación de [!DNL Oracle Responsys], consulte la [[!DNL Oracle Responsys] guía de autenticación](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su cuenta de [!DNL Oracle Responsys] a Experience Platform.

## Conectar su cuenta de [!DNL Oracle Responsys]

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Fuentes]** en el panel de navegación izquierdo para acceder al área de trabajo [!UICONTROL Fuentes]. La pantalla [!UICONTROL Catálogo] muestra una variedad de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría [!UICONTROL Automatización de marketing], seleccione **[!UICONTROL Oracle Responsys]** y, a continuación, seleccione **[!UICONTROL Agregar datos]**.

![El catálogo de orígenes de Adobe Experience Platform con el origen Oracle Responsys resaltado.](../../../../images/tutorials/create/oracle-responsys/catalog.png)

Aparecerá la página **[!UICONTROL Conectar la cuenta de Responsys de Oracle]**. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para usar una cuenta existente, seleccione la cuenta de [!DNL Oracle Responsys] con la que desee crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![Pantalla de autenticación de cuenta existente para Oracle Responsys.](../../../../images/tutorials/create/oracle-responsys/existing.png)

### Nueva cuenta

Para crear una nueva cuenta, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre, una descripción opcional y los valores apropiados para sus credenciales de [!DNL Oracle Responsys]. Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y deje pasar un tiempo para que se establezca la nueva conexión.

![La nueva pantalla de autenticación de cuenta para Oracle Responsys.](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Pasos siguientes

Siguiendo este tutorial, ha autenticado y creado una conexión de origen entre su cuenta de [!DNL Oracle Responsys] y Experience Platform. Ahora puede continuar con el siguiente tutorial y [crear un flujo de datos para llevar los datos de automatización de marketing a Experience Platform](../../dataflow/marketing-automation.md).
