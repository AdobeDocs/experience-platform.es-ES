---
title: Uso de ID de dispositivos de origen en la recopilación de datos
description: Configure ID de dispositivos de origen (FPID) para la identidad duradera en implementaciones web que envían datos a Edge Network.
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1905'
ht-degree: 0%

---

# Uso de ID de dispositivos de origen en la recopilación de datos

Experience Platform Edge Network utiliza Experience Cloud ID (ECID) para identificar a los visitantes del sitio web. Para mejorar la durabilidad de la identidad en las propiedades propias, puede establecer y administrar sus propios identificadores de dispositivo, conocidos como ID de dispositivos de origen (FPID). Edge Network utiliza el FPID para iniciar el ECID que utilizan las soluciones de Adobe.

En esta página se da por hecho que está familiarizado con los ECID y `identityMap`. Consulte [Identidad en la recopilación de datos](./overview.md) para obtener más información.

## Cuándo usar FPID {#when-to-use}

Las restricciones del explorador pueden acortar la vida de las cookies que utiliza Adobe para reconocer a los visitantes que regresan. Si necesita una identidad más duradera en los sitios que su organización posee y controla, los FPID le permiten administrar su propio identificador de dispositivo y utilizarlo para iniciar el ECID.

Las FPID son compatibles con las implementaciones web que utilizan Web SDK, incluida la extensión de etiquetas de Web SDK. Son ideales cuando el objetivo principal es una mayor persistencia de la identidad en los dominios de su organización o cuando desea una mejor continuidad para la creación de informes y personalización en las propiedades web propias. También le permiten establecer y administrar una cookie de origen desde la infraestructura que controla.

Los FPID no son la herramienta correcta cuando su objetivo principal es la transferencia de aplicación a web o la continuidad de identidad en varios dominios. Para estos escenarios, vea [uso compartido de identidades entre dispositivos móviles y web](./mobile-to-web.md) y [uso compartido entre dominios](./cross-domain-sharing.md).

Los beneficios de utilizar FPID incluyen:

* Persistencia más sólida en las propiedades propias.
* Más control sobre cómo se genera y administra el identificador del dispositivo.
* Una base duradera para el análisis y la personalización.

El equilibrio entre el uso de FPID incluye:

* Más responsabilidad de la implementación que depender del comportamiento de identidad predeterminado.
* Coordinación entre la lógica de cookies del servidor y la configuración de recopilación de datos.
* Validación adicional para confirmar que el identificador se está utilizando según lo esperado.

### Ruta de configuración de alto nivel

1. Genere y administre un ID de dispositivo de origen en la infraestructura que controle.
1. Configure su implementación para que lea ese ID desde una [cookie de origen](#setting-cookie-datastreams) o desde la [carga útil de identidad](#identityMap).
1. Compruebe que los visitantes de retorno conservan una identidad coherente a lo largo del tiempo en sus propiedades.

## Cómo funcionan los FPID {#how-fpids-work}

El FPID pasado a Adobe Experience Cloud se convierte en un ECID mediante un algoritmo determinista. Cada vez que se envía el mismo FPID a Edge Network, se siembra el mismo ECID desde el FPID. Una vez que el FPID se ha utilizado para iniciar un ECID, se elimina del `identityMap` y se reemplaza por el ECID generado. FPID no se almacena en soluciones de Adobe Experience Platform o Experience Cloud.

Cuando existen un ECID y un FPID, el ECID siempre se utiliza para identificar primero al usuario. Esta priorización garantiza que, cuando un ECID existente esté presente en el almacén de cookies del explorador, siga siendo el identificador principal y que los recuentos de visitantes existentes no corran el riesgo de inflación. Para los usuarios existentes, el FPID no se convierte en la identidad principal hasta que el ECID caduca o se elimina como resultado de la política del explorador o de la acción manual.

Las identidades se priorizan en el siguiente orden:

1. ECID incluido en `identityMap`
1. ECID almacenado en una cookie
1. FPID incluido en `identityMap`
1. FPID almacenado en una cookie

## Generar y establecer la cookie FPID {#set-fpid-cookie}

Edge Network solo acepta ID que cumplan con el [formato UUIDv4](https://datatracker.ietf.org/doc/html/rfc4122). Se rechazan los ID de dispositivo que no están en formato UUIDv4.

* Los UUID son únicos y aleatorios, con una probabilidad insignificante de colisión.
* UUIDv4 no se puede inicializar mediante direcciones IP ni ninguna otra información de identificación personal (PII).
* Las bibliotecas para generar UUID están disponibles para todos los lenguajes de programación.

### Configuración de cookies del lado del servidor {#set-cookie-server}

Al configurar una cookie a través de su propio servidor, puede utilizar varios métodos para evitar que las directivas del explorador restrinjan la cookie:

* Generación de cookies mediante lenguajes de scripts del lado del servidor
* Establecer cookies en respuesta a una solicitud de API realizada a un subdominio u otro extremo del sitio
* Generación de cookies mediante un sistema de administración de contenido (CMS)
* Generación de cookies mediante una red de entrega de contenido (CDN)

Las cookies de origen son más efectivas cuando se establecen con un servidor que usa un registro DNS [A](https://datatracker.ietf.org/doc/html/rfc1035) (para IPv4) o [registro AAAA](https://datatracker.ietf.org/doc/html/rfc3596) (para IPv6), a diferencia de un código DNS `CNAME` o JavaScript.

>[!IMPORTANT]
>
>Las cookies configuradas mediante el método `document.cookie` de JavaScript (incluido el uso del método de etiqueta [`cookie.set()`](../tags/cookie.md)) casi nunca están protegidas frente a directivas de explorador que restringen la duración de las cookies.

Tenga en cuenta que los registros `A` o `AAAA` solo se admiten para configurar y rastrear cookies. El método principal para la recopilación de datos es mediante un DNS `CNAME`. Los FPID se establecen utilizando un registro `A` o `AAAA` y se envían a Adobe utilizando `CNAME`. El [programa de certificados administrados por Adobe](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program) le permite configurar un `CNAME` para la recopilación de datos.

### Cuándo se establece la cookie {#when-to-set-cookie}

La cookie FPID se establece de forma ideal antes de enviar datos a Edge Network. Si su implementación requiere consentimiento antes de recopilar datos, consulte [Consentimiento con ID de dispositivos de origen](./consent.md#consent-with-fpids) para obtener instrucciones sobre cómo coordinar la cookie FPID con el flujo de consentimiento. La inflación de visitantes se reduce cuando se asegura de que el FPID está disponible para iniciar el ECID desde la primera solicitud. En los casos en los que esto no es posible, se sigue generando un ECID con los métodos existentes y actúa como identificador principal siempre y cuando exista la cookie. El FPID generado no se convierte en el identificador principal hasta que el ECID ya no está presente. Suponiendo que el ECID se vea afectado finalmente por una política de eliminación del explorador, pero el FPID no, el FPID se convierte en el identificador principal en la siguiente visita y se utiliza para iniciar el ECID en cada visita posterior.

### Configuración de la caducidad {#set-expiration}

Adobe recomienda considerar cuidadosamente la duración de la cookie FPID. Asegúrese de tener en cuenta la política de privacidad de su organización junto con las leyes y políticas de los países o regiones en los que opera su organización. Según la configuración de su organización, puede adoptar una directiva de configuración de cookies para toda la compañía o una que varíe para los usuarios en cada configuración regional en la que trabaje. Independientemente de la caducidad inicial de la cookie, asegúrese de incluir una lógica que amplíe la caducidad cada vez que se produce una nueva visita al sitio.

### Indicadores de cookie {#cookie-flags}

Existen varios indicadores de cookies que afectan a cómo se tratan las cookies en los distintos exploradores:

* **`HTTPOnly`**: no se puede tener acceso a las cookies configuradas con el indicador `HTTPOnly` mediante scripts del lado del cliente. Esto significa que si establece un indicador `HTTPOnly` al configurar el FPID, debe utilizar un lenguaje de scripts del lado del servidor para leer el valor de la cookie para incluirlo en `identityMap`. Si elige que Edge Network lea el valor de la cookie FPID, establecer el indicador `HTTPOnly` garantiza que los scripts del lado del cliente no puedan acceder al valor, pero no afecta negativamente a la capacidad de Edge Network para leer la cookie. El uso del indicador `HTTPOnly` no afecta a las directivas de cookies que pueden restringir la duración de las cookies. Sin embargo, sigue siendo algo que hay que tener en cuenta al configurar y leer el valor del FPID.
* **`Secure`**: las cookies configuradas con el atributo `Secure` solo se envían al servidor con una solicitud cifrada a través del protocolo HTTPS. El uso de este indicador puede ayudar a garantizar que los atacantes intermediarios no puedan acceder fácilmente al valor de la cookie. Siempre que sea posible, es aconsejable establecer el indicador `Secure`.
* **`SameSite`**: el atributo `SameSite` permite a los servidores determinar si las cookies se envían con solicitudes entre sitios. El atributo proporciona cierta protección contra ataques de falsificación entre sitios. Existen tres valores posibles: `Strict`, `Lax` y `None`. Consulte con su equipo interno para determinar qué configuración es correcta para su organización. Si no se especifica ningún atributo `SameSite`, la configuración predeterminada para algunos exploradores es `SameSite=Lax`.

## Enviar el FPID a Edge Network {#send-fpid}

Puede enviar FPID a Edge Network de dos formas:

* **[Método 1](#setting-cookie-datastreams)**: configure un `CNAME` para sus llamadas de SDK web e incluya el nombre de su cookie FPID en la configuración de su secuencia de datos.
* **[Método 2](#identityMap)**: incluya el FPID en el mapa de identidad.

### Método 1: Configurar un `CNAME` y establecer una cookie de ID de origen en el conjunto de datos {#setting-cookie-datastreams}

Para establecer una cookie FPID desde su propio dominio, debe configurar su propio `CNAME` para las llamadas a SDK web y, a continuación, habilitar la funcionalidad de cookie de ID de origen en la configuración de su secuencia de datos. Un registro `CNAME` en su DNS le permite crear un alias de un nombre de dominio a otro. Este alias puede ayudar a que los servicios de terceros aparezcan como si fueran parte de su propio dominio, haciendo que sus cookies parezcan cookies de origen. Cuando la recopilación de datos de origen está habilitada mediante `CNAME`, todas las cookies del dominio se envían en solicitudes realizadas al extremo de recopilación de datos.

1. Trabaje con Adobe para crear un registro `CNAME` para la recopilación de datos que utilizará en su organización. Consulte el [programa de certificados administrados por Adobe](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/adobe-managed-cert) para ver el proceso completo.
1. Habilite la opción **[!UICONTROL First Party ID Cookie]** en su secuencia de datos. Esta configuración indica a Edge Network que haga referencia a la cookie especificada al buscar un ID de dispositivo de origen en lugar de buscar el valor en el mapa de identidad. Al habilitar esta configuración, debe proporcionar el nombre de la cookie donde se espera que se almacene el FPID. Consulte [Crear y configurar flujos de datos](/help/datastreams/configure.md#advanced-options) para obtener más información.

   ![Imagen de la interfaz de usuario de la plataforma que muestra la configuración de secuencia de datos destacando la configuración de cookie de ID de origen](/help/collection/js/assets/first-party-id-datastreams.png)

### Método 2: usar FPID en `identityMap` {#identityMap}

Como alternativa al almacenamiento del FPID en su propia cookie, puede enviar el FPID a Edge Network a través del mapa de identidad.

A continuación se muestra un ejemplo de cómo establecer un FPID en `identityMap`:

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": true
      }
    ]
  }
}
```

Al igual que con otros tipos de identidad, puede incluir el FPID con otras identidades dentro de `identityMap`. El siguiente ejemplo incluye el FPID con un ID de CRM autenticado:

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": false
      }
    ],
    "EMAIL": [
      {
        "id": "user@example.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

Si el FPID está contenido en una cookie que está leyendo Edge Network cuando la recopilación de datos de origen está habilitada, capture solo el ID de CRM autenticado:

```json
{
  "identityMap": {
    "EMAIL": [
      {
        "id": "user@example.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

Los(as) siguientes `identityMap` resultan en una respuesta de error de Edge Network porque le falta el indicador `primary` para el FPID. Al menos uno de los identificadores presentes en `identityMap` debe marcarse como `primary`.

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-12d3-a456-426614174000",
        "authenticatedState": "ambiguous"
      }
    ],
    "EMAIL": [
      {
        "id": "user@example.com",
        "authenticatedState": "authenticated"
      }
    ]
  }
}
```

## Migración a FPID {#migrating-to-fpid}

Si está migrando a ID de dispositivos de origen desde una implementación anterior, puede resultar difícil visualizar el aspecto que podría tener la transición en un nivel bajo. Para ilustrar este proceso, considere un escenario que implique a un cliente que haya visitado anteriormente su sitio y el impacto que una migración de FPID tendría en cómo se identifica ese cliente en las soluciones de Adobe.

![Diagrama que muestra cómo se actualizan los valores de ID de un cliente entre visitas después de migrar a FPID](/help/collection/js/assets/identity/tracking/visits.png)

| Visita | Descripción |
| --- | --- |
| Primera visita | Supongamos que aún no ha empezado a configurar la cookie FPID. El ECID contenido en la [cookie AMCV](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8) es el identificador usado para identificar al visitante. |
| Segunda visita | Se ha iniciado el despliegue de la solución FPID. El ECID existente sigue presente y sigue siendo el identificador principal para la identificación del visitante. |
| Tercera visita | Entre la segunda y la tercera visita, ha transcurrido tiempo suficiente para que el ECID se haya eliminado debido a la política del explorador. Sin embargo, dado que el FPID se estableció mediante un registro `A` DNS, el FPID persiste. El FPID ahora se considera el ID principal y se utiliza para inicializar el ECID, que se escribe en el dispositivo del usuario final. Ahora se considera un nuevo visitante en las soluciones Adobe Experience Platform y Experience Cloud. |
| Cuarta visita | Entre la tercera y la cuarta visita, ha transcurrido tiempo suficiente para que el ECID se haya eliminado debido a la política del explorador. Al igual que la visita anterior, el FPID se mantiene debido a la forma en que se estableció. Esta vez, se genera el mismo ECID que la visita anterior. El usuario se ve en todas las soluciones de Adobe Experience Platform y Experience Cloud como el mismo usuario de la visita anterior. |
| Quinta visita | Entre la cuarta y la quinta visita, el usuario final borró todas las cookies del explorador. Se genera un nuevo FPID y se utiliza para iniciar la creación de un nuevo ECID. Ahora se considera un nuevo visitante en las soluciones Adobe Experience Platform y Experience Cloud. |
