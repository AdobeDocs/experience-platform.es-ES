---
title: Información general sobre PathFactory Source
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
>El origen [!DNL PathFactory] está en la versión beta. Lea [información general de orígenes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de orígenes etiquetados como beta.

[[!DNL PathFactory]](https://www.pathfactory.com/) ofrece una plataforma basada en la nube que ayuda a las empresas a administrar los recorridos de contenido y a impulsar la participación mediante perspectivas de contenido inteligentes. Esta guía detalla cómo puede integrar los datos de PathFactory en Experience Platform, utilizando los conectores de PathFactory para una ingesta de datos óptima.

Puede ingerir datos de [[!DNL PathFactory]](https://www.pathfactory.com/) mediante tres orígenes principales:

* **[!DNL Visitors]**: ingrese datos de clientes y contactos como registros para comprender mejor a su audiencia.
* **[!DNL Sessions]**: eventos de series temporales que rastrean actividades de sesión de usuarios individuales en su plataforma.
* **[!DNL Page Views]**: eventos de series de tiempo que proporcionan perspectivas sobre qué páginas se están viendo, lo que le ayuda a analizar el rendimiento del contenido.

Lea el documento siguiente para obtener información sobre cómo configurar su cuenta de origen de [!DNL PathFactory].

## LISTA DE PERMITIDOS de direcciones IP {#ip-allow-list}

Es posible que sea necesario agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la página [lista de permitidos de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Requisitos previos {#prerequisites}

Antes de comenzar a integrar los conectores de [[!DNL PathFactory]](https://www.pathfactory.com/) con Experience Platform, asegúrese de cumplir los siguientes requisitos previos:

* **Cuenta de [PathFactory]**.
   * Póngase en contacto con [[!DNL PathFactory]](https://www.pathfactory.com/portal/company/contactus.shtml) si todavía no tiene una cuenta válida.
* **Suscripción activa** a cualquier producto [!DNL PathFactory].
* **Nombre de usuario, contraseña y dominio**.
   * Estas credenciales son necesarias para tener acceso a la cuenta de [!DNL PathFactory] y a sus datos.
* **Token de acceso** y **extremos de API**.
   * Son necesarios para conectarse con las API [!DNL PathFactory].

### Cómo obtener credenciales y tokens de acceso {#gather-credentials}

Para conectar a [!DNL PathFactory] al Experience Platform, debe proporcionar las siguientes credenciales:

| Credencial | Descripción | Punto de conexión |
| --- | --- | --- |
| Nombre de usuario | Su nombre de usuario de la cuenta [!DNL PathFactory]. | No aplicable |
| Contraseña | Contraseña de su cuenta de [!DNL PathFactory]. | No aplicable |
| Dominio | El dominio asociado con su cuenta de [!DNL PathFactory]. | No aplicable |
| Token de acceso | Un token único utilizado para la autenticación de API. | No aplicable |
| Punto final de visitantes | Extremo de la API para datos de visitantes. | `/api/public/v3/data_lake_apis/visitors.json` |
| Punto final de sesiones | Punto final de API para los datos de sesión. | `/api/public/v3/data_lake_apis/sessions.json` |
| Extremo de vistas de página | Punto final de la API para los datos de vista de página. | `/api/public/v3/data_lake_apis/page_views.json` |

Para obtener instrucciones detalladas sobre cómo obtener tu nombre de usuario, contraseña, dominio y token de acceso, visita el [[!DNL PathFactory] Centro de soporte](https://support.pathfactory.com/categories/adobe/). Este recurso proporciona guías completas para recuperar y administrar las credenciales.

### Configuración de permisos en el Experience Platform

Debe tener los permisos para **[!UICONTROL Ver fuentes]** y **[!UICONTROL Administrar fuentes]** habilitados en su cuenta para conectar su cuenta de [!DNL PathFactory] al Experience Platform. Póngase en contacto con el administrador del producto para obtener los permisos necesarios. Para obtener más información, lea la [guía de la interfaz de usuario de control de acceso](../../../access-control/ui/overview.md).

## Conectar [!DNL PathFactory] a Platform {#pathfactory-connect}

La siguiente documentación proporciona información sobre cómo conectar [!DNL PathFactory] a Platform mediante API o la interfaz de usuario:

* [Cree una conexión de origen y un flujo de datos para llevar [!DNL PathFactory] datos a Platform mediante API](../../tutorials/api/create/marketing-automation/pathfactory.md).
* [Conecte su cuenta de  [!DNL PathFactory] al Experience Platform mediante la interfaz de usuario](../../tutorials/ui/create/marketing-automation/pathfactory.md).
* [Cree un flujo de datos para una conexión de origen mediante la interfaz de usuario](../../tutorials/ui/dataflow/marketing-automation.md).
