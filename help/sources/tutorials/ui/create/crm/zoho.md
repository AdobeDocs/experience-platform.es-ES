---
keywords: Experience Platform;inicio;temas populares;Zoho CRM;zoho crm;Zoho;zoho
solution: Experience Platform
title: Crear una conexión de origen Zoho CRM en la interfaz de usuario
type: Tutorial
description: Aprenda a crear una conexión de origen Zoho CRM mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: c648fc3e-beea-4030-8d36-dd8a7e2c281e
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 1%

---

# Crear un [!DNL Zoho CRM] conexión de origen en la interfaz de usuario

Los conectores de origen en Adobe Experience Platform permiten introducir datos CRM de origen externo de forma programada. Este tutorial proporciona los pasos para crear una [!DNL Zoho CRM] conector de origen mediante [!DNL Platform] interfaz de usuario.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene un válido [!DNL Zoho CRM] cuenta de, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/crm.md).

### Recopilar credenciales necesarias

Para poder conectarse [!DNL Zoho CRM] En Platform, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| --- | --- |
| Extremo | El punto final del [!DNL Zoho CRM] servidor al que está realizando la solicitud. |
| URL de cuentas | La dirección URL de cuentas se utiliza para generar los tokens de acceso y actualización. La dirección URL debe ser específica del dominio. |
| ID del cliente | El ID de cliente que corresponde con su [!DNL Zoho CRM] cuenta de usuario. |
| Secreto de cliente | El secreto de cliente que corresponde con su [!DNL Zoho CRM] cuenta de usuario. |
| Token de acceso | El token de acceso autoriza su acceso seguro y temporal a su [!DNL Zoho CRM] cuenta. |
| Actualizar token | Un token de actualización es un token que se utiliza para generar un nuevo token de acceso, una vez que el token de acceso ha caducado. |

Para obtener más información sobre estas credenciales, consulte la documentación sobre [[!DNL Zoho CRM] authentication](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Conecte su [!DNL Zoho CRM] account

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL Zoho CRM] cuenta a [!DNL Platform].

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. El [!UICONTROL Catálogo] La pantalla muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el [!UICONTROL CRM] categoría, seleccionar **[!UICONTROL Zoho CRM]**, y luego seleccione **[!UICONTROL Añadir datos]**.

![catalogar](../../../../images/tutorials/create/zoho/catalog.png)

El **[!UICONTROL Conectar la cuenta de Zoho CRM]** página. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para utilizar una cuenta existente, seleccione la [!DNL Zoho CRM] cuenta con la que desea crear un nuevo flujo de datos y seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/zoho/existing.png)

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre, una descripción opcional y su [!DNL Zoho CRM] credenciales. Cuando termine, seleccione **[!UICONTROL Conectar con el origen]** y, a continuación, espere un poco para que se establezca la nueva conexión.

>[!TIP]
>
>El dominio URL de las cuentas debe corresponder con la ubicación de dominio adecuada. A continuación se indican los distintos dominios y las direcciones URL de sus cuentas correspondientes:<ul><li>Estados Unidos: https://accounts.zoho.com</li><li>Australia: https://accounts.zoho.com.au</li><li>Europa: https://accounts.zoho.eu</li><li>India: https://accounts.zoho.in</li><li>China: https://accounts.zoho.com.cn</li></ul>

![nuevo](../../../../images/tutorials/create/zoho/new.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL Zoho CRM] cuenta. Ahora puede continuar con el siguiente tutorial y [configuración de un flujo de datos para introducir datos en Platform](../../dataflow/crm.md).
