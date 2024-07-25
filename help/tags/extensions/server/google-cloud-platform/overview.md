---
title: Extensión de reenvío de eventos de Google Cloud Platform
description: Esta extensión de reenvío de eventos de Adobe Experience Platform envía eventos de Edge Network a Google Cloud Platform.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: c5da1889-f917-42aa-b3a4-9557c31d6ee8
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 2%

---

# Extensión de reenvío de eventos de [!DNL Google Cloud Platform]

[[!DNL Google Cloud Platform]](https://cloud.google.com/) es una plataforma de computación en la nube que ofrece una amplia variedad de servicios, como computación distribuida, almacenamiento de bases de datos, entrega de contenido y servicios de integración de software como servicio (SaaS) para la administración de la relación con los clientes (CRM) y la planificación de recursos empresariales (ERP).

La extensión [!DNL Google Cloud Platform] [reenvío de eventos](../../../ui/event-forwarding/overview.md) aprovecha [[!DNL Cloud Pub/Sub]](https://cloud.google.com/pubsub) para enviar eventos del Edge Network de Adobe Experience Platform a [!DNL Google Cloud Platform] para un procesamiento posterior. Esta guía explica cómo instalar la extensión y utilizar sus funcionalidades en una regla de reenvío de eventos.

## Requisitos previos

Para usar esta extensión, debe tener una cuenta de [!DNL Google Cloud Platform] con un tema de [!DNL Cloud Pub/Sub] existente. Si no tiene un tema preexistente, consulte la documentación de [[!DNL Google Cloud Platform]](https://cloud.google.com/pubsub/docs/create-topic) sobre la creación y administración de temas.

### Creación de un secreto y un elemento de datos

En primer lugar, cree un nuevo `Google OAuth 2` [secreto de reenvío de eventos](../../../ui/event-forwarding/secrets.md), que se utilizará para autenticar la conexión con su cuenta y mantener el valor seguro.

A continuación, [cree un elemento de datos](../../../ui/managing-resources/data-elements.md#create-a-data-element) con la extensión **[!UICONTROL Core]** y un tipo de elemento de datos **[!UICONTROL Secret]** para hacer referencia al secreto `Google OAuth 2` que acaba de crear.

## Instalar y configurar la extensión [!DNL Google Cloud Platform] {#install}

Para instalar la extensión, [cree una propiedad de reenvío de eventos](../../../ui/event-forwarding/overview.md#properties) o elija una propiedad existente para editar en su lugar.

Seleccione **[!UICONTROL Extensiones]** en el panel de navegación izquierdo. En la ficha **[!UICONTROL Catálogo]**, seleccione **[!UICONTROL Instalar]** en la tarjeta de la extensión [!DNL Google Cloud Platform].

![La extensión del catálogo [!DNL Google Cloud Platform] resalta la instalación.](../../../images/extensions/server/google-cloud-platform/install-extension.png)

En la pantalla de configuración, escriba el secreto del elemento de datos que creó anteriormente en el campo **[!UICONTROL Token de acceso]**. El secreto del elemento de datos contendrá su token de OAuth 2 [!DNL Google Cloud Platform]. Seleccione **[!UICONTROL Guardar]** cuando haya terminado.

![Página de configuración de la extensión [!DNL Google Cloud Platform].](../../../images/extensions/server/google-cloud-platform/configure-extension.png)

## Crear una regla [!DNL Send Data to Cloud Pub/Sub] {#tracking-rule}

Una vez instalada la extensión, cree una nueva regla de reenvío de eventos [rule](../../../ui/managing-resources/rules.md) y configure sus condiciones como desee. Al configurar las acciones de la regla, seleccione la extensión **[!UICONTROL Google Cloud Platform]** y, a continuación, seleccione **[!UICONTROL Enviar datos a Cloud Pub/Sub]** para el tipo de acción.

![Vista de configuración de acción para [!UICONTROL Google Cloud Platform], con la acción resaltada y [!UICONTROL Enviar datos a Cloud Pub/Sub].](../../../images/extensions/server/google-cloud-platform/event-action.png)

| Entrada | Descripción |
| --- | --- |
| [!UICONTROL Tema] | Tema que recibirá los eventos del reenvío de eventos. El valor debe tener el formato `projects/{projectName}/topics/{topicName}`. |
| [!UICONTROL Datos] | Este campo contiene los datos que se van a reenviar al tema [!DNL Cloud Pub/Sub] en formato JSON.<br><br>En la opción **[!UICONTROL Sin procesar]**, puede pegar el objeto JSON directamente en el campo de texto proporcionado o puede seleccionar el icono del elemento de datos (![Icono del conjunto de datos](/help/images/icons/database.png)) para seleccionarlo de una lista de elementos de datos existentes para representar los datos.<br><br>También puede usar la opción **[!UICONTROL Editor de pares clave-valor de JSON]** para agregar manualmente cada par clave-valor a través de un editor de interfaz de usuario. Cada valor se puede representar mediante una entrada sin procesar o se puede seleccionar un elemento de datos en su lugar. |
| [!UICONTROL Atributos] | Este campo contiene el objeto JSON con atributos adicionales que se envían junto con el mensaje.<br><br>En la opción **[!UICONTROL Sin procesar]**, puede pegar el objeto JSON directamente en el campo de texto proporcionado o puede seleccionar el icono del elemento de datos (![Icono del conjunto de datos](/help/images/icons/database.png)) para seleccionarlo de una lista de elementos de datos existentes para representar los datos.<br><br>También puede usar la opción **[!UICONTROL Editor de pares clave-valor de JSON]** para agregar manualmente cada par clave-valor a través de un editor de interfaz de usuario. Cada valor se puede representar mediante una entrada sin procesar o se puede seleccionar un elemento de datos en su lugar. |

{style="table-layout:auto"}

## Pasos siguientes

Esta guía explica cómo enviar datos a [!DNL Cloud Pub/Sub] mediante la extensión de reenvío de eventos [!DNL Google Cloud Platform]. Para obtener más información sobre las funcionalidades de reenvío de eventos en Experience Platform, consulte la [descripción general del reenvío de eventos](../../../ui/event-forwarding/overview.md).
