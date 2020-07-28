---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Descripción general de los Simuladores para pruebas
topic: overview
translation-type: tm+mt
source-git-commit: c52d8cdbc5a4ee6fab8c2b1b284efea5f735d424
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 0%

---


# Descripción general de los Simuladores para pruebas

Adobe Experience Platform está diseñado para enriquecer las aplicaciones de experiencia digital a escala global. Las Compañías suelen ejecutar varias aplicaciones de experiencia digital en paralelo y deben encargarse del desarrollo, la prueba y la implementación de estas aplicaciones al mismo tiempo que garantizan el cumplimiento de normas operacionales.

Para satisfacer esta necesidad, Experience Platform proporciona **entornos** limitados que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Este documento proporciona información general de alto nivel sobre los entornos limitados en Experience Platform.

## Aspectos básicos de los entornos limitados

Los Simuladores de pruebas son particiones virtuales dentro de una sola instancia de Experience Platform, que permiten una integración sin fisuras con el proceso de desarrollo de las aplicaciones de experiencia digital. Una instancia de Experience Platform admite un entorno limitado de producción y varios entornos limitados que no sean de producción, y cada entorno limitado mantiene su propia biblioteca independiente de recursos de Platform (incluidos esquemas, conjuntos de datos, perfiles, etc.).  Todo el contenido y las acciones realizadas dentro de un entorno limitado solo se limitan a ese entorno limitado y no afectan a ningún otro entorno limitado.

Los entornos limitados que no son de producción le permiten probar características, ejecutar experimentos y realizar configuraciones personalizadas sin afectar al entorno limitado de producción. Además, los entornos limitados que no son de producción tienen una función de restablecimiento que elimina todos los recursos creados por el cliente del entorno limitado. Los entornos limitados que no son de producción no se pueden convertir en entornos limitados de producción.

>[!NOTE]
>
>Cuando se crea un simulador para pruebas por primera vez, no contiene ningún dato. Dado que cada simulador de pruebas mantiene su propio almacén de datos aislado, también deben ingestar sus datos de forma independiente.

En resumen, los entornos limitados proporcionan las siguientes ventajas:

* **Administración** del ciclo vital de las aplicaciones: Cree entornos virtuales independientes para desarrollar y desarrollar aplicaciones de experiencia digital.
* **Gestión** de proyectos y marcas: Permita que varios proyectos se ejecuten en paralelo dentro de la misma organización de IMS, al tiempo que proporciona aislamiento y control de acceso. Las próximas versiones serán compatibles con la implementación en varias regiones.
* **Ecosistema** de desarrollo flexible: Proporcione entornos limitados de una manera transparente, escalable y rentable para fines de exploración, habilitación y demostración.

## Control de acceso para entornos limitados

De forma predeterminada, todos los usuarios de una organización tienen acceso a un entorno limitado de producción. Un administrador del sistema, un administrador de productos o un administrador de perfil de productos deben otorgar acceso a los entornos limitados que no sean de producción a través de [Adobe Admin Console](https://adminconsole.adobe.com).

Para poder vista, crear, actualizar o eliminar entornos limitados que no sean de producción, también se deben otorgar a los usuarios permisos de administración de Simuladores para pruebas.

Para obtener más información sobre la administración de funciones y permisos para entornos limitados, consulte la descripción general [del](../access-control/home.md)control de acceso.

## Entornos aislados en la interfaz de usuario del Experience Platform

En la interfaz [de usuario del](https://platform.adobe.com)Experience Platform, los usuarios pueden cambiar entre los entornos limitados a los que tienen acceso mediante el control del conmutador **de** simulador de pruebas en la parte superior izquierda de la pantalla.  Los usuarios con privilegios de administración de Simuladores para pruebas también tienen acceso a la ficha **[!UICONTROL Entornos]** para pruebas de la izquierda, donde pueden realizar vistas y administrar entornos limitados para su organización. Para obtener más información sobre cómo trabajar con los entornos limitados en la interfaz de usuario, consulte la guía [del usuario del](ui/overview.md)simulador de pruebas.

## Simuladores de pruebas en API de Experience Platform

Al realizar llamadas a API de Experience Platform, se debe proporcionar un nombre de simulador de pruebas en el encabezado `x-sandbox-name`. Por ejemplo, al realizar una llamada a la [!DNL Catalog Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) para que vista todos los conjuntos de datos dentro del entorno limitado de producción, el nombre del entorno limitado (&quot;prod&quot;) se proporciona como encabezado en la solicitud de API:

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: prod'
```

Si no `x-sandbox-name` se incluye en una llamada de API, el sistema utilizará un entorno limitado predeterminado. Sin embargo, lo mejor es incluir siempre este encabezado en todas las llamadas de API, incluso cuando se utiliza el entorno limitado predeterminado. Por este motivo, la documentación de API para Experience Platform se considera `x-sandbox-name` como un encabezado obligatorio.

### API de Simulador para pruebas

La API de Simulador para pruebas le permite administrar entornos limitados mediante operaciones de API de RESTful. Consulte la guía [para desarrolladores de](api/getting-started.md) simuladores de pruebas para obtener información detallada sobre cómo utilizar la API, incluidas las solicitudes con el formato adecuado y las respuestas de ejemplo.

## Pasos siguientes

Al leer este documento, se le han presentado los conceptos esenciales de los entornos limitados en Experience Platform. Para ver los pasos detallados sobre cómo administrar los entornos limitados, consulte la guía [de](ui/overview.md) usuario de la interfaz de usuario o la guía [para](./api/getting-started.md) desarrolladores de la API.

Aunque los entornos limitados son una herramienta valiosa para aislar entornos de Platform para su equipo de desarrollo, también puede administrar un control de acceso más granular mediante Adobe Admin Console. Consulte la descripción general [del](../access-control/home.md) control de acceso para obtener más información.