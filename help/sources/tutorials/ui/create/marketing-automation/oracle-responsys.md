---
keywords: Experience Platform;inicio;temas populares;orígenes;conectores;oracle;
title: (Beta) Crear una conexión de origen de Responsys de Oracle mediante la IU de Platform
description: Obtenga información sobre cómo conectar Adobe Experience Platform a Oracle Responsys mediante la IU de Platform.
hide: true
hidefromtoc: true
exl-id: 9ec5e1c2-3d9e-4729-be81-89a85d5ea782
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---

# (Beta) Cree una [!DNL Oracle Responsys] conexión de origen mediante la IU de Platform

>[!NOTE]
>
>El [!DNL Oracle Responsys] el origen está en versión beta. Consulte la [Resumen de orígenes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores etiquetados como beta.

Este tutorial le proporciona los pasos para crear una [[!DNL Oracle Responsys]](../../../../connectors/marketing-automation/oracle-responsys.md) conexión de origen mediante la interfaz de usuario de Adobe Experience Platform.

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Platform:

* [Fuentes](../../../../home.md): Platform permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Si ya tiene un [!DNL Oracle Responsys] cuenta en Platform, puede omitir el resto de este documento y continuar con el tutorial sobre [creación de un flujo de datos para llevar los datos de automatización de marketing a Platform](../../dataflow/marketing-automation.md).

### Recopilar credenciales necesarias

Para poder conectarse [!DNL Oracle Responsys] En Platform, debe proporcionar valores para las siguientes propiedades de autenticación:

| Credencial | Descripción |
| --- | --- |
| Extremo | La URL del extremo de autenticación REST de su [!DNL Oracle Responsys] ejemplo. |
| ID del cliente | El ID de cliente de su [!DNL Oracle Responsys] ejemplo. |
| Secreto de cliente | El secreto de cliente de su [!DNL Oracle Responsys] ejemplo. |

Para obtener más información sobre las credenciales de autenticación de [!DNL Oracle Responsys], consulte la [[!DNL Oracle Responsys] guía de autenticación](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL Oracle Responsys] a Platform.

## Conecte su [!DNL Oracle Responsys] account

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. El [!UICONTROL Catálogo] La pantalla muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el [!UICONTROL Automatización de marketing] categoría, seleccionar **[!UICONTROL Oracle Responsys]**, y luego seleccione **[!UICONTROL Añadir datos]**.

![El catálogo de fuentes de Adobe Experience Platform con el Oracle de fuente Responsys resaltado.](../../../../images/tutorials/create/oracle-responsys/catalog.png)

El **[!UICONTROL Conectar la cuenta de Responsys de Oracle]** página. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para utilizar una cuenta existente, seleccione la [!DNL Oracle Responsys] cuenta con la que desea crear un nuevo flujo de datos y seleccione **[!UICONTROL Siguiente]** para continuar.

![La pantalla de autenticación de cuenta existente para Responsys de Oracle.](../../../../images/tutorials/create/oracle-responsys/existing.png)

### Nueva cuenta

Para crear una nueva cuenta, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre, una descripción opcional y los valores adecuados para su [!DNL Oracle Responsys] credenciales. Cuando termine, seleccione **[!UICONTROL Conectar con el origen]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![La nueva pantalla de autenticación de cuenta para Responsys de Oracle.](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Pasos siguientes

Al seguir este tutorial, ha autenticado y creado una conexión de origen entre sus [!DNL Oracle Responsys] y Platform. Ahora puede continuar con el siguiente tutorial y [crear un flujo de datos para llevar los datos de automatización de marketing a Platform](../../dataflow/marketing-automation.md).
