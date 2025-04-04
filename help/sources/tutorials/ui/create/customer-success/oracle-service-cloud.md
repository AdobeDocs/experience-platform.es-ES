---
keywords: Experience Platform;inicio;temas populares;Oracle Service Cloud;oracle service cloud
title: Creación de una conexión de Oracle Service Cloud Source en la interfaz de usuario
description: Obtenga información sobre cómo crear una conexión de origen de Oracle Service Cloud mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: e5869c09-b61e-4d23-a594-5a07769da3c4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 2%

---

# Crear una conexión de origen de Oracle Service Cloud en la interfaz de usuario

>[!WARNING]
>
>El origen [!DNL Oracle Service Cloud] quedará obsoleto a finales de junio de 2025.

Este tutorial proporciona los pasos para crear una conexión de origen de Oracle Service Cloud mediante la interfaz de usuario de Adobe Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una conexión de origen de Oracle Service Cloud válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/customer-success.md)

### Recopilar credenciales necesarias

Para acceder a su cuenta de Oracle Service Cloud en [!DNL Experience Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| Host | La URL de host de la instancia de Oracle Service Cloud. |
| Nombre de usuario | El nombre de usuario de la cuenta de usuario de Oracle Service Cloud. |
| Contraseña | La contraseña de su cuenta de Oracle Service Cloud. |

Para obtener más información sobre cómo autenticar su cuenta de Oracle Service Cloud, consulte la [[!DNL Oracle] guía de autenticación](https://docs.oracle.com/en/cloud/saas/b2c-service/20c/cxska/OKCS_Authenticate_and_Authorize.html).

## Conecte su cuenta de Oracle Service Cloud

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Fuentes]** en el panel de navegación izquierdo para acceder al área de trabajo [!UICONTROL Fuentes]. La pantalla [!UICONTROL Catálogo] muestra una variedad de orígenes que se pueden usar para crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar en la barra de búsqueda.

En la categoría [!UICONTROL Éxito del cliente], seleccione **[!UICONTROL Oracle Service Cloud]** y, a continuación, **[!UICONTROL Agregar datos]**.

![Se resaltó el catálogo de orígenes con el origen de Oracle Service Cloud.](../../../../images/tutorials/create/oracle-service-cloud/catalog.png)

Aparecerá la página **[!UICONTROL Conectarse a Oracle Service Cloud]**. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para conectar una cuenta existente, selecciona la cuenta de Oracle Service Cloud con la que deseas conectarte y, a continuación, selecciona **[!UICONTROL Siguiente]** para continuar.

![Interfaz de cuenta existente.](../../../../images/tutorials/create/oracle-service-cloud/existing.png)

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y las credenciales de Oracle Service Cloud. Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y deje pasar un tiempo para que se establezca la nueva conexión.

![Interfaz de la nueva cuenta con valores de marcador de posición para.](../../../../images/tutorials/create/oracle-service-cloud/new.png)

## Pasos siguientes

Con este tutorial ha establecido una conexión con su cuenta de Oracle Service Cloud. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para llevar los datos de éxito de los clientes a Experience Platform](../../dataflow/crm.md).
