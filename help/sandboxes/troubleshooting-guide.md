---
keywords: Experience Platform;inicio;temas populares;solución de problemas de zonas protegidas
solution: Experience Platform
title: Guía de solución de problemas de zonas protegidas
description: Este documento proporciona respuestas a las preguntas frecuentes acerca de los entornos limitados de Adobe Experience Platform.
exl-id: 6a496509-a4e9-4e76-829b-32d67ccfcce6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 9%

---

# Solución de problemas de los entornos aislados guía

Este documento proporciona respuestas a las preguntas más frecuentes sobre los entornos aislados en Adobe Experience Platform. Para preguntas y problemas relacionados con otros servicios Experience Platform, consulte el guía de solución de problemas de Experience Platform[](../landing/troubleshooting.md).

Los entornos aislados dividen una sola Experience Platform instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital. Consulte la [información general sobre las zonas protegidas](home.md) para obtener más detalles.

## ¿Qué es un sandbox?

Las zonas protegidas son particiones virtuales dentro de una única instancia de Experience Platform. Cada entorno limitado mantiene su propia biblioteca independiente de recursos Experience Platform (incluidos esquemas, conjuntos de datos, perfiles, etc.). Todo el contenido y las acciones realizadas en una zona protegida se limitan únicamente a esa zona protegida y no afectan a ninguna otra. Consulte la [información general sobre las zonas protegidas](home.md) para obtener más detalles.

## ¿Qué tipos de zonas protegidas están disponibles y cuáles son sus diferencias? {#sandbox-types}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtypes"
>title="Tipo de zona protegida"
>abstract="El tipo de zona protegida indica si se trata de una zona protegida de producción o desarrollo. Las zonas protegidas de producción incluyen datos activos y las zonas protegidas de desarrollo se utilizan para pruebas y desarrollo."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sandbox/ui/user-guide.html?lang=es#create" text="Creación de una zona protegida en la interfaz de usuario"

Hay dos tipos de sandbox disponibles en Experience Platform:

* **Sandbox** de producción: Un sandbox de producción está diseñado para usarse con perfiles en su entorno de producción. Experience Platform le permite crear múltiples entornos limitados de producción para proporcionar la funcionalidad correcta para los datos y, al mismo tiempo, mantener el aislamiento operativo. Esta característica le permite dedicar entornos limitados de producción específicos a distintas líneas de negocio, marcas, proyectos o regiones. Los entornos limitados de producción admiten un volumen de perfiles de producción hasta su compromiso con licencia [!DNL Profile] (medido acumulativamente en todos sus entornos limitados de producción autorizados). Tiene derecho a utilizar todo el volumen total de datos con licencia (medido acumulativamente en todas las zonas protegidas de producción autorizadas).

* **Entorno aislado de desarrollo**: Un entorno aislado de desarrollo es un entorno aislado que se puede usar exclusivamente para el desarrollo y las pruebas con perfiles que no sean de producción. Los entornos limitados de desarrollo admiten un volumen de perfiles que no son de producción de hasta el 10 % de la asignación [!DNL Profile] con licencia (medida de forma acumulativa en todos los entornos limitados de desarrollo autorizados). Tiene derecho a hasta:
   * Un trabajo de segmentación por lotes al día, por zona protegida de desarrollo;
   * Un promedio de 120 [!DNL Profile] llamadas de API, por [!DNL Profile], por año (medidas acumulativamente en todas sus zonas protegidas de desarrollo autorizadas).

Consulte la [información general sobre las zonas protegidas](./home.md) para obtener más detalles.

## ¿Puedo acceder a un recurso desde más de un entorno limitado?

Las cajas de arena son particiones aisladas de una sola instancia de Experience Platform, y cada caja de arena mantiene su propia biblioteca independiente de recursos. No se puede acceder a un recurso que existe en un entorno limitado desde ningún otro entorno limitado, independientemente del tipo de entorno limitado (producción o no producción).

## ¿Qué es el simulador de pruebas de producción predeterminado?

El simulador de pruebas de producción predeterminado es el primer simulador de pruebas de producción que se crea cuando se aprovisiona una organización por primera vez. El espacio aislado de producción predeterminado le permite ingerir o consumir datos de Experience Platform, así como aceptar solicitudes que no incluyan valores para un nombre de espacio aislado o un ID de espacio aislado. El entorno de pruebas de producción predeterminado se puede restablecer pero no eliminar.

## ¿Cuántos sandboxes de producción puedo tener?

Una instancia de Experience Platform admite varios entornos limitados de producción y desarrollo, y cada entorno limitado mantiene su propia biblioteca independiente de recursos de Experience Platform (incluidos esquemas, conjuntos de datos y perfiles).

Una licencia predeterminada de Experience Platform le concede un total de cinco zonas protegidas, que puede clasificar como producción o desarrollo. Puede obtener una licencia de paquetes adicionales de 10 zonas protegidas, hasta un máximo de 75 zonas protegidas en total.

Las zonas protegidas de producción se pueden restablecer o eliminar, excepto las que también se están usando en Adobe Analytics para la característica [Análisis entre dispositivos (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=es), o si Adobe Audience Manager también está usando el gráfico de identidades alojado en ellas para la característica [Destinos basados en personas (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=es).

Puede actualizar el título de una zona protegida de producción. Sin embargo, no se puede cambiar el nombre de un entorno limitado de producción.

>[!NOTE]
>
>El nombre del espacio aislado se usa con fines de búsqueda en las llamadas de API, mientras que el título del espacio aislado se usa como nombre para mostrar.

## ¿Cuántos sandboxes de desarrollo puedo tener?

Experience Platform actualmente permite que un máximo de 75 sandboxes totales (producción y desarrollo) estén activos dentro de una sola organización.

Los entornos limitados de desarrollo admiten funcionalidades de restablecimiento y eliminación.

## Acabo de crear un sandbox. ¿Cómo configuro permisos para los usuarios que trabajarán con esta zona protegida?

Adobe Admin Console vincula a los usuarios a zonas protegidas y permisos mediante el uso de perfiles de producto. Después de crear una nueva zona protegida, vaya a la pestaña **Permisos** del perfil de producto al que desea conceder acceso y, a continuación, haga clic en **Zonas protegidas**. Desde aquí, puede agregar o quitar el acceso a la nueva zona protegida de la misma manera que otros permisos.

Si desea agregar permisos únicos a los usuarios de una zona protegida determinada, es posible que tenga que crear un nuevo perfil de producto con las zonas protegidas y los permisos adecuados aplicados y asignar esos usuarios a ese perfil.

Consulte la [guía del usuario de control de acceso](../access-control/ui/overview.md) para obtener más información sobre la administración de zonas protegidas y permisos en Admin Console.
