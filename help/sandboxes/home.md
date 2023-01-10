---
keywords: Experience Platform;inicio;temas populares;Sandbox;Sandbox;pruebas;Pruebas
solution: Experience Platform
title: Información general de entornos limitados
description: Los entornos limitados son particiones virtuales dentro de una sola instancia de Experience Platform, lo que permite una integración perfecta con el proceso de desarrollo de las aplicaciones de experiencia digital.
exl-id: b760a979-8134-4a44-8433-ec6fb49bc508
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 0%

---

# Información general sobre Sandboxes

Adobe Experience Platform está diseñado para enriquecer las aplicaciones de experiencia digital a escala global. A menudo, las empresas ejecutan varias aplicaciones de experiencia digital en paralelo y deben encargarse del desarrollo, las pruebas y la implementación de estas aplicaciones, asegurando al mismo tiempo el cumplimiento de las normas operacionales.

Para satisfacer esta necesidad, Experience Platform proporciona entornos limitados que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Este documento proporciona información general de alto nivel sobre los entornos limitados en Experience Platform.

## Aspectos básicos de los entornos limitados

Los entornos limitados son particiones virtuales dentro de una sola instancia de Experience Platform, lo que permite una integración perfecta con el proceso de desarrollo de las aplicaciones de experiencia digital. Todo el contenido y las acciones realizadas dentro de un simulador de pruebas solo se limitan a ese simulador de pruebas y no afectan a ningún otro simulador de pruebas. El Experience Platform admite dos tipos de entornos limitados:

* **Espacio aislado de producción**: Un simulador para pruebas de producción está diseñado para utilizarse con perfiles en el entorno de producción. Platform le permite crear varios entornos limitados de producción para proporcionar la funcionalidad adecuada a los datos sin dejar de mantener el aislamiento operativo. Esta función le permite dedicar entornos limitados de producción específicos a distintas líneas de negocio, marcas, proyectos o regiones. Los entornos limitados de producción admiten un volumen de perfiles de producción hasta la licencia [!DNL Profile] compromiso (medido acumulativamente en todos los entornos limitados de producción autorizados). Tiene derecho a usar un perfil promedio autorizado por cada [!DNL Profile] (medida acumulativamente en todos los entornos limitados de producción autorizados).
* **Entornos aislados de desarrollo**: Un entorno limitado de desarrollo es un entorno limitado que se puede utilizar exclusivamente para desarrollo y pruebas con perfiles que no sean de producción. Los entornos limitados de desarrollo admiten un volumen de perfiles que no son de producción de hasta el 10% de las licencias [!DNL Profile] compromiso (medido acumulativamente en todos los entornos limitados de desarrollo autorizados). Tiene derecho a:
   * Una riqueza media de perfil no productiva de 75 kilobytes por perfil no de producción autorizado (medida acumulativamente en todos los entornos limitados de desarrollo autorizados);
   * Un trabajo de segmentación por lotes al día, por simulador de pruebas de desarrollo;
   * Un promedio de 120 [!DNL Profile] llamadas de API, por [!DNL Profile], por año (se mide acumulativamente en todos los entornos limitados de desarrollo autorizados.

Una instancia de Experience Platform admite varios entornos limitados de producción y desarrollo, y cada entorno limitado mantiene su propia biblioteca independiente de recursos de Platform (incluidos esquemas, conjuntos de datos, perfiles, etc.). Además, tanto los entornos limitados de producción como los de desarrollo tienen una función de restablecimiento que elimina todos los recursos creados por el cliente del entorno limitado. Los entornos limitados de desarrollo no se pueden convertir en entornos limitados de producción.

Una licencia de Experience Platform predeterminada le otorga un total de cinco entornos limitados, que puede clasificar como de producción o desarrollo. Puede obtener una licencia de paquetes adicionales de 10 entornos limitados hasta un máximo de 75 entornos limitados en total. Estos entornos limitados adicionales se pueden usar para crear entornos limitados de producción y desarrollo. Póngase en contacto con su administrador de organización de IMS o con su representante de ventas de Adobe para obtener más información.

Por último, el entorno limitado de producción predeterminado es el primer entorno limitado de producción que se crea al crear una organización de IMS por primera vez. El entorno limitado de producción predeterminado le permite ingerir o consumir datos de Platform, así como aceptar solicitudes que no incluyan valores para un nombre de entorno limitado o un ID de simulador de pruebas.

>[!NOTE]
>
>Cuando se crea un simulador para pruebas por primera vez, no contiene datos. Dado que cada simulador de pruebas mantiene su propio almacén de datos aislado, también deben introducir sus datos de forma independiente.

En resumen, los entornos limitados ofrecen las siguientes ventajas:

* **Administración del ciclo de vida de las aplicaciones**: Cree entornos virtuales independientes para desarrollar y desarrollar aplicaciones de experiencia digital.
* **Administración de proyectos y marcas**: Permita que varios proyectos se ejecuten en paralelo dentro de la misma organización de IMS, al mismo tiempo que proporciona aislamiento y control de acceso. Las futuras versiones serán compatibles con la implementación en varias regiones.
* **ecosistema de desarrollo flexible**: Proporcionar entornos limitados de manera fácil, escalable y rentable para fines de exploración, habilitación y demostración.

## Control de acceso para entornos limitados

De forma predeterminada, todos los usuarios de una organización tienen acceso a un simulador para pruebas de producción. El acceso a los entornos limitados que no sean de producción debe ser otorgado por un administrador del sistema, un administrador de productos o un administrador de perfiles de productos a través de la variable [Adobe Admin Console](https://adminconsole.adobe.com).

Para ver, crear, actualizar o eliminar entornos limitados que no sean de producción, también se deben otorgar permisos de administración de entornos limitados a los usuarios.

Para obtener más información sobre la administración de funciones y permisos para entornos limitados, consulte la [información general sobre el control de acceso](../access-control/home.md).

## Sandboxes en la interfaz de usuario del Experience Platform

En el [interfaz de usuario del Experience Platform](https://platform.adobe.com), los usuarios pueden cambiar entre los entornos limitados a los que tienen acceso mediante el **conmutador de simulador de pruebas** en la parte superior izquierda de la pantalla.  Los usuarios con privilegios de administración de espacio aislado también tienen acceso al **[!UICONTROL Sandboxes]** en la sección de navegación izquierda, donde pueden ver y administrar entornos limitados para su organización. Para obtener más información sobre cómo trabajar con entornos limitados en la interfaz de usuario, consulte la [guía del usuario de sandbox](ui/overview.md).

## Sandboxes en las API de Experience Platform

Al realizar llamadas a las API de Experience Platform, se debe proporcionar un nombre de simulador de pruebas en el encabezado `x-sandbox-name`. Por ejemplo, al realizar una llamada a la función [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) para ver todos los conjuntos de datos dentro del entorno limitado de producción, el nombre del entorno limitado (&quot;prod&quot;) se proporciona como un encabezado en la solicitud de API:

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: prod'
```

If `x-sandbox-name` no se incluye en una llamada de API, el sistema utilizará un simulador para pruebas predeterminado. Sin embargo, la práctica recomendada es incluir siempre este encabezado en todas las llamadas a la API, incluso cuando se utilice el entorno limitado predeterminado. Por este motivo, la documentación de la API para el tratamiento del Experience Platform `x-sandbox-name` como encabezado obligatorio.

### API de Sandbox

La API de espacio aislado permite administrar entornos limitados mediante operaciones de API RESTful. Consulte la [guía para desarrolladores de sandbox](api/overview.md) para obtener información detallada sobre cómo utilizar la API, incluidas las solicitudes con formato correcto y las respuestas de ejemplo.

## Pasos siguientes

Al leer este documento, se le han introducido los conceptos esenciales sobre los entornos limitados en Experience Platform. Para ver los pasos detallados sobre cómo administrar entornos limitados, consulte la [guía del usuario](ui/overview.md) para la interfaz de usuario o el [guía para desarrolladores](./api/getting-started.md) para la API.

Aunque los entornos limitados sirven como una valiosa herramienta para aislar los entornos de Platform para su equipo de desarrollo, también puede administrar un control de acceso más granular mediante Adobe Admin Console. Consulte la [información general sobre el control de acceso](../access-control/home.md) para obtener más información.
