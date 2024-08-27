---
title: Algoritmo de optimización de identidad
description: Obtenga información acerca del algoritmo de optimización de identidad en el servicio de identidad.
badge: Beta
exl-id: 5545bf35-3f23-4206-9658-e1c33e668c98
source-git-commit: d3b43c5fa90b67bcba6015d521b78998d50cc3d7
workflow-type: tm+mt
source-wordcount: '1533'
ht-degree: 1%

---

# Algoritmo de optimización de identidad

>[!AVAILABILITY]
>
>Las reglas de vinculación de gráficos de identidad están actualmente en fase beta. Póngase en contacto con el equipo de su cuenta de Adobe para obtener información sobre los criterios de participación. La funcionalidad y la documentación están sujetas a cambios.

El algoritmo de optimización de identidad es un algoritmo gráfico del servicio de identidad que ayuda a garantizar que un gráfico de identidad sea representativo de una sola persona y, por lo tanto, evita la combinación no deseada de identidades en el perfil del cliente en tiempo real.

## Parámetros de entrada {#input-parameters}

Lea esta sección para obtener información sobre áreas de nombres únicas y prioridad de áreas de nombres. Estos dos conceptos sirven como parámetros de entrada requeridos por el algoritmo de optimización de identidad.

### Área de nombres única {#unique-namespace}

Un área de nombres única determina los vínculos que se eliminan si se contrae el gráfico.

Un solo perfil combinado y su gráfico de identidad correspondiente deben representar a un único individuo (entidad de persona). Un solo individuo suele estar representado por CRMID o ID de inicio de sesión. Se espera que no se fusionen dos personas (CRMID) en un solo perfil o gráfico.

Debe especificar qué áreas de nombres representan una entidad de persona en Identity Service mediante el algoritmo de optimización de identidad. Por ejemplo, si una base de datos CRM define una cuenta de usuario para asociarla a un único CRMID y a una sola dirección de correo electrónico, la configuración de identidad de esta zona protegida tendría este aspecto:

* Área de nombres CRMID = única
* Área de nombres de correo electrónico = única

Un área de nombres que declare única se configurará automáticamente para tener un límite máximo de uno dentro de un gráfico de identidad determinado. Por ejemplo, si declara un área de nombres CRMID como única, un gráfico de identidades solo puede tener una identidad que contenga un área de nombres CRMID. Si no declara un área de nombres como única, el gráfico puede contener más de una identidad con ese área de nombres.

>[!NOTE]
>
>* En este momento no se admite la representación de entidades del hogar (&quot;gráficos del hogar&quot;).
>
>* Todas las áreas de nombres que sean identificadores de persona y que se utilicen en la zona protegida para generar gráficos de identidad deben marcarse como un área de nombres única. De lo contrario, puede ver resultados de vinculación no deseados.

### Prioridad de área de nombres {#namespace-priority}

La prioridad del área de nombres determina cómo elimina los vínculos el algoritmo de optimización de identidad.

Los espacios de nombres del servicio de identidad tienen un orden de importancia relativo implícito. Consideremos un gráfico estructurado como una pirámide. Hay un nodo en la capa superior, dos nodos en la capa media y cuatro nodos en la capa inferior. La prioridad del área de nombres debe reflejar este orden relativo para garantizar que una entidad de persona se represente con precisión.

Para obtener información detallada sobre la prioridad del área de nombres y sus funcionalidades y usos completos, lea la [guía de prioridad del área de nombres](./namespace-priority.md).

![capas de gráficos y prioridad de área de nombres](../images/namespace-priority/graph-layers.png)

## Proceso {#process}

Al ingerir nuevas identidades, el servicio de identidad comprueba si las nuevas identidades y sus áreas de nombres correspondientes se adhieren a configuraciones de área de nombres únicas. Si se siguen las configuraciones, la ingesta continúa y las nuevas identidades se vinculan al gráfico. Sin embargo, si no se siguen las configuraciones, el algoritmo de optimización de identidad:

* Introduzca el evento más reciente, teniendo en cuenta la prioridad del área de nombres.
* Elimine el vínculo que combinaría dos entidades de persona de la capa de gráfico adecuada.

## Detalles del algoritmo de optimización de identidad

Cuando se infringe la restricción de área de nombres única, el algoritmo de optimización de identidad vuelve a reproducir los vínculos y reconstruye el gráfico desde cero.

* Los vínculos se ordenan en el siguiente orden:
   * Último evento.
   * Marca de tiempo por suma de prioridad de área de nombres (suma inferior = orden superior).
* El gráfico se restablecería en función del orden anterior. Si al agregar el vínculo se infringe la restricción del límite (por ejemplo, el gráfico contiene dos o más identidades con un área de nombres única), los vínculos se eliminan.
* El gráfico resultante será compatible con la restricción de área de nombres única que ha configurado.

![Diagrama que visualiza el algoritmo de optimización de identidad.](../images/ido_algorithm.png)

## Ejemplo de escenarios de algoritmo de optimización de identidad

En la siguiente sección se describe cómo se comporta el algoritmo de optimización de la identidad en situaciones como dispositivos compartidos o ingesta de datos con la misma marca de tiempo.

### Dispositivo compartido

Un dispositivo compartido hace referencia a un dispositivo que utilizan más de un individuo. Por ejemplo, un dispositivo compartido puede ser un portátil o una tableta que comparta con un compañero o un familiar, un equipo de biblioteca o un quiosco público.

>[!BEGINTABS]

>[!TAB Ejemplo uno]

| Área de nombres | Área de nombres única |
| --- | --- |
| CRMID | Sí |
| Correo electrónico | Sí |
| ECID | No |

En este ejemplo, tanto CRMID como Email se designan como áreas de nombres únicas. En `timestamp=0`, se incorpora un conjunto de datos de registro de CRM y se crean dos gráficos diferentes debido a la configuración del área de nombres única. Cada gráfico contiene un CRMID y un área de nombres de correo electrónico.

* `timestamp=1`: Jane inicia sesión en el sitio web de comercio electrónico con un equipo portátil. Jane está representada por su CRMID y su correo electrónico, mientras que el explorador web de su portátil que utiliza está representado por un ECID.
* `timestamp=2`: John inicia sesión en el sitio web de comercio electrónico con el mismo equipo portátil. John está representado por su CRMID y su correo electrónico, mientras que el explorador web que utilizó ya está representado por un ECID. Debido a que el mismo ECID se vincula a dos gráficos diferentes, el servicio de identidad puede saber que este dispositivo (portátil) es compartido.
* Sin embargo, debido a la configuración del área de nombres única que establece un máximo de un área de nombres CRMID y un área de nombres de correo electrónico por gráfico, el algoritmo de optimización de identidad divide el gráfico en dos.
   * Finalmente, como John es el último usuario autenticado, el ECID que representa el portátil permanece vinculado a su gráfico en lugar de al de Jane.

![caso uno del dispositivo compartido](../images/identity-settings/shared-device-case-one.png)

>[!TAB Ejemplo dos]

| Área de nombres | Área de nombres única |
| --- | --- |
| CRMID | Sí |
| ECID | No |

En este ejemplo, el área de nombres CRMID se designa como un área de nombres única.

* `timestamp=1`: Jane inicia sesión en el sitio web de comercio electrónico con un equipo portátil. Está representada por su CRMID y el explorador web del portátil está representado por el ECID.
* `timestamp=2`: John inicia sesión en el sitio web de comercio electrónico con el mismo equipo portátil. Está representado por su CRMID y el explorador web que utiliza está representado por el mismo ECID.
   * Este evento vincula dos CRMID independientes al mismo ECID, lo que supera el límite configurado de un CRMID.
   * Como resultado, el algoritmo de optimización de identidad elimina el vínculo más antiguo, que en este caso es el CRMID de Jane que se vinculó en `timestamp=1`.
   * Sin embargo, aunque el CRMID de Jane ya no existirá como gráfico en el servicio de identidad, persistirá como perfil en el perfil del cliente en tiempo real. Esto se debe a que un gráfico de identidad debe contener al menos dos identidades vinculadas y, como resultado de la eliminación de los vínculos, el CRMID de Jane ya no tiene otra identidad a la que vincular.

![shared-device-case-two](../images/identity-settings/shared-device-case-two.png)

>[!ENDTABS]

### Correo electrónico incorrecto

Hay casos en los que un usuario puede introducir valores erróneos en su correo electrónico o números de teléfono.

| Área de nombres | Área de nombres única |
| --- | --- |
| CRMID | Sí |
| Correo electrónico | Sí |
| ECID | No |

En este ejemplo, las áreas de nombres CRMID y Email se designan como únicas. Considere el caso de que Jane y John se hayan registrado en el sitio web de comercio electrónico con un valor incorrecto de correo electrónico (por ejemplo, test<span>@test.com).

* `timestamp=1`: Jane inicia sesión en su sitio web de comercio electrónico utilizando Safari en su iPhone, estableciendo su CRMID (información de inicio de sesión) y su ECID (explorador).
* `timestamp=2`: John inicia sesión en su sitio web de comercio electrónico utilizando Google Chrome en su iPhone y estableciendo su CRMID (información de inicio de sesión) y ECID (explorador).
* `timestamp=3`: el ingeniero de datos ingiere el registro CRM de Jane, lo que hace que su CRMID se vincule al correo electrónico incorrecto.
* `timestamp=4`: el ingeniero de datos ingiere el registro CRM de John, lo que hace que su CRMID se vincule al correo electrónico incorrecto.
   * Esto se convierte en una infracción de la configuración del área de nombres única, ya que crea un solo gráfico con dos áreas de nombres CRMID.
   * Como resultado, el algoritmo de optimización de identidad elimina el vínculo más antiguo, que en este caso es el vínculo entre la identidad de Jane con el área de nombres CRMID y la identidad con test<span>@test.

Con el algoritmo de optimización de identidad, los valores de identidad incorrectos, como correos electrónicos o números de teléfono falsos, no se propagan en varios gráficos de identidad diferentes.

![correo electrónico incorrecto](../images/identity-settings/bad-email.png)

### Asociación de evento anónimo

Los ECID almacenan eventos no autenticados (anónimos), mientras que CRMID almacena eventos autenticados. En el caso de los dispositivos compartidos, el ECID (portador de eventos no autenticados) se asocia con el **último usuario autenticado**.

Vea el diagrama siguiente para comprender mejor cómo funciona la asociación de eventos anónimos:

* Kevin y Nora comparten una tableta.
   * `timestamp=1`: Kevin inicia sesión en un sitio web de comercio electrónico usando su cuenta, estableciendo así su CRMID (información de inicio de sesión) y un ECID (explorador). En el momento del inicio de sesión, Kevin ahora se considera el último usuario autenticado.
   * `timestamp=2`: Nora inicia sesión en un sitio web de comercio electrónico usando su cuenta, estableciendo así su CRMID (información de inicio de sesión) y el mismo ECID. En el momento del inicio de sesión, Nora ahora se considera el último usuario autenticado.
   * `timestamp=3`: Kevin usa la tableta para examinar el sitio web de comercio electrónico, pero no inicia sesión con su cuenta. La actividad de navegación de Kevin se almacena entonces en el ECID, que a su vez se asocia con Nora porque es el último usuario autenticado. En este punto, Nora posee los eventos anónimos.
      * Hasta que Kevin vuelva a iniciar sesión, el perfil combinado de Nora se asociará a todos los eventos no autenticados almacenados con el ECID (con eventos en los que ECID es la identidad principal).
   * `timestamp=4`: Kevin inicia sesión por segunda vez. En este punto, una vez más se convierte en el último usuario autenticado y ahora también posee los eventos no autenticados:
      * Antes de su inicio de sesión anterior a `timestamp=1`; y
      * Cualquier actividad que él o Nora hicieran mientras navegaban anónimamente entre el primer y el segundo inicio de sesión de Kevin.

![anon-event-association](../images/identity-settings/anon-event-association.png)


## Pasos siguientes

Para obtener más información sobre las reglas de vinculación de gráficos de identidad, lea la siguiente documentación:

* [Resumen de reglas de vinculación de gráficos de identidad](./overview.md)
* [Prioridad de área de nombres](./namespace-priority.md)
* [Casos de ejemplo para configurar reglas de vinculación de gráficos de identidad](./example-scenarios.md)
* [Lógica de vinculación de identidad](../features/identity-linking-logic.md)
* [Servicio de identidad y perfil del cliente en tiempo real](../identity-and-profile.md)
