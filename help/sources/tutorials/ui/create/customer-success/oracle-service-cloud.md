---
keywords: Experience Platform;inicio;temas populares;nube de servicio de Oracle;nube de servicio de oracle
title: Creación de una conexión de origen de nube de Oracle Service en la interfaz de usuario
description: Obtenga información sobre cómo crear una conexión de origen de nube de Oracle Service mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: e5869c09-b61e-4d23-a594-5a07769da3c4
source-git-commit: 1695b7d638feb648d5cd7af07879f3ed13f938eb
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---

# Creación de una conexión de origen de nube de Oracle Service en la interfaz de usuario

Este tutorial proporciona los pasos para crear una conexión de origen de la nube de Oracle Service mediante la interfaz de usuario de Adobe Experience Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición del esquema](../../../../../xdm/schema/composition.md): Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión de origen de Oracle Service Cloud válida, puede omitir el resto de este documento y continuar con el tutorial en [configuración de un flujo de datos](../../dataflow/customer-success.md)

### Recopilar las credenciales necesarias

Para acceder a su cuenta de Oracle Service Cloud en [!DNL Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| Host | La URL de host de la instancia de nube de servicio de Oracle. |
| Nombre de usuario | El nombre de usuario de su cuenta de usuario de Oracle Service Cloud. |
| Una contraseña | La contraseña de su cuenta de Oracle Service Cloud. |

Para obtener más información sobre la autenticación de su cuenta de Oracle Service Cloud, consulte la [[!DNL Oracle] guía de autenticación](https://docs.oracle.com/en/cloud/saas/b2c-service/20c/cxska/OKCS_Authenticate_and_Authorize.html).

## Conecte su cuenta de Oracle Service Cloud

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** desde el panel de navegación izquierdo para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable [!UICONTROL Catálogo] muestra una variedad de fuentes que pueden utilizarse para crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la barra de búsqueda.

En el [!UICONTROL Éxito del cliente] categoría, seleccione **[!UICONTROL Nube de servicio de oracle]** y, a continuación, seleccione **[!UICONTROL Añadir datos]**.

![El catálogo de fuentes con el origen de nube de Oracle Service resaltado.](../../../../images/tutorials/create/oracle-service-cloud/catalog.png)

La variable **[!UICONTROL Conectarse a Oracle Service Cloud]** se abre. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de Oracle Service Cloud con la que desee conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![Interfaz de cuenta existente.](../../../../images/tutorials/create/oracle-service-cloud/existing.png)

### Nueva cuenta

Si está utilizando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, indique un nombre, una descripción opcional y las credenciales de Oracle Service Cloud. Cuando termine, seleccione **[!UICONTROL Conectar a origen]** y, a continuación, permita que la nueva conexión se establezca durante algún tiempo.

![La nueva interfaz de cuenta con valores de marcador de posición para .](../../../../images/tutorials/create/oracle-service-cloud/new.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión con su cuenta de Oracle Service Cloud. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para incorporar los datos de éxito de los clientes a Platform](../../dataflow/crm.md).
