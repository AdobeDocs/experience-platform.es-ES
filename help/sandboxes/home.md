---
keywords: Experience Platform;inicio;temas populares;Sandbox;Sandbox;pruebas;Pruebas
solution: Experience Platform
title: Información general de entornos limitados
topic: sobre validación
description: Los entornos limitados son particiones virtuales dentro de una sola instancia de Experience Platform, lo que permite una integración perfecta con el proceso de desarrollo de las aplicaciones de experiencia digital.
translation-type: tm+mt
source-git-commit: ee2fb54ba59f22a1ace56a6afd78277baba5271e
workflow-type: tm+mt
source-wordcount: '778'
ht-degree: 0%

---


# Información general sobre Sandboxes

Adobe Experience Platform está diseñado para enriquecer las aplicaciones de experiencia digital a escala global. A menudo, las empresas ejecutan varias aplicaciones de experiencia digital en paralelo y deben encargarse del desarrollo, las pruebas y la implementación de estas aplicaciones, asegurando al mismo tiempo el cumplimiento de las normas operacionales.

Para satisfacer esta necesidad, Experience Platform proporciona entornos limitados que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Este documento proporciona información general de alto nivel sobre los entornos limitados en Experience Platform.

## Aspectos básicos de los entornos limitados

>[!NOTE]
>
>La función Entornos aislados de producción múltiple está en fase beta.

Los entornos limitados son particiones virtuales dentro de una sola instancia de Experience Platform, lo que permite una integración perfecta con el proceso de desarrollo de las aplicaciones de experiencia digital. Una instancia de Experience Platform admite varios entornos limitados de producción y sin producción, y cada entorno limitado mantiene su propia biblioteca independiente de recursos de Platform (incluidos esquemas, conjuntos de datos, perfiles, etc.). Todo el contenido y las acciones realizadas dentro de un simulador de pruebas solo se limitan a ese simulador de pruebas y no afectan a ningún otro simulador de pruebas.

Los entornos limitados que no son de producción le permiten probar características, ejecutar experimentos y realizar configuraciones personalizadas sin afectar a su entorno limitado de producción. Además, tanto los entornos limitados de producción como los que no son de producción tienen una función de restablecimiento que elimina todos los recursos creados por el cliente del entorno limitado. Los entornos limitados que no sean de producción no se pueden convertir en entornos limitados de producción. Una licencia de Experience Platform predeterminada le otorga cinco entornos limitados (una producción y cuatro no producción). Puede agregar paquetes de diez entornos limitados hasta un máximo de 75 entornos limitados en total. Estos entornos limitados adicionales se pueden usar para crear entornos limitados de producción y sin producción. Póngase en contacto con su administrador de organización de IMS o con su representante de ventas de Adobe para obtener más información.

>[!NOTE]
>
>Cuando se crea un simulador para pruebas por primera vez, no contiene datos. Dado que cada simulador de pruebas mantiene su propio almacén de datos aislado, también deben introducir sus datos de forma independiente.

En resumen, los entornos limitados ofrecen las siguientes ventajas:

* **Administración del ciclo de vida de las aplicaciones**: Cree entornos virtuales independientes para desarrollar y desarrollar aplicaciones de experiencia digital.
* **Administración de proyectos y marcas**: Permita que varios proyectos se ejecuten en paralelo dentro de la misma organización de IMS, al mismo tiempo que proporciona aislamiento y control de acceso. Las futuras versiones serán compatibles con la implementación en varias regiones.
* **ecosistema** de desarrollo flexible: Proporcionar entornos limitados de manera fácil, escalable y rentable para fines de exploración, habilitación y demostración.

## Control de acceso para entornos limitados

De forma predeterminada, todos los usuarios de una organización tienen acceso a un simulador para pruebas de producción. El acceso a los entornos limitados que no sean de producción debe ser otorgado por un administrador del sistema, un administrador de productos o un administrador de perfiles de productos a través de [Adobe Admin Console](https://adminconsole.adobe.com).

Para ver, crear, actualizar o eliminar entornos limitados de producción y que no sean de producción, también se deben otorgar permisos de administración de entornos limitados a los usuarios.

Para obtener más información sobre la administración de funciones y permisos para entornos limitados, consulte la [información general del control de acceso](../access-control/home.md).

## Sandboxes en la interfaz de usuario del Experience Platform

En la [interfaz de usuario del Experience Platform](https://platform.adobe.com), los usuarios pueden cambiar entre los entornos limitados a los que tienen acceso mediante el control **sandbox switch** en la parte superior izquierda de la pantalla.  Los usuarios con privilegios de administración de espacio aislado también tienen acceso a la pestaña **[!UICONTROL Sandboxes]** en la navegación izquierda, donde pueden ver y administrar entornos limitados para su organización. Para obtener más información sobre cómo trabajar con entornos limitados en la interfaz de usuario, consulte la [guía del usuario del entorno limitado](ui/overview.md).

## Sandboxes en las API de Experience Platform

Al realizar llamadas a las API de Experience Platform, se debe proporcionar un nombre de simulador de pruebas en el encabezado `x-sandbox-name`. Por ejemplo, al realizar una llamada a [[!DNL Catalog Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) para ver todos los conjuntos de datos dentro del entorno limitado de producción, el nombre del entorno limitado (&quot;prod&quot;) se proporciona como un encabezado en la solicitud de API:

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: prod'
```

Si `x-sandbox-name` no está incluido en una llamada de API, el sistema usará un entorno limitado predeterminado en su lugar. Sin embargo, la práctica recomendada es incluir siempre este encabezado en todas las llamadas a la API, incluso cuando se utilice el entorno limitado predeterminado. Por este motivo, la documentación de API para el Experience Platform trata a `x-sandbox-name` como un encabezado obligatorio.

### API de Sandbox

La API de espacio aislado permite administrar entornos limitados mediante operaciones de API RESTful. Consulte la [guía para desarrolladores de entornos limitados](api/getting-started.md) para obtener información detallada sobre cómo utilizar la API, incluidas las solicitudes con formato correcto y las respuestas de ejemplo.

## Pasos siguientes

Al leer este documento, se le han introducido los conceptos esenciales sobre los entornos limitados en Experience Platform. Para ver los pasos detallados sobre cómo administrar entornos limitados, consulte la [guía del usuario](ui/overview.md) para la interfaz de usuario o la [guía para desarrolladores](./api/getting-started.md) para la API.

Aunque los entornos limitados sirven como una valiosa herramienta para aislar los entornos de Platform para su equipo de desarrollo, también puede administrar un control de acceso más granular mediante Adobe Admin Console. Consulte la [descripción general del control de acceso](../access-control/home.md) para obtener más información.