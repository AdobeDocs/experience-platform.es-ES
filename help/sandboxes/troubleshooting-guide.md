---
keywords: Experience Platform;inicio;temas populares;solución de problemas de entornos limitados
solution: Experience Platform
title: Guía de solución de problemas de entornos limitados
description: Este documento proporciona respuestas a las preguntas más frecuentes sobre los entornos limitados de Adobe Experience Platform.
exl-id: 6a496509-a4e9-4e76-829b-32d67ccfcce6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 9%

---

# Guía de solución de problemas de los Simuladores para pruebas

Este documento proporciona respuestas a las preguntas más frecuentes sobre los entornos limitados de Adobe Experience Platform. Para preguntas y solución de problemas relacionados con otros servicios de Platform, consulte la [Guía de solución de problemas del Experience Platform](../landing/troubleshooting.md).

Los entornos limitados dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital. Consulte la [información general sobre las zonas protegidas](home.md) para obtener más detalles.

## ¿Qué es un simulador de pruebas?

Los entornos limitados son particiones virtuales dentro de una sola instancia de Experience Platform. Cada simulador para pruebas mantiene su propia biblioteca independiente de recursos de Platform (incluidos esquemas, conjuntos de datos, perfiles, etc.). Todo el contenido y las acciones realizadas dentro de un simulador de pruebas solo se limitan a ese simulador de pruebas y no afectan a ningún otro simulador de pruebas. Consulte la [información general sobre las zonas protegidas](home.md) para obtener más detalles.

## ¿Qué tipos de entornos limitados están disponibles y cuáles son sus diferencias? {#sandbox-types}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtypes"
>title="Tipo de zona protegida"
>abstract="El tipo de zona protegida indica si se trata de una zona protegida de producción o desarrollo. Las zonas protegidas de producción incluyen datos activos y las zonas protegidas de desarrollo se utilizan para pruebas y desarrollo."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sandbox/ui/user-guide.html?lang=es#create" text="Creación de una zona protegida en la interfaz de usuario"

Hay dos tipos de entornos limitados disponibles en el Experience Platform:

* **Espacio aislado de producción**: Un simulador para pruebas de producción está diseñado para utilizarse con perfiles en el entorno de producción. Platform le permite crear varios entornos limitados de producción para proporcionar la funcionalidad adecuada a los datos sin dejar de mantener el aislamiento operativo. Esta función le permite dedicar entornos limitados de producción específicos a distintas líneas de negocio, marcas, proyectos o regiones. Los entornos limitados de producción admiten un volumen de perfiles de producción hasta la licencia [!DNL Profile] compromiso (medido acumulativamente en todos los entornos limitados de producción autorizados). Tiene derecho a usar un perfil promedio autorizado por cada [!DNL Profile] (medida acumulativamente en todos los entornos limitados de producción autorizados).
* **Entornos aislados de desarrollo**: Un entorno limitado de desarrollo es un entorno limitado que se puede utilizar exclusivamente para desarrollo y pruebas con perfiles que no sean de producción. Los entornos limitados de desarrollo admiten un volumen de perfiles que no son de producción de hasta el 10% de las licencias [!DNL Profile] compromiso (medido acumulativamente en todos los entornos limitados de desarrollo autorizados). Tiene derecho a:
   * Una riqueza media de perfil no productiva de 75 kilobytes por perfil no de producción autorizado (medida acumulativamente en todos los entornos limitados de desarrollo autorizados);
   * Un trabajo de segmentación por lotes al día, por simulador de pruebas de desarrollo;
   * Un promedio de 120 [!DNL Profile] llamadas de API, por [!DNL Profile], por año (se mide acumulativamente en todos los entornos limitados de desarrollo autorizados.

Consulte la [información general sobre las zonas protegidas](./home.md) para obtener más detalles.

## ¿Puedo acceder a un recurso desde más de un simulador para pruebas?

Los entornos limitados son particiones aisladas de una sola instancia de Platform, y cada entorno limitado mantiene su propia biblioteca de recursos independiente. No se puede acceder a un recurso que existe en un simulador de pruebas desde ningún otro simulador de pruebas, independientemente del tipo de simulación de pruebas (de producción o sin producción).

## ¿Cuál es el entorno limitado de producción predeterminado?

El entorno limitado de producción predeterminado es el primer entorno limitado de producción que se crea cuando se aprovisiona por primera vez una organización. El entorno limitado de producción predeterminado le permite ingerir o consumir datos de Platform, así como aceptar solicitudes que no incluyan valores para un nombre de entorno limitado o un ID de simulador de pruebas. El simulador para pruebas de producción predeterminado se puede restablecer, pero no eliminar.

## ¿Cuántos entornos limitados de producción puedo tener?

Una instancia de Experience Platform admite varios entornos limitados de producción y desarrollo, y cada entorno limitado mantiene su propia biblioteca independiente de recursos de Platform (incluidos esquemas, conjuntos de datos y perfiles).

Una licencia de Experience Platform predeterminada le otorga un total de cinco entornos limitados, que puede clasificar como de producción o desarrollo. Puede obtener una licencia de paquetes adicionales de 10 entornos limitados hasta un máximo de 75 entornos limitados en total.

Los entornos limitados de producción se pueden restablecer o eliminar, excepto en los entornos limitados de producción que también esté utilizando Adobe Analytics para el [Análisis entre dispositivos (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=es) o si el gráfico de identidad alojado en él también está siendo utilizado por Adobe Audience Manager para la función [People Based Destinations (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=es) función.

Puede actualizar el título de un simulador para pruebas de producción. Sin embargo, no se puede cambiar el nombre de un simulador para pruebas de producción.

>[!NOTE]
>
>El nombre del simulador para pruebas se utiliza con fines de búsqueda en llamadas a la API, mientras que el título del simulador para pruebas se utiliza como nombre para mostrar.

## ¿Cuántos entornos limitados de desarrollo puedo tener?

Actualmente, el Experience Platform permite que un máximo de 75 entornos limitados (producción y desarrollo) estén activos dentro de una sola organización.

Los entornos limitados de desarrollo admiten las funciones de restablecimiento y eliminación.

## Acabo de crear un simulador de pruebas. ¿Cómo establezco permisos para los usuarios que trabajarán con este simulador para pruebas?

Adobe Admin Console vincula a los usuarios con entornos limitados y permisos mediante el uso de perfiles de producto. Después de crear un nuevo simulador de pruebas, vaya a la **Permisos** del perfil de producto al que desea conceder acceso y, a continuación, haga clic en **Sandboxes**. Desde aquí, puede agregar o eliminar el acceso al nuevo simulador de pruebas del mismo modo que con otros permisos.

Si desea agregar permisos únicos a los usuarios de un entorno limitado concreto, es posible que tenga que crear un nuevo perfil de producto con los entornos limitados y permisos adecuados aplicados y asignar esos usuarios a ese perfil.

Consulte la [guía del usuario de control de acceso](../access-control/ui/overview.md) para obtener más información sobre la administración de entornos limitados y permisos en el Admin Console.
