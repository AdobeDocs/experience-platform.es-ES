---
title: Crear una conexión de origen de Azure Event Hubs en la interfaz de usuario
description: Obtenga información sobre cómo crear una conexión de origen de Azure Event Hubs mediante la interfaz de usuario de Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 7e67e213-8ccb-4fa5-b09f-ae77aba8614c
source-git-commit: 22f3b76c02e641d2f4c0dd7c0e5cc93038782836
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 1%

---

# Crear un [!DNL Azure Event Hubs] conexión de origen en la interfaz de usuario

>[!IMPORTANT]
>
>El [!DNL Azure Event Hubs] La fuente de está disponible en el catálogo de fuentes de para los usuarios que han adquirido Real-time Customer Data Platform Ultimate.

Lea este tutorial para aprender a crear un [!DNL Azure Event Hubs] mediante la interfaz de usuario de Adobe Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene un válido [!DNL Event Hubs] conexión, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/streaming/cloud-storage-streaming.md).

### Recopilar credenciales necesarias

Para autenticar su [!DNL Event Hubs] conector de origen, debe proporcionar valores para las siguientes propiedades de conexión:

>[!BEGINTABS]

>[!TAB Autenticación estándar]

| Credencial | Descripción |
| --- | --- |
| Nombre de clave SAS | Nombre de la regla de autorización, que también se conoce como nombre de clave SAS. |
| Clave SAS | La clave principal del [!DNL Event Hubs] namespace. El `sasPolicy` que el `sasKey` corresponde a debe tener `manage` derechos configurados para el [!DNL Event Hubs] lista que se va a rellenar. |
| Área de nombres | El área de nombres del [!DNL Event Hubs] está accediendo a. Un [!DNL Event Hubs] el espacio de nombres proporciona un contenedor de ámbito único, en el que puede crear uno o más [!DNL Event Hubs]. |

>[!TAB Autenticación SAS]

| Credencial | Descripción |
| --- | --- |
| Nombre de clave SAS | Nombre de la regla de autorización, que también se conoce como nombre de clave SAS. |
| Clave SAS | La clave principal del [!DNL Event Hubs] namespace. El `sasPolicy` que el `sasKey` corresponde a debe tener `manage` derechos configurados para el [!DNL Event Hubs] lista que se va a rellenar. |
| Área de nombres | El área de nombres del [!DNL Event Hubs] está accediendo a. Un [!DNL Event Hubs] el espacio de nombres proporciona un contenedor de ámbito único, en el que puede crear uno o más [!DNL Event Hubs]. |
| Nombre del centro de eventos | El nombre de su [!DNL Event Hubs] origen. |

Para obtener más información sobre la autenticación de firmas de acceso compartido (SAS) para [!DNL Event Hubs], lea la [[!DNL Azure] guía sobre el uso de SAS](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

>[!TAB Autenticación de Active Directory de Azure Event Hub]

| Credencial | Descripción |
| --- | --- |
| ID de inquilino | El ID de inquilino desde el que desea solicitar permiso. Su ID de inquilino puede tener el formato de GUID o de nombre descriptivo. **Nota**: el ID de inquilino se denomina &quot;ID de directorio&quot; en la variable [!DNL Microsoft Azure] interfaz. |
| ID de cliente | El ID de aplicación asignado a su aplicación. Puede recuperar este ID desde el [!DNL Microsoft Entra ID] portal donde registró su [!DNL Azure Active Directory]. |
| Valor secreto de cliente | El secreto de cliente que se utiliza junto con el ID de cliente para autenticar la aplicación. Puede recuperar el secreto de cliente desde el [!DNL Microsoft Entra ID] portal donde registró su [!DNL Azure Active Directory]. |
| Área de nombres | El área de nombres del [!DNL Event Hubs] está accediendo a. Un [!DNL Event Hubs] el espacio de nombres proporciona un contenedor de ámbito único, en el que puede crear uno o más [!DNL Event Hubs]. |

Para obtener más información sobre [!DNL Azure Active Directory], lea la [Guía de Azure sobre el uso de Microsoft Entra ID](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application).

>[!TAB Auth de Azure Active Directory con ámbito de Event Hub]

| Credencial | Descripción |
| --- | --- |
| ID de inquilino | El ID de inquilino desde el que desea solicitar permiso. Su ID de inquilino puede tener el formato de GUID o de nombre descriptivo. **Nota**: el ID de inquilino se denomina &quot;ID de directorio&quot; en la variable [!DNL Microsoft Azure] interfaz. |
| ID de cliente | El ID de aplicación asignado a su aplicación. Puede recuperar este ID desde el [!DNL Microsoft Entra ID] portal donde registró su [!DNL Azure Active Directory]. |
| Valor secreto de cliente | El secreto de cliente que se utiliza junto con el ID de cliente para autenticar la aplicación. Puede recuperar el secreto de cliente desde el [!DNL Microsoft Entra ID] portal donde registró su [!DNL Azure Active Directory]. |
| Área de nombres | El área de nombres del [!DNL Event Hubs] está accediendo a. Un [!DNL Event Hubs] el espacio de nombres proporciona un contenedor de ámbito único, en el que puede crear uno o más [!DNL Event Hubs]. |
| Nombre del centro de eventos | El nombre de su [!DNL Event Hubs] origen. |

Para obtener más información sobre [!DNL Azure Active Directory], lea la [Guía de Azure sobre el uso de Microsoft Entra ID](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application).

>[!ENDTABS]

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL Event Hubs] cuenta para el Experience Platform.

## Conecte su [!DNL Event Hubs] account

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. El [!UICONTROL Catálogo] La pantalla de muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el [!UICONTROL Almacenamiento en la nube] categoría, seleccionar **[!UICONTROL Azure Event Hubs]**, y luego seleccione **[!UICONTROL Añadir datos]**.

![El catálogo de fuentes con Azure Event Hubs seleccionado.](../../../../images/tutorials/create/eventhub/catalog.png)

El **[!UICONTROL Conectar con Azure Event Hubs]** aparece el cuadro de diálogo. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para utilizar una cuenta existente, seleccione la [!DNL Event Hubs] cuenta que desee utilizar y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![Una lista de cuentas de origen de Azure Event Hubs.](../../../../images/tutorials/create/eventhub/existing.png)

### Nueva cuenta

>[!TIP]
>
>Una vez creado, no se puede cambiar el tipo de autenticación de una [!DNL Event Hubs] conexión base. Para cambiar el tipo de autenticación, debe crear una nueva conexión base.

Para crear una nueva cuenta, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre y una descripción opcional para la nueva [!DNL Event Hubs] cuenta.

![La nueva interfaz de creación de cuentas para Azure Event Hubs.](../../../../images/tutorials/create/eventhub/new.png)

>[!BEGINTABS]

>[!TAB Autenticación estándar]

Para crear un [!DNL Event Hubs] cuenta con autenticación estándar, utilice el [!UICONTROL Autenticación de cuenta] y, a continuación, seleccione **[!UICONTROL Autenticación estándar]**. A continuación, proporcione valores para su [!UICONTROL Nombre de clave SAS], [!UICONTROL Clave SAS], y [!UICONTROL Área de nombres].

Una vez que haya introducido las credenciales de autenticación, seleccione **[!UICONTROL Conectar con el origen]**.

![Interfaz de autenticación estándar para Azure Event Hubs.](../../../../images/tutorials/create/eventhub/standard.png)

>[!TAB Autenticación SAS]

Para crear un [!DNL Event Hubs] cuenta con autenticación SAS, utilice la [!UICONTROL Autenticación de cuenta] y, a continuación, seleccione **[!UICONTROL Autenticación SAS]**. A continuación, proporcione valores para su [!UICONTROL Nombre de clave SAS], [!UICONTROL Clave SAS], [!UICONTROL Área de nombres], y [!UICONTROL Nombre de Event Hubs].

Una vez que haya introducido las credenciales de autenticación, seleccione **[!UICONTROL Conectar con el origen]**.

![Interfaz de autenticación SAS para Azure Event Hubs.](../../../../images/tutorials/create/eventhub/sas.png)

>[!TAB Autenticación de Active Directory de Azure Event Hub]

Para crear un [!DNL Event Hubs] cuenta con la autenticación de Azure Active Directory de Event Hub, use [!UICONTROL Autenticación de cuenta] y, a continuación, seleccione **[!UICONTROL Azure Active Directory Event Hub]**. A continuación, proporcione valores para su [!UICONTROL ID de inquilino], [!UICONTROL ID de cliente], [!UICONTROL Valor secreto de cliente], y [!UICONTROL Área de nombres].

![Azure Event Hub Azure Active Directory Authentication](../../../../images/tutorials/create/eventhub/active-directory.png)

>[!TAB Auth de Azure Active Directory con ámbito de Event Hub]

Para crear un [!DNL Event Hubs] cuenta con ámbito de Event Hub Autenticación de Azure Active Directory, use [!UICONTROL Autenticación de cuenta] y, a continuación, seleccione **[!UICONTROL Ámbito del concentrador de eventos de Azure Active Directory]**. A continuación, proporcione valores para su [!UICONTROL ID de inquilino], [!UICONTROL ID de cliente], [!UICONTROL Valor secreto de cliente], [!UICONTROL Área de nombres], y [!UICONTROL Nombre del hub de eventos].

![Azure Event Hub con ámbito de autenticación de Azure Activity Directory](../../../../images/tutorials/create/eventhub/scoped.png)

>[!ENDTABS]


## Pasos siguientes

Al seguir este tutorial, ha conectado su [!DNL Event Hubs] cuenta para el Experience Platform. Ahora puede continuar con el siguiente tutorial y [configure un flujo de datos para traer datos de su almacenamiento en la nube a Experience Platform](../../dataflow/streaming/cloud-storage-streaming.md).
