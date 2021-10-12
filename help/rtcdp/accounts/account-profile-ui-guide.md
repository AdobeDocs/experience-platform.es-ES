---
keywords: perfil rtcdp;perfiles rtcdp;identidades rtcdp;políticas de combinación rtcdp;perfil de cliente en tiempo real
title: Guía de la interfaz de usuario del perfil de cuenta
description: Mediante el uso de perfiles de cuenta, Real-time Customer Data Platform B2B Edition le permite unificar la información de la cuenta de múltiples fuentes. Esta guía proporciona detalles para interactuar con perfiles de cuenta en la interfaz de usuario de Adobe Experience Platform.
exl-id: a05e8b84-026e-4482-a288-aa25b441bd69
source-git-commit: 5bd2afcc594d96878ee51af2e9e99d74b764009e
workflow-type: tm+mt
source-wordcount: '1191'
ht-degree: 0%

---

# Guía de la interfaz de usuario del perfil de la cuenta

>[!IMPORTANT]
>
>Real-time Customer Data Platform B2B Edition está actualmente en versión beta. La documentación y la funcionalidad están sujetas a cambios.

>[!NOTE]
>
>Los perfiles de cuenta solo están disponibles para los clientes de Real-time Customer Data Platform B2B Edition. Para obtener más información sobre CDP en tiempo real, incluidas las funciones y funcionalidades disponibles para cada tipo de licencia, comience leyendo la [información general de CDP en tiempo real](../overview.md).

Los perfiles de cuenta permiten unificar la información de la cuenta de varias fuentes. Esta vista unificada de una cuenta aúna datos de sus muchos canales de marketing y los diversos sistemas que está utilizando su organización para almacenar información de cuentas de clientes. Este documento proporciona una guía para interactuar con perfiles de cuenta mediante las funciones de CDP en tiempo real, B2B Edition disponibles en la interfaz de usuario (IU) de Adobe Experience Platform.

## Explorar perfiles de cuenta

Para examinar los perfiles de cuenta, comience por seleccionar **[!UICONTROL Profiles]** en [!UICONTROL Accounts] en el panel de navegación izquierdo.

![](images/b2b-account-browse.png)

En la pestaña **[!UICONTROL Browse]**, puede explorar los perfiles de cuenta mediante un ID de cuenta de un origen empresarial conectado o introduciendo directamente los detalles del origen.

![](images/b2b-account-browse-by.png)

### Examinar por [!UICONTROL Origen empresarial conectado]

Para examinar los perfiles de cuenta por fuente de empresa conectada, seleccione **[!UICONTROL Connected enterprise source]** en la lista desplegable **[!UICONTROL Browse by]** y, a continuación, elija una fuente conectada con el botón de selección situado junto al campo **[!UICONTROL Source]**.

![](images/b2b-account-browse.png)

Se abre el cuadro de diálogo **[!UICONTROL Seleccionar origen]**, donde puede seleccionar un origen basado en las conexiones que ha establecido su organización.

>[!NOTE]
>
>Su organización puede tener varias fuentes configuradas para el mismo proveedor de servicios (por ejemplo, Marketo), por lo que es importante revisar el nombre de la conexión, el sistema de origen y la instancia del sistema de origen para asegurarse de que está buscando por la instancia de origen correcta.

Para obtener más información sobre la conexión de orígenes empresariales, consulte [sources overview](../sources/sources-overview.md).

![](images/b2b-account-select-source.png)

Para elegir un origen, seleccione el botón de opción situado junto al nombre de la conexión y, a continuación, utilice **[!UICONTROL Select]** para volver a la pestaña [!UICONTROL Browse].

Con un origen seleccionado, debe introducir un **[!UICONTROL Account ID]** relacionado con el origen. Por ejemplo, si selecciona un origen de Salesforce, tendrá que introducir un ID de cuenta de la instancia de Salesforce para poder ver el perfil de cuenta vinculado a dicho ID.

>[!NOTE]
>
>Para los ID de cuenta de Marketo, hay dos tablas de cuenta posibles a las que se puede hacer referencia, por lo que debe utilizar una sintaxis específica para asegurarse de que está viendo la cuenta correcta.
>
>La sintaxis estándar más común es el ID de cuenta de Marketo anexado por `.mkto_org` (por ejemplo, `1234567.mkto_org`). Los clientes de Marketing basado en cuentas de Marketo pueden tener valores adicionales que se pueden encontrar usando el ID de cuenta de Marketo anexado por `.mkto_account`. Si no está seguro de qué sintaxis utilizar, consulte con su administrador de Marketo.

![](images/b2b-account-browse-id.png)

### Examinar por [!UICONTROL Others]

CDP en tiempo real, B2B Edition admite la capacidad de realizar una búsqueda directa permitiéndole introducir un **[!UICONTROL Nombre de origen]**, **[!UICONTROL Instancia de origen]** y **[!UICONTROL ID de cuenta]** para una cuenta que desee ver. Al introducir el nombre de origen y la instancia directamente, se proporciona el contexto necesario para que el Experience Platform busque y muestre los datos de perfil de cuenta correctos.

La capacidad de realizar una búsqueda directa es útil en circunstancias en las que no es posible establecer una conexión de origen directamente a los datos. Por ejemplo, si su organización cuenta con políticas de control de datos que impiden la conexión directa a un CRM, puede exportar esos datos a un sistema de almacenamiento en la nube y luego incorporarlos a un Experience Platform.

Otro ejemplo podría ser que está realizando una transformación en los datos entre el momento en que deja un sistema e ingresa en Platform. Puede utilizar la funcionalidad de búsqueda directa para proporcionar contexto a los datos (como especificar que son datos de Marketo, a pesar de que provienen de un bucket de Amazon S3, por ejemplo), de modo que el sistema sepa dónde buscar y cómo procesar correctamente los datos.

Para comenzar una búsqueda directa, seleccione **[!UICONTROL Others]** en la lista desplegable **[!UICONTROL Browse by]** y, a continuación, introduzca un **[!UICONTROL Source name]**, **[!UICONTROL Source instance]** y **[!UICONTROL Account ID]** para la cuenta que desea ver.

![](images/b2b-account-browse-adhoc.png)

## Ver detalles del perfil de la cuenta

Después de utilizar la pestaña **[!UICONTROL Browse]** para localizar un perfil de cuenta, al seleccionar **[!UICONTROL Profile ID]** se abre la pestaña **[!UICONTROL Detail]** del perfil de cuenta. La información de perfil mostrada en la pestaña **[!UICONTROL Detail]** se ha combinado desde varios fragmentos de perfil para formar una sola vista de la cuenta individual. Esto incluye detalles de la cuenta, como atributos básicos y datos de medios sociales.

Los campos predeterminados mostrados también se pueden cambiar en el nivel de organización para mostrar los atributos de perfil de cuenta preferidos.

>[!NOTE]
>
>Hay funciones similares disponibles para perfiles de clientes y se ha creado una guía paso a paso con instrucciones para añadir y eliminar atributos, cambiar el tamaño de los paneles, etc. Lea la [guía de personalización de detalles del perfil](../../profile/ui/profile-customization.md) para obtener más información.

![](images/b2b-account-details.png)

Puede ver detalles adicionales relacionados con la cuenta seleccionando otra de las pestañas disponibles. Estas pestañas incluyen atributos, personas y la pestaña de oportunidades que muestra las oportunidades abiertas y cerradas relacionadas con la cuenta en los sistemas empresariales. Consulte las secciones siguientes para obtener más información sobre cada pestaña.

## Ficha Atributos

La pestaña **[!UICONTROL Attributes]** enumera toda la información de registro relacionada con la cuenta. Esto incluye los datos de atributos procedentes de varios orígenes que se han combinado para formar una sola vista de la cuenta.

Además de poder ver los datos en una lista, puede utilizar la barra de búsqueda para buscar atributos específicos o ver los datos de registro como JSON.

![](images/b2b-account-attributes.png)

## Pestaña Personas

La pestaña **[!UICONTROL People]** proporciona una lista de personas individuales asociadas a la cuenta. Estas personas pueden ser contactos y posibles clientes de diferentes sistemas empresariales gestionados por diferentes equipos de su organización, pero en tiempo real CDP, B2B Edition se presentan juntos como una lista única que le permite ver una vista más holística de los contactos de su cuenta.

>[!NOTE]
>
>La pestaña [!UICONTROL People] muestra una lista de hasta 25 personas asociadas con la cuenta. Para cuentas con más de 25 personas asociadas, el sistema muestra un muestreo aleatorio de 25 registros.

Además de mostrarle una instantánea de la información del contacto, cada persona enumerada también incluye un **[!UICONTROL ID de perfil]**, que es un vínculo en el que se puede hacer clic que le permite explorar el Perfil del cliente en tiempo real para ese individuo. Para obtener más información sobre la visualización de perfiles de clientes individuales relacionados con sus cuentas, visite la guía para [examinar perfiles en CDP en tiempo real, B2B Edition](../profile/profile-browse.md).

![](images/b2b-account-people.png)

## Ficha Oportunidades

La pestaña **[!UICONTROL Oportunidades]** proporciona información para oportunidades abiertas y cerradas relacionadas con la cuenta. Estas oportunidades se pueden incorporar en Experience Platform de múltiples fuentes, sin embargo, CDP en tiempo real, B2B Edition facilita a los especialistas en marketing ver todas estas oportunidades juntas en un solo lugar.

>[!NOTE]
>
>La pestaña [!UICONTROL Oportunidades] muestra una lista de hasta 25 oportunidades asociadas con la cuenta. Para cuentas con más de 25 oportunidades asociadas, el sistema muestra un muestreo aleatorio de 25 registros.

Cada oportunidad incluye información como el nombre de la oportunidad, su cantidad, etapa y si la oportunidad está abierta, cerrada, ganada o perdida.

![](images/b2b-account-opportunities.png)
