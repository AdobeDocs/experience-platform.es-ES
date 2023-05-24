---
keywords: Experience Platform;inicio;temas populares;Nube de servicios de Oracle;Nube de servicios de oracle
title: Creación de una conexión de origen de nube de servicio de Oracle en la IU
description: Obtenga información sobre cómo crear una conexión de origen de Cloud Oracle Service mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: e5869c09-b61e-4d23-a594-5a07769da3c4
source-git-commit: 1695b7d638feb648d5cd7af07879f3ed13f938eb
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---

# Crear una conexión de origen de nube de Oracle Service en la interfaz de usuario

Este tutorial proporciona los pasos para crear una conexión de origen de Cloud Oracle Service mediante la interfaz de usuario de Adobe Experience Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una conexión de origen de Oracle Service Cloud válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/customer-success.md)

### Recopilar credenciales necesarias

Para acceder a su cuenta de Oracle Service Cloud en [!DNL Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| Host | La URL de host de la instancia de Oracle Service Cloud. |
| Nombre de usuario | El nombre de usuario de su cuenta de usuario de Oracle Service Cloud. |
| Una contraseña | La contraseña de su cuenta de Oracle Service Cloud. |

Para obtener más información sobre la autenticación de su cuenta de Oracle Service Cloud, consulte la [[!DNL Oracle] guía de autenticación](https://docs.oracle.com/en/cloud/saas/b2c-service/20c/cxska/OKCS_Authenticate_and_Authorize.html).

## Conecte su cuenta de Oracle Service Cloud

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. El [!UICONTROL Catálogo] La pantalla muestra una variedad de fuentes que pueden utilizarse para crear una cuenta de.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar en la barra de búsqueda.

En el [!UICONTROL Éxito del cliente] categoría, seleccionar **[!UICONTROL Oracle Service Cloud]** y luego seleccione **[!UICONTROL Añadir datos]**.

![El catálogo de fuentes con la fuente de Oracle Service Cloud resaltada.](../../../../images/tutorials/create/oracle-service-cloud/catalog.png)

El **[!UICONTROL Conectar con Oracle Service Cloud]** página. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de Oracle Service Cloud con la que desee conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![Interfaz de cuenta existente.](../../../../images/tutorials/create/oracle-service-cloud/existing.png)

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y las credenciales de Cloud Service de Oracle. Cuando termine, seleccione **[!UICONTROL Conectar con el origen]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![La nueva interfaz de cuenta con valores de marcador de posición para.](../../../../images/tutorials/create/oracle-service-cloud/new.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de Oracle Service Cloud. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para llevar los datos de éxito de los clientes a Platform](../../dataflow/crm.md).
