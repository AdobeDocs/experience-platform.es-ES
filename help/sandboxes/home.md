---
keywords: Experience Platform;inicio;temas populares;zona de pruebas;zona de pruebas;pruebas;Pruebas
solution: Experience Platform
title: Información general de los Simuladores de pruebas
topic: overview
description: Los Simuladores de pruebas son particiones virtuales dentro de una sola instancia de Experience Platform, que permiten una integración sin fisuras con el proceso de desarrollo de las aplicaciones de experiencia digital.
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 0%

---


# Descripción general de los Simuladores para pruebas

Adobe Experience Platform está diseñado para enriquecer las aplicaciones de experiencia digital a escala global. Las compañías suelen ejecutar varias aplicaciones de experiencia digital en paralelo y deben encargarse del desarrollo, la prueba y la implementación de estas aplicaciones al mismo tiempo que garantizan el cumplimiento de normas operacionales.

Para satisfacer esta necesidad, Experience Platform proporciona entornos limitados que dividen una instancia de plataforma única en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Este documento proporciona información general de alto nivel sobre los entornos limitados en Experience Platform.

## Aspectos básicos de los entornos limitados

Los Simuladores de pruebas son particiones virtuales dentro de una sola instancia de Experience Platform, que permiten una integración sin fisuras con el proceso de desarrollo de las aplicaciones de experiencia digital. Una instancia de Experience Platform admite un entorno limitado de producción y varios entornos limitados que no sean de producción, y cada entorno limitado mantiene su propia biblioteca independiente de recursos de la Plataforma (incluidos esquemas, conjuntos de datos, perfiles, etc.).  Todo el contenido y las acciones realizadas dentro de un entorno limitado solo se limitan a ese entorno limitado y no afectan a ningún otro entorno limitado.

Los entornos limitados que no son de producción le permiten probar características, ejecutar experimentos y realizar configuraciones personalizadas sin afectar al entorno limitado de producción. Además, los entornos limitados que no son de producción tienen una función de restablecimiento que elimina todos los recursos creados por el cliente del entorno limitado. Los entornos limitados que no son de producción no se pueden convertir en entornos limitados de producción. Una licencia de Experience Platform predeterminada le otorga cinco entornos limitados (una producción y cuatro no producción). Puede agregar paquetes de diez entornos limitados sin producción hasta un máximo de 75 entornos limitados en total. Póngase en contacto con el administrador de la organización IMS o con el representante de ventas de Adobe para obtener más información.

>[!NOTE]
>
>Cuando se crea un simulador para pruebas por primera vez, no contiene ningún dato. Dado que cada simulador de pruebas mantiene su propio almacén de datos aislado, también deben ingestar sus datos de forma independiente.

En resumen, los entornos limitados proporcionan las siguientes ventajas:

* **Administración** del ciclo vital de las aplicaciones: Cree entornos virtuales independientes para desarrollar y desarrollar aplicaciones de experiencia digital.
* **Gestión** de proyectos y marcas: Permita que varios proyectos se ejecuten en paralelo dentro de la misma organización de IMS, al tiempo que proporciona aislamiento y control de acceso. Las próximas versiones serán compatibles con la implementación en varias regiones.
* **Ecosistema** de desarrollo flexible: Proporcione entornos limitados de una manera transparente, escalable y rentable para fines de exploración, habilitación y demostración.

## Control de acceso para entornos limitados

De forma predeterminada, todos los usuarios de una organización tienen acceso a un entorno limitado de producción. Un administrador del sistema, un administrador de productos o un administrador de perfil de productos debe otorgar acceso a entornos limitados que no sean de producción a través de [Adobe Admin Console](https://adminconsole.adobe.com).

Para poder vista, crear, actualizar o eliminar entornos limitados que no sean de producción, también se deben otorgar a los usuarios permisos de administración de Simuladores para pruebas.

Para obtener más información sobre la administración de funciones y permisos para entornos limitados, consulte la [información general de control de acceso](../access-control/home.md).

## Entornos aislados en la interfaz de usuario del Experience Platform

En la [interfaz de usuario del Experience Platform](https://platform.adobe.com), los usuarios pueden cambiar entre los entornos limitados a los que tienen acceso mediante el control **simulador de pruebas** en la parte superior izquierda de la pantalla.  Los usuarios con privilegios de administración de Simulador para pruebas también tienen acceso a la ficha **[!UICONTROL Simuladores para pruebas]** en la navegación izquierda, donde pueden realizar vistas y administrar entornos limitados para su organización. Para obtener más información sobre cómo trabajar con los entornos limitados en la interfaz de usuario, consulte la [guía del usuario del entorno limitado](ui/overview.md).

## Simuladores de pruebas en API de Experience Platform

Al realizar llamadas a API de Experience Platform, se debe proporcionar un nombre de simulador de pruebas en el encabezado `x-sandbox-name`. Por ejemplo, al realizar una llamada a [[!DNL Catalog Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) para la vista de todos los conjuntos de datos dentro del entorno limitado de producción, el nombre del entorno limitado (&quot;prod&quot;) se proporciona como encabezado en la solicitud de API:

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: prod'
```

Si `x-sandbox-name` no se incluye en una llamada de API, el sistema utilizará un entorno limitado predeterminado. Sin embargo, lo mejor es incluir siempre este encabezado en todas las llamadas de API, incluso cuando se utiliza el entorno limitado predeterminado. Por este motivo, la documentación de API para Experience Platform trata a `x-sandbox-name` como un encabezado requerido.

### API de Simulador para pruebas

La API de Simulador para pruebas le permite administrar entornos limitados mediante operaciones de API de RESTful. Consulte la [guía para desarrolladores de simuladores de pruebas](api/getting-started.md) para obtener información detallada sobre cómo utilizar la API, incluidas las solicitudes formateadas correctamente y las respuestas de ejemplo.

## Pasos siguientes

Al leer este documento, se le han presentado los conceptos esenciales de los entornos limitados en Experience Platform. Para ver los pasos detallados sobre cómo administrar los entornos limitados, consulte la [guía del usuario](ui/overview.md) para la interfaz de usuario o la [guía para desarrolladores](./api/getting-started.md) para la API.

Aunque los entornos limitados sirven como una valiosa herramienta para aislar los entornos de la plataforma para su equipo de desarrollo, también puede administrar controles de acceso más granulares mediante Adobe Admin Console. Consulte la [información general del control de acceso](../access-control/home.md) para obtener más información.