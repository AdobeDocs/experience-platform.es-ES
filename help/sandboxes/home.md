---
keywords: Experience Platform;inicio;temas populares;espacio aislado;espacio aislado;prueba;Pruebas
solution: Experience Platform
title: Información general sobre zonas protegidas
description: Los zonas protegidas son particiones virtuales en una sola instancia de Experience Platform, lo que permite una integración perfecta con el proceso de desarrollo de sus aplicaciones de experiencia digital.
exl-id: b760a979-8134-4a44-8433-ec6fb49bc508
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 2%

---

# Información general de zonas protegidas

Adobe Experience Platform está diseñado para enriquecer las aplicaciones de experiencia digital a escala global. Las empresas suelen ejecutar varias aplicaciones de experiencia digital en paralelo y necesitan encargarse del desarrollo, las pruebas y la implementación de estas aplicaciones, a la vez que garantizan el cumplimiento normativo.

Para satisfacer esta necesidad, Experience Platform proporciona entornos limitados que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar aplicaciones de experiencia digital y hacer que evolucionen.

Este documento proporciona información general de alto nivel sobre los entornos limitados de Experience Platform.

## Explicación de las zonas protegidas

Los zonas protegidas son particiones virtuales en una sola instancia de Experience Platform, lo que permite una integración perfecta con el proceso de desarrollo de sus aplicaciones de experiencia digital. Todo el contenido y las acciones realizadas en una zona protegida se limitan únicamente a esa zona protegida y no afectan a ninguna otra. Existen dos tipos de zonas protegidas compatibles con Experience Platform:

* **Zona protegida de producción**: Una zona protegida de producción está pensada para utilizarse con perfiles en su entorno de producción. Experience Platform le permite crear varios entornos limitados de producción para proporcionar la funcionalidad adecuada para los datos sin perder el aislamiento operativo. Esta función le permite dedicar entornos limitados de producción específicos a distintas líneas de negocio, marcas, proyectos o regiones. Las zonas protegidas de producción admiten un volumen de perfiles de producción hasta el compromiso con licencia [!DNL Profile] (medido acumulativamente en todas las zonas protegidas de producción autorizadas). Tiene derecho a utilizar todo el volumen total de datos con licencia (medido acumulativamente en todas las zonas protegidas de producción autorizadas).

* **Entorno aislado de desarrollo**: Un entorno aislado de desarrollo es un entorno aislado que se puede usar exclusivamente para el desarrollo y las pruebas con perfiles que no sean de producción. Los entornos limitados de desarrollo admiten un volumen de perfiles que no son de producción de hasta el 10 % de la asignación [!DNL Profile] con licencia (medida de forma acumulativa en todos los entornos limitados de desarrollo autorizados). Tiene derecho a hasta:
   * Un trabajo de segmentación por lotes al día, por zona protegida de desarrollo;
   * Un promedio de 120 [!DNL Profile] llamadas de API, por [!DNL Profile], por año (medidas acumulativamente en todas sus zonas protegidas de desarrollo autorizadas).

Una instancia de Experience Platform admite varios entornos limitados de producción y desarrollo, y cada entorno limitado mantiene su propia biblioteca independiente de recursos de Experience Platform (incluidos esquemas, conjuntos de datos, perfiles, etc.). Además, tanto los entornos limitados de producción como los de desarrollo tienen una función de restablecimiento que elimina todos los recursos creados por el cliente de los entornos limitados. Las zonas protegidas de desarrollo no se pueden convertir en zonas protegidas de producción.

Una licencia predeterminada de Experience Platform le concede un total de cinco zonas protegidas, que puede clasificar como producción o desarrollo. Puede obtener una licencia de paquetes adicionales de 10 zonas protegidas, hasta un máximo de 75 zonas protegidas en total. Estos entornos limitados adicionales se pueden utilizar para crear entornos limitados de producción y desarrollo. Póngase en contacto con el administrador de su organización o con el representante de ventas de Adobe para obtener más información.

Por último, la zona protegida de producción predeterminada es la primera que se crea cuando se crea una organización por primera vez. La zona protegida de producción predeterminada le permite introducir o consumir datos de Experience Platform, así como aceptar solicitudes que no incluyen valores para un nombre de zona protegida o un ID de zona protegida.

>[!NOTE]
>
>Cuando se crea una zona protegida por primera vez, no contiene datos. Dado que cada zona protegida mantiene su propio almacén de datos aislado, también deben introducir sus datos de forma independiente.

En resumen, los entornos limitados ofrecen las siguientes ventajas:

* **Administración del ciclo de vida de las aplicaciones**: cree entornos virtuales independientes para desarrollar y desarrollar aplicaciones de experiencia digital.
* **Administración de proyectos y marcas**: permita que varios proyectos se ejecuten en paralelo dentro de la misma organización y, al mismo tiempo, proporcione aislamiento y control de acceso.
* **Ecosistema de desarrollo flexible**: proporcione zonas protegidas de una manera sencilla, escalable y rentable para fines de exploración, habilitación y demostración.

## Control de acceso para zonas protegidas

De forma predeterminada, todos los usuarios de una organización tienen acceso a una zona protegida de producción. El acceso a las zonas protegidas que no sean de producción lo debe conceder un administrador del sistema, un administrador de productos o un administrador de perfiles de productos a través de [Adobe Admin Console](https://adminconsole.adobe.com).

Para ver, crear, actualizar o eliminar zonas protegidas que no sean de producción, los usuarios también deben tener permisos de administración de zonas protegidas.

Para obtener más información sobre la administración de funciones y permisos en las zonas protegidas, consulte la [descripción general del control de acceso](../access-control/home.md).

## Zonas protegidas en la IU de Experience Platform

En la [interfaz de usuario de Experience Platform](https://platform.adobe.com), los usuarios pueden cambiar entre las zonas protegidas a las que tienen acceso mediante el control **conmutador de zonas protegidas** en la parte superior izquierda de la pantalla.  Los usuarios con privilegios de administración de zonas protegidas también tienen acceso a la pestaña **[!UICONTROL Zonas protegidas]** en el panel de navegación izquierdo, donde pueden ver y administrar las zonas protegidas de su organización. Para obtener más información sobre cómo trabajar con zonas protegidas en la interfaz de usuario, consulte la [guía del usuario de zonas protegidas](ui/overview.md).

## Zonas protegidas en las API de Experience Platform

Al realizar llamadas a las API de Experience Platform, se debe proporcionar un nombre de zona protegida en el encabezado `x-sandbox-name`. Por ejemplo, al realizar una llamada a [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) para ver todos los conjuntos de datos de la zona protegida de producción, el nombre de la zona protegida (&quot;prod&quot;) se proporciona como encabezado en la solicitud de API:

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: prod'
```

Si `x-sandbox-name` no se incluye en una llamada de API, el sistema usará una zona protegida predeterminada en su lugar. Sin embargo, la práctica recomendada es incluir siempre este encabezado en todas las llamadas a la API, incluso cuando se utilice la zona protegida predeterminada. Por este motivo, la documentación de la API para Experience Platform trata `x-sandbox-name` como un encabezado obligatorio.

### API de zona protegida

La API de espacio aislado permite administrar los espacios aislados mediante operaciones de API RESTful. Consulte la [guía para desarrolladores de espacio aislado](api/overview.md) para obtener información detallada sobre cómo usar la API, incluidas las solicitudes con formato correcto y las respuestas de ejemplo.

## Pasos siguientes

Al leer este documento, se le han presentado los conceptos esenciales sobre los entornos limitados de Experience Platform. Para ver los pasos detallados sobre cómo administrar las zonas protegidas, consulte la [guía del usuario](ui/overview.md) para la interfaz de usuario o la [guía para desarrolladores](./api/getting-started.md) para la API.

Aunque los entornos limitados sirven como una valiosa herramienta para aislar los entornos de Experience Platform de su equipo de desarrollo, también puede administrar un control de acceso más granular mediante Adobe Admin Console. Consulte la [descripción general del control de acceso](../access-control/home.md) para obtener más información.
