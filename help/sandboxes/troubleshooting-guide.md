---
keywords: Experience Platform;inicio;temas populares;solución de problemas de zonas protegidas
solution: Experience Platform
title: Guía de solución de problemas de zonas protegidas
description: Este documento proporciona respuestas a las preguntas frecuentes acerca de los entornos limitados de Adobe Experience Platform.
exl-id: 6a496509-a4e9-4e76-829b-32d67ccfcce6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 8%

---

# Guía de solución de problemas de zonas protegidas

Este documento proporciona respuestas a las preguntas frecuentes acerca de los entornos limitados de Adobe Experience Platform. Si tiene preguntas o necesita solución de problemas en relación con otros servicios de Platform, consulte la [guía de solución de problemas para Experience Platform](../landing/troubleshooting.md).

Los entornos limitados dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital. Consulte la [información general sobre las zonas protegidas](home.md) para obtener más detalles.

## ¿Qué es una zona protegida?

Las zonas protegidas son particiones virtuales en una sola instancia de Experience Platform. Cada zona protegida mantiene su propia biblioteca independiente de recursos de Platform (incluidos esquemas, conjuntos de datos, perfiles, etc.). Todo el contenido y las acciones realizadas en una zona protegida se limitan únicamente a esa zona protegida y no afectan a ninguna otra. Consulte la [información general sobre las zonas protegidas](home.md) para obtener más detalles.

## ¿Qué tipos de zonas protegidas están disponibles y cuáles son sus diferencias? {#sandbox-types}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtypes"
>title="Tipo de zona protegida"
>abstract="El tipo de zona protegida indica si se trata de una zona protegida de producción o desarrollo. Las zonas protegidas de producción incluyen datos activos y las zonas protegidas de desarrollo se utilizan para pruebas y desarrollo."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sandbox/ui/user-guide.html?lang=es#create" text="Creación de una zona protegida en la interfaz de usuario"

Hay dos tipos de zonas protegidas disponibles en Experience Platform:

* **Zona protegida de producción**: Una zona protegida de producción está pensada para utilizarse con perfiles en su entorno de producción. Platform le permite crear varios entornos limitados de producción para proporcionar la funcionalidad adecuada para los datos sin perder el aislamiento operativo. Esta función le permite dedicar entornos limitados de producción específicos a distintas líneas de negocio, marcas, proyectos o regiones. Las zonas protegidas de producción admiten un volumen de perfiles de producción hasta el compromiso con licencia [!DNL Profile] (medido acumulativamente en todas las zonas protegidas de producción autorizadas). Tiene derecho a utilizar el perfil promedio con licencia por cada [!DNL Profile] autorizado (medido acumulativamente en todas las zonas protegidas de producción autorizadas).
* **Entorno aislado de desarrollo**: Un entorno aislado de desarrollo es un entorno aislado que se puede usar exclusivamente para el desarrollo y las pruebas con perfiles que no sean de producción. Los entornos limitados de desarrollo admiten un volumen de perfiles que no son de producción de hasta el 10 % de la asignación [!DNL Profile] con licencia (medida de forma acumulativa en todos los entornos limitados de desarrollo autorizados). Tiene derecho a hasta:
   * Una riqueza promedio de perfiles de no producción de 75 kilobytes por perfil de no producción autorizado (medida acumulativamente en todas las zonas protegidas de desarrollo autorizadas).
   * Un trabajo de segmentación por lotes al día, por zona protegida de desarrollo;
   * Un promedio de 120 [!DNL Profile] llamadas de API, por [!DNL Profile], por año (medidas acumulativamente en todas sus zonas protegidas de desarrollo autorizadas).

Consulte la [información general sobre las zonas protegidas](./home.md) para obtener más detalles.

## ¿Puedo acceder a un recurso desde más de una zona protegida?

Los entornos limitados para pruebas son particiones aisladas de una sola instancia de Platform, y cada entorno limitado mantiene su propia biblioteca independiente de recursos. No se puede acceder a un recurso que existe en una zona protegida desde ninguna otra, independientemente del tipo de zona protegida (producción o no producción).

## ¿Cuál es la zona protegida de producción predeterminada?

La zona protegida de producción predeterminada es la primera zona protegida de producción que se crea cuando se aprovisiona una organización por primera vez. La zona protegida de producción predeterminada le permite introducir o consumir datos de Platform, así como aceptar solicitudes que no incluyen valores para un nombre de zona protegida o un ID de zona protegida. La zona protegida de producción predeterminada se puede restablecer, pero no eliminar.

## ¿Cuántas zonas protegidas de producción puedo tener?

Una instancia de Experience Platform admite varios entornos limitados de producción y desarrollo, y cada uno de ellos mantiene su propia biblioteca independiente de recursos de Platform (incluidos esquemas, conjuntos de datos y perfiles).

Una licencia de Experience Platform predeterminada le concede un total de cinco zonas protegidas, que puede clasificar como producción o desarrollo. Puede obtener una licencia de paquetes adicionales de 10 zonas protegidas, hasta un máximo de 75 zonas protegidas en total.

Las zonas protegidas de producción se pueden restablecer o eliminar, excepto las que también se están usando en Adobe Analytics para la característica [Análisis entre dispositivos (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=es), o si Adobe Audience Manager también está usando el gráfico de identidades alojado en ellas para la característica [Destinos basados en personas (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=es).

Puede actualizar el título de una zona protegida de producción. Sin embargo, no se puede cambiar el nombre de una zona protegida de producción.

>[!NOTE]
>
>El nombre de la zona protegida se utiliza con fines de búsqueda en llamadas a la API, mientras que el título de la zona protegida se utiliza como nombre para mostrar.

## ¿Cuántas zonas protegidas de desarrollo puedo tener?

En la actualidad, Experience Platform permite que un máximo de 75 zonas protegidas totales (producción y desarrollo) estén activas dentro de una sola organización.

Los entornos limitados de desarrollo admiten las funcionalidades de restablecimiento y eliminación.

## Acabo de crear una zona protegida. ¿Cómo configuro permisos para los usuarios que trabajarán con esta zona protegida?

Adobe Admin Console vincula a los usuarios a zonas protegidas y permisos mediante el uso de perfiles de producto. Después de crear una nueva zona protegida, vaya a la pestaña **Permisos** del perfil de producto al que desea conceder acceso y, a continuación, haga clic en **Zonas protegidas**. Desde aquí, puede agregar o quitar el acceso a la nueva zona protegida de la misma manera que otros permisos.

Si desea agregar permisos únicos a los usuarios de una zona protegida determinada, es posible que tenga que crear un nuevo perfil de producto con las zonas protegidas y los permisos adecuados aplicados y asignar esos usuarios a ese perfil.

Consulte la [guía del usuario de control de acceso](../access-control/ui/overview.md) para obtener más información sobre la administración de zonas protegidas y permisos en el Admin Console.
