---
keywords: Experience Platform;inicio;temas populares;Zoho CRM;zoho crm;Zoho;zoho
solution: Experience Platform
title: Crear una conexión de origen de Zoho CRM en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen Zoho CRM mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: c648fc3e-beea-4030-8d36-dd8a7e2c281e
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 1%

---

# Cree un [!DNL Zoho CRM] conexión de origen en la interfaz de usuario

Los conectores de origen en Adobe Experience Platform permiten la ingesta de datos CRM de origen externo de forma programada. Este tutorial proporciona los pasos para crear un [!DNL Zoho CRM] conector de origen utilizando [!DNL Platform] interfaz de usuario.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición del esquema](../../../../../xdm/schema/composition.md): Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una [!DNL Zoho CRM] cuenta, puede omitir el resto de este documento y continuar con el tutorial en [configuración de un flujo de datos](../../dataflow/crm.md).

### Recopilar las credenciales necesarias

Para conectarse [!DNL Zoho CRM] en Platform, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| --- | --- |
| Punto final | El punto final de la variable [!DNL Zoho CRM] servidor al que está realizando la solicitud. |
| Dirección URL de cuentas | La dirección URL de la cuenta se usa para generar los tokens de acceso y actualización. La dirección URL debe ser específica del dominio. |
| ID del cliente | El ID de cliente que corresponde a su [!DNL Zoho CRM] cuenta de usuario. |
| Secreto del cliente | El secreto de cliente que corresponde a su [!DNL Zoho CRM] cuenta de usuario. |
| Token de acceso | El token de acceso autoriza su acceso seguro y temporal a su [!DNL Zoho CRM] cuenta. |
| Actualizar token | Un token de actualización es un token que se utiliza para generar un nuevo token de acceso, una vez que el token de acceso ha caducado. |

Para obtener más información sobre estas credenciales, consulte la documentación de [[!DNL Zoho CRM] autenticación](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Conecte su [!DNL Zoho CRM] account

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular sus [!DNL Zoho CRM] cuenta para [!DNL Platform].

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable [!UICONTROL Catálogo] muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En el [!UICONTROL CRM] categoría, seleccione **[!UICONTROL Zoho CRM]** y, a continuación, seleccione **[!UICONTROL Añadir datos]**.

![catálogo](../../../../images/tutorials/create/zoho/catalog.png)

La variable **[!UICONTROL Conectar cuenta de Zoho CRM]** se abre. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para usar una cuenta existente, seleccione la opción [!DNL Zoho CRM] cuenta con la que desee crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/zoho/existing.png)

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre, una descripción opcional y su [!DNL Zoho CRM] credenciales. Cuando termine, seleccione **[!UICONTROL Conectar a origen]** y, a continuación, permita que la nueva conexión se establezca durante algún tiempo.

>[!TIP]
>
>El dominio URL de su cuenta debe corresponder a su ubicación de dominio apropiada. A continuación se muestran los distintos dominios y las direcciones URL de sus cuentas correspondientes:<ul><li>Estados Unidos: https://accounts.zoho.com</li><li>Australia: https://accounts.zoho.com.au</li><li>Europa: https://accounts.zoho.eu</li><li>India: https://accounts.zoho.in</li><li>China: https://accounts.zoho.com.cn</li></ul>

![new](../../../../images/tutorials/create/zoho/new.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL Zoho CRM] cuenta. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en Platform](../../dataflow/crm.md).
