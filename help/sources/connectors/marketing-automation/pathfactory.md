---
title: Información general de origen de PathFactory
description: Obtenga información sobre cómo conectar PathFactory a Adobe Experience Platform mediante API o la interfaz de usuario.
last-substantial-update: 2024-04-30T00:00:00Z
badge: Beta
exl-id: befb73c4-fd6a-4512-9124-d23a1c27e0e0
source-git-commit: ca17854830edabaf2bd74265258d6f0096f2888e
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 3%

---

# [!DNL PathFactory]

>[!NOTE]
>
>El [!DNL PathFactory] el origen está en versión beta. Lea el [información general de orígenes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes etiquetadas como beta.

[[!DNL PathFactory]](https://www.pathfactory.com/) ofrece una plataforma basada en la nube que ayuda a las empresas a administrar los recorridos de contenido y a impulsar la participación mediante perspectivas de contenido inteligentes. Esta guía detalla cómo puede integrar los datos de PathFactory en Experience Platform, utilizando los conectores de PathFactory para una ingesta de datos óptima.

Puede introducir datos de [[!DNL PathFactory]](https://www.pathfactory.com/) uso de tres fuentes principales:

* **[!DNL Visitors]**: ingrese datos de clientes y contactos como registros para comprender mejor a su audiencia.
* **[!DNL Sessions]**: Eventos de series temporales que rastrean actividades de sesión de usuarios individuales en la plataforma.
* **[!DNL Page Views]**: Eventos de series temporales que proporcionan perspectivas sobre qué páginas se están viendo, lo que le ayuda a analizar el rendimiento del contenido.

Lea el siguiente documento para obtener información sobre cómo configurar su [!DNL PathFactory] cuenta de origen.

## LISTA DE PERMITIDOS de direcciones IP {#ip-allow-list}

Es posible que sea necesario agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la [LISTA DE PERMITIDOS de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Requisitos previos {#prerequisites}

Antes de comenzar la integración [[!DNL PathFactory]](https://www.pathfactory.com/) conectores con Experience Platform, asegúrese de cumplir los siguientes requisitos previos:

* **A [cuenta de PathFactory]**.
   * Contacto [[!DNL PathFactory]](https://www.pathfactory.com/portal/company/contactus.shtml) si todavía no tiene una cuenta válida.
* **Una suscripción activa** a cualquier [!DNL PathFactory] producto.
* **Nombre de usuario, contraseña y dominio**.
   * Estas credenciales son necesarias para acceder a su [!DNL PathFactory] y sus datos.
* **Token de acceso** y **Extremos de API**.
   * Son necesarios para conectarse a [!DNL PathFactory] API.

### Cómo obtener credenciales y tokens de acceso {#gather-credentials}

Para conectar [!DNL PathFactory] para acceder a Experience Platform, debe proporcionar las siguientes credenciales:

| Credencial | Descripción | Extremo |
| --- | --- | --- |
| Nombre de usuario | Su [!DNL PathFactory] nombre de usuario de cuenta. | No aplicable |
| Una contraseña | Su [!DNL PathFactory] contraseña de la cuenta. | No aplicable |
| Dominio | El dominio asociado con su [!DNL PathFactory] cuenta. | No aplicable |
| Token de acceso | Un token único utilizado para la autenticación de API. | No aplicable |
| Punto final de visitantes | Extremo de la API para datos de visitantes. | `/api/public/v3/data_lake_apis/visitors.json` |
| Punto final de sesiones | Punto final de API para los datos de sesión. | `/api/public/v3/data_lake_apis/sessions.json` |
| Extremo de vistas de página | Punto final de la API para los datos de vista de página. | `/api/public/v3/data_lake_apis/page_views.json` |

Para obtener instrucciones detalladas sobre cómo obtener su nombre de usuario, contraseña, dominio y token de acceso, visite la [[!DNL PathFactory] Centro de asistencia](https://support.pathfactory.com/categories/adobe/). Este recurso proporciona guías completas para recuperar y administrar las credenciales.

### Configuración de permisos en el Experience Platform

Debe tener ambos **[!UICONTROL Ver orígenes]** y **[!UICONTROL Administrar fuentes]** permisos habilitados para su cuenta con el fin de conectar su [!DNL PathFactory] cuenta para el Experience Platform. Póngase en contacto con el administrador del producto para obtener los permisos necesarios. Para obtener más información, lea la [guía de IU de control de acceso](../../../access-control/ui/overview.md).

## Connect [!DNL PathFactory] a Platform {#pathfactory-connect}

La siguiente documentación proporciona información sobre cómo conectarse [!DNL PathFactory] Vaya a Platform mediante las API o la interfaz de usuario de:

* [Crear una conexión de origen y un flujo de datos para traer [!DNL PathFactory] datos a Platform mediante API](../../tutorials/api/create/marketing-automation/pathfactory.md).
* [Conecte su [!DNL PathFactory] cuenta de al Experience Platform mediante la interfaz de usuario de](../../tutorials/ui/create/marketing-automation/pathfactory.md).
* [Crear un flujo de datos para una conexión de origen mediante la interfaz de usuario](../../tutorials/ui/dataflow/marketing-automation.md).
