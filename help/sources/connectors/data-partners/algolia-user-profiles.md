---
title: Algolia Perfiles de usuario Source Información general
description: Obtenga información acerca de la fuente de perfiles de usuario de Algolia en Adobe Experience Platform
hide: true
hidefromtoc: true
source-git-commit: 1bde4b831f1b79de1a8292ad5f221f522e871d08
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# [!DNL Algolia User Profiles]

[[!DNL Algolia]](https://www.algolia.com/) es una potente plataforma de API de búsqueda y descubrimiento que permite a las empresas ofrecer experiencias de búsqueda rápidas, relevantes y personalizables. Proporciona funciones de búsqueda en tiempo real con funciones como tolerancia ante errores tipográficos, filtrado, faceteo y ajuste de relevancia con tecnología de IA. [!DNL Algolia] ayuda a las empresas a mejorar la participación del usuario, las tasas de conversión y la experiencia general del cliente al proporcionar soluciones de búsqueda de alto rendimiento para sitios web, plataformas de comercio electrónico y aplicaciones.

Algunos de los beneficios clave de [!DNL Algolia] son:

* Búsqueda ultrarrápida con resultados instantáneos.
* Recomendaciones muy relevantes impulsadas por IA.
* Clasificación personalizable para priorizar las necesidades comerciales.
* Capacidad de ampliación para gestionar cargas de tráfico elevadas sin esfuerzo.

Para obtener más información, visite la [[!DNL Algolia] documentación del producto](https://resources.algolia.com/).

## Arquitectura

Fuentes de autoservicio (SDK por lotes) proporciona todas las funciones necesarias, como autenticación, paginación o extracción de datos completa o parcial. El origen [!DNL Algolia User Profiles] utiliza estas características para completar la integración.

![Arquitectura de la integración de Algolia y Experience Platform](../../images/tutorials/create/algolia/user-profiles/algolia-aep-user-profiles-arch.png)

## Requisitos previos {#prerequisites}

Debe completar los siguientes pasos previos para poder conectar su cuenta de [!DNL Algolia] a Experience Platform.

1. Use [[!DNL Algolia] panel](https://dashboard.algolia.com/users/sign_up) para iniciar sesión en su cuenta de [!DNL Algolia] o crear una nueva cuenta.
2. [Prepare su índice](https://www.algolia.com/doc/guides/sending-and-managing-data/prepare-your-data/in-depth/prepare-data-in-depth/).
3. [Configurar las facetas](https://www.algolia.com/doc/guides/managing-results/refine-results/faceting/).
4. [Enviar eventos de usuario](https://www.algolia.com/doc/guides/sending-events/getting-started/).
5. [Personalice su índice](https://www.algolia.com/doc/guides/personalization/advanced-personalization/configure/setup/indices/).

### Configuración de permisos en Experience Platform

Debe tener los permisos para **[!UICONTROL Ver fuentes]** y **[!UICONTROL Administrar fuentes]** habilitados en su cuenta para conectar su cuenta de [!DNL Algolia] a Experience Platform. Póngase en contacto con el administrador del producto para obtener los permisos necesarios. Para obtener más información, lea la [guía de la interfaz de usuario de control de acceso](../../../access-control/abac/ui/permissions.md).

### LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la página [lista de permitidos de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Conecte su cuenta de [!DNL Algolia] a Experience Platform

Una vez que hayas completado los requisitos previos, puedes continuar con el siguiente paso y [conectar tu cuenta de  [!DNL Algolia] a Experience Platform](../../tutorials/ui/create/data-partners/algolia-user-profiles.md).
