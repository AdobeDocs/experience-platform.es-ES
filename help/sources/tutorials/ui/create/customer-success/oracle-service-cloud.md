---
keywords: Experience Platform;inicio;temas populares;Nube de servicios de Oracle;Nube de servicios de oracle
title: Creación de una conexión de Oracle Service Cloud Source en la IU
description: Obtenga información sobre cómo crear una conexión de origen de Cloud Oracle Service mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: e5869c09-b61e-4d23-a594-5a07769da3c4
source-git-commit: 474b81aa8caf58013f8ea7cff9ad59d92466aac8
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 2%

---

# Crear una conexión de origen de nube de Oracle Service en la interfaz de usuario

>[!WARNING]
>
>El origen [!DNL Oracle Service Cloud] quedará obsoleto a finales de mayo de 2025.

Este tutorial proporciona los pasos para crear una conexión de origen de Cloud Oracle Service mediante la interfaz de usuario de Adobe Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una conexión de origen de Oracle Service Cloud válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/customer-success.md)

### Recopilar credenciales necesarias

Para acceder a su cuenta de Oracle Service Cloud en [!DNL Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| Host | La URL de host de la instancia de Oracle Service Cloud. |
| Nombre de usuario | El nombre de usuario de su cuenta de usuario de Oracle Service Cloud. |
| Contraseña | La contraseña de su cuenta de Oracle Service Cloud. |

Para obtener más información sobre cómo autenticar su cuenta de Oracle Service Cloud, consulte la [[!DNL Oracle] guía de autenticación](https://docs.oracle.com/en/cloud/saas/b2c-service/20c/cxska/OKCS_Authenticate_and_Authorize.html).

## Conecte su cuenta de Oracle Service Cloud

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al área de trabajo [!UICONTROL Sources]. La pantalla [!UICONTROL Catálogo] muestra una variedad de orígenes que se pueden usar para crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar en la barra de búsqueda.

En la categoría [!UICONTROL Éxito del cliente], seleccione **[!UICONTROL Oracle Service Cloud]** y, a continuación, seleccione **[!UICONTROL Agregar datos]**.

![Se resaltó el catálogo de orígenes con la fuente de nube de Oracle Service.](../../../../images/tutorials/create/oracle-service-cloud/catalog.png)

Aparecerá la página **[!UICONTROL Conectarse a la nube del servicio de Oracle]**. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para conectar una cuenta existente, selecciona la cuenta de Oracle Service Cloud con la que deseas conectarte y, a continuación, selecciona **[!UICONTROL Siguiente]** para continuar.

![Interfaz de cuenta existente.](../../../../images/tutorials/create/oracle-service-cloud/existing.png)

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y las credenciales de Cloud Service de Oracle. Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y deje pasar un tiempo para que se establezca la nueva conexión.

![Interfaz de la nueva cuenta con valores de marcador de posición para.](../../../../images/tutorials/create/oracle-service-cloud/new.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de Oracle Service Cloud. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para llevar los datos de éxito de los clientes a la plataforma](../../dataflow/crm.md).
