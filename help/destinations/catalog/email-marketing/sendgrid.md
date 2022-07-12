---
keywords: correo electrónico;correo electrónico;destinos de correo electrónico;cuadrícula de envío;destino de cuadrícula de envío
title: Conexión SendGrid
description: El destino SendGrid le permite exportar los datos de origen y activarlos en SendGrid según sus necesidades comerciales.
exl-id: 6f22746f-2043-4a20-b8a6-097d721f2fe7
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '1548'
ht-degree: 2%

---

# [!DNL SendGrid] connection

## Información general {#overview}

[SendGrid](https://www.sendgrid.com) es una plataforma de comunicación popular para clientes que envía correos electrónicos de marketing y transaccionales.

Esta [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) aprovecha el [[!DNL SendGrid Marketing Contacts API]](https://api.sendgrid.com/v3/marketing/contacts), que le permite exportar sus perfiles de correo electrónico de origen y activarlos en un nuevo segmento de SendGrid para sus necesidades comerciales.

SendGrid utiliza tokens de portador de API como mecanismo de autenticación para comunicarse con la API de SendGrid.

## Requisitos previos {#prerequisites}

Los siguientes elementos son necesarios antes de empezar a configurar el destino.

1. Debe tener una cuenta de SendGrid.
   * Ir a SendGrid [signup](https://signup.sendgrid.com/) para registrar y crear una cuenta de SendGrid, si todavía no la tiene.
1. Después de iniciar sesión en el portal de SendGrid, también debe generar un token de API.
1. Vaya al sitio web de SendGrid y acceda al **[!DNL Settings]** > **[!DNL API Keys]** página. También puede consultar la [Documentación de SendGrid](https://app.sendgrid.com/settings/api_keys) para acceder a la sección correspondiente de la aplicación SendGrid.
1. Finalmente, seleccione la **[!DNL Create API Key]** botón.
   * Consulte la [Documentación de SendGrid](https://docs.sendgrid.com/ui/account-and-settings/api-keys#creating-an-api-key), si necesita instrucciones sobre qué acciones realizar.
   * Si desea generar la clave de API mediante programación, consulte la [Documentación de SendGrid](https://docs.sendgrid.com/api-reference/api-keys/create-api-keys).

![](../../assets/catalog/email-marketing/sendgrid/01-api-key.jpg)

Antes de activar los datos en el destino de SendGrid, debe tener una [esquema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=es), [conjunto de datos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)y [segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) creado en [!DNL Experience Platform]. Consulte también la [límites](#limits) más abajo en esta página.

>[!IMPORTANT]
>
>* La API SendGrid utilizada para crear la lista de correo a partir de perfiles de correo electrónico requiere que se proporcionen direcciones de correo electrónico únicas dentro de cada perfil. Esto es independientemente de si se utiliza como valor para *email* o *correo electrónico alternativo*. Dado que la conexión SendGrid admite asignaciones para valores de correo electrónico y de correo electrónico alternativo, asegúrese de que todas las direcciones de correo electrónico utilizadas sean únicas dentro de cada perfil del *Conjunto de datos*. De lo contrario, cuando los perfiles de correo electrónico se envían a SendGrid, el resultado es un error y ese perfil de correo electrónico no estará presente en la exportación de datos.
>
>* Actualmente, no hay ninguna funcionalidad para eliminar perfiles de SendGrid cuando se eliminan de segmentos en el Experience Platform.


## Identidades compatibles {#supported-identities}

SendGrid admite la activación de identidades descritas en la siguiente tabla. Más información sobre [identidades](/help/identity-service/namespaces.md).

| Identidad de Target | Descripción | Consideraciones |
|---|---|---|
| email | Correo electrónico Dirección | Tenga en cuenta que tanto el texto sin formato como las direcciones de correo electrónico con hash SHA256 son compatibles con [!DNL Adobe Experience Platform]. Si el campo de origen de Experience Platform contiene atributos sin hash, marque la casilla de verificación **[!UICONTROL Aplicar transformación]** para [!DNL Platform] hash automático de los datos al activarlos.<br/><br/> Tenga en cuenta que **SendGrid** no admite direcciones de correo electrónico con hash, por lo que solo se envían al destino los datos de texto sin formato sin transformación. |

{style=&quot;table-layout:auto&quot;}

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Está exportando todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se elige en la pantalla seleccionar atributos de perfil del [flujo de trabajo de activación de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de flujo continuo son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como un perfil se actualiza en el Experience Platform en función de la evaluación de segmentos, el conector envía la actualización descendente a la plataforma de destino. Más información sobre [destinos de flujo continuo](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino SendGrid, estos son ejemplos de casos de uso que [!DNL Experience Platform] los clientes de pueden resolver utilizando este destino.

### Crear una lista de marketing para varias actividades de marketing

Los equipos de marketing que utilizan SendGrid pueden crear una lista de correo dentro de SendGrid y rellenarla con direcciones de correo electrónico. La lista de correo creada en SendGrid puede utilizarse posteriormente para varias actividades de marketing.

## Conectarse al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos que aparecen en las dos secciones siguientes.

### Autenticar en destino {#authenticate}

1. Dentro de [!DNL Adobe Experience Platform] consola, vaya a **Destinos**.

1. Seleccione el **Catálogo** y busque *SendGrid*. A continuación, seleccione **Configuración**. Después de establecer una conexión con el destino, la etiqueta de la interfaz de usuario cambia a **Activar segmentos**.
   ![](../../assets/catalog/email-marketing/sendgrid/02-catalog.jpg)

1. Se le muestra un asistente que le ayuda a configurar el destino de SendGrid. Cree el nuevo destino seleccionando **Configurar nuevo destino**.
   ![](../../assets/catalog/email-marketing/sendgrid/03.jpg)

1. Seleccione el **Nueva cuenta** y rellene la **Token del portador** valor. Este valor es SendGrid *Clave de API* mencionado anteriormente en la sección [sección de requisitos previos](#prerequisites).
   ![](../../assets/catalog/email-marketing/sendgrid/04.jpg)

1. Select **Conectarse al destino**. Si el objeto SendGrid *Clave de API* la interfaz de usuario que ha proporcionado es válida, muestra una **Conectado** con una marca de verificación verde, puede continuar con el siguiente paso para rellenar campos de información adicionales.

![](../../assets/catalog/email-marketing/sendgrid/05.jpg)

### Rellenar detalles de destino {#destination-details}

While [configuración](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) Para este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: El nombre por el que reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción opcional que le ayudará a identificar este destino en el futuro.

![](../../assets/catalog/email-marketing/sendgrid/06.jpg)

### Habilitar alertas {#enable-alerts}

Puede activar las alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista para suscribirse y recibir notificaciones sobre el estado de su flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Lectura [Activar perfiles y segmentos en destinos de exportación de segmentos de flujo continuo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

Consulte las siguientes imágenes para obtener detalles específicos sobre este destino.

1. Seleccione uno o varios segmentos para exportar a SendGrid.
   ![](../../assets/catalog/email-marketing/sendgrid/11.jpg)

1. En el **[!UICONTROL Asignación]** paso, después de seleccionar **[!UICONTROL Añadir nueva asignación]**, se muestra la página de asignación para asignar los campos XDM de origen a los campos de destino de la API SendGrid. Las imágenes siguientes muestran cómo asignar áreas de nombres de identidad entre Experience Platform y SendGrid. Asegúrese de que la variable **[!UICONTROL Campo de origen]** *Correo electrónico* debe asignarse a la variable **[!UICONTROL Campo de destino]** *external_id* como se muestra a continuación.
   ![](../../assets/catalog/email-marketing/sendgrid/13.jpg)

   ![](../../assets/catalog/email-marketing/sendgrid/14.jpg)
   ![](../../assets/catalog/email-marketing/sendgrid/15.jpg)
   ![](../../assets/catalog/email-marketing/sendgrid/16.jpg)

1. Del mismo modo, asigne el [!DNL Adobe Experience Platform] atributos que desea exportar al destino de SendGrid.
   ![](../../assets/catalog/email-marketing/sendgrid/17.jpg)

   ![](../../assets/catalog/email-marketing/sendgrid/18.jpg)

1. Después de completar las asignaciones, seleccione **[!UICONTROL Siguiente]** para pasar a la pantalla de revisión.
   ![](../../assets/catalog/email-marketing/sendgrid/22.png)

1. Select **[!UICONTROL Finalizar]** para completar la configuración.
   ![](../../assets/catalog/email-marketing/sendgrid/23.jpg)

La lista completa de asignaciones de atributos compatibles que se pueden configurar para la variable [Contactos de marketing de SendGrid > Agregar o actualizar la API de contacto](https://docs.sendgrid.com/api-reference/contacts/add-or-update-a-contact) a continuación.

| Campo de origen | Campo de destino | Tipo | Descripción | Límites |
|---|---|---|---|---|
| xdm:<br/> homeAddress.street1 | xdm:<br/> address_line_1 | Cadena | La primera línea de la dirección. | Longitud máxima:<br/> 100 caracteres |
| xdm:<br/> homeAddress.street2 | xdm:<br/> address_line_2 | Cadena | Una segunda línea opcional para la dirección. | Longitud máxima:<br/> 100 caracteres |
| xdm:<br/> _extconndev.alternative_emails | xdm:<br/> alternative_emails | Matriz de cadena | Correos electrónicos adicionales asociados al contacto. | <ul><li>Máx.: 5 elementos</li><li>Mínimo: 0 artículos</li></ul> |
| xdm:<br/> homeAddress.city | xdm:<br/> city | Cadena | La ciudad del contacto. | Longitud máxima:<br/> 60 caracteres |
| xdm:<br/> homeAddress.country | xdm:<br/> country | Cadena | El país del contacto. Puede ser un nombre completo o una abreviatura. | Longitud máxima:<br/> 50 caracteres |
| identityMap:<br/> Correo electrónico | Identidad:<br/> external_id | Cadena | El correo electrónico principal del contacto. Debe ser un correo electrónico válido. | Longitud máxima:<br/> 254 caracteres |
| xdm:<br/> person.name.firstName | xdm:<br/> first_name | Cadena | El nombre del contacto | Longitud máxima:<br/> 50 caracteres |
| xdm:<br/> person.name.lastName | xdm:<br/> last_name | Cadena | El apellido del contacto | Longitud máxima:<br/> 50 caracteres |
| xdm:<br/> homeAddress.postalCode | xdm:<br/> postal_code | Cadena | El código postal del contacto. |  |
| xdm:<br/> homeAddress.stateProvincia | xdm:<br/> state_provincia_región | Cadena | Estado, provincia o región del contacto. | Longitud máxima:<br/> 50 caracteres |

## Validación de la exportación de datos dentro de SendGrid {#validate}

Para validar que ha configurado correctamente el destino, siga los pasos a continuación:

1. Select **[!UICONTROL Destinos]** > **[!UICONTROL Examinar]** para navegar a la lista de destinos.
   ![](../../assets/catalog/email-marketing/sendgrid/25.jpg)

1. Seleccione el destino y valide que el estado es **[!UICONTROL enabled]**.
   ![](../../assets/catalog/email-marketing/sendgrid/26.jpg)

1. Cambie a la **[!DNL Activation data]** y, a continuación, seleccione un nombre de segmento.
   ![](../../assets/catalog/email-marketing/sendgrid/27.jpg)

1. Monitorice el resumen del segmento y compruebe el recuento de perfiles correspondientes al recuento creado dentro del conjunto de datos.
   ![](../../assets/catalog/email-marketing/sendgrid/28.jpg)

1. La variable [Listas de marketing de SendGrid > Crear API de lista](https://docs.sendgrid.com/api-reference/lists/create-list) se utiliza para crear listas de contactos únicas dentro de SendGrid uniendo el valor de *list_name* y la marca de tiempo de la exportación de datos. Vaya al sitio SendGrid y compruebe si se crea la nueva lista de contactos que se ajusta al patrón de nombres.
   ![](../../assets/catalog/email-marketing/sendgrid/29.jpg)

   ![](../../assets/catalog/email-marketing/sendgrid/30.jpg)

1. Seleccione la lista de contactos recién creada y compruebe si el nuevo registro de correo electrónico del conjunto de datos que ha creado se está rellenando en la nueva lista de contactos.

1. Además, compruebe también un par de correos electrónicos para validar si la asignación de campos es correcta.
   ![](../../assets/catalog/email-marketing/sendgrid/31.jpg)

   ![](../../assets/catalog/email-marketing/sendgrid/32.jpg)

## Uso y gobernanza de los datos {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] exige el control de datos; consulte [Información general sobre la administración de datos](/help/data-governance/home.md).

## Recursos adicionales {#additional-resources}

Este destino de SendGrid aprovecha las siguientes API:
* [Listas de marketing de SendGrid > Crear API de lista](https://docs.sendgrid.com/api-reference/lists/create-list)
* [Contactos de marketing de SendGrid > Agregar o actualizar la API de contacto](https://docs.sendgrid.com/api-reference/contacts/add-or-update-a-contact)

### Límites {#limits}

* La variable [Contactos de marketing de SendGrid > Agregar o actualizar la API de contacto](https://api.sendgrid.com/v3/marketing/contacts) puede aceptar 30 000 contactos o 6 MB de datos, lo que sea menor.
