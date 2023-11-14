---
title: Algoritmo de optimización de identidad
description: Obtenga información acerca del algoritmo de optimización de identidad en el servicio de identidad.
hide: true
hidefromtoc: true
badge: Alfa
source-git-commit: 8f99dc633c87fa36cc0c5413d23b97b4fce7dbc3
workflow-type: tm+mt
source-wordcount: '1319'
ht-degree: 2%

---

# Algoritmo de optimización de identidad

>[!IMPORTANT]
>
>El algoritmo de optimización de identidad está en Alpha. La funcionalidad y la documentación están sujetas a cambios.

El algoritmo de optimización de identidad es una regla que ayuda a garantizar que un gráfico de identidad sea representativo de una sola persona y, por lo tanto, evita la combinación no deseada de identidades en el perfil del cliente en tiempo real.

## Parámetros de entrada

Un solo perfil combinado y su gráfico de identidad correspondiente deben representar a un único individuo (entidad de persona). Un solo individuo suele estar representado por ID de CRM o ID de inicio de sesión. Se espera que no se combinen dos personas (ID de CRM) en un solo perfil o gráfico.

Debe especificar qué áreas de nombres representan una entidad de persona en Identity Service mediante el algoritmo de optimización de identidad. Por ejemplo, si una base de datos de CRM define una cuenta de usuario que se asociará con un único ID de CRM y una sola dirección de correo electrónico, la configuración de identidad para esta zona protegida tendría este aspecto:

* Área de nombres de ID de CRM = única
* Área de nombres de correo electrónico = única

Un área de nombres que declare única se configurará automáticamente para tener un límite máximo de uno dentro de un gráfico de identidad determinado. Por ejemplo, si declara un área de nombres de ID de CRM como única, un gráfico de identidades solo puede tener una identidad que contenga un área de nombres de ID de CRM.

>[!NOTE]
>
>* Actualmente, el algoritmo solo admite el uso de un único identificador de inicio de sesión (un área de nombres de inicio de sesión). En este momento no se admiten varios identificadores de inicio de sesión (se usan varias áreas de nombres de identidad para iniciar sesión), gráficos de entidades domésticas y estructuras de gráficos jerárquicos.
>
>* Todas las áreas de nombres que sean identificadores de persona y que se utilicen en la zona protegida para generar gráficos de identidad deben marcarse como un área de nombres única. De lo contrario, puede ver resultados de vinculación no deseados.

## Proceso

Al ingerir nuevas identidades, el servicio de identidad comprueba si las nuevas identidades y sus áreas de nombres correspondientes superarán los límites configurados. Si no se superan los límites, la ingesta de nuevas identidades se realizará y estas identidades se vincularán al gráfico. Sin embargo, si se superan los límites, el algoritmo de optimización de la identidad actualizará el gráfico de modo que se respete la marca de tiempo más reciente y se eliminen los vínculos más antiguos con las áreas de nombres de prioridad inferior.

## Ejemplo de escenarios de algoritmo de optimización de identidad

En la siguiente sección se describe cómo se comporta el algoritmo de optimización de la identidad en situaciones como dispositivos compartidos o ingesta de datos con la misma marca de tiempo.

### Dispositivo compartido

Un dispositivo compartido hace referencia a un dispositivo que utilizan más de un individuo. Por ejemplo, un dispositivo compartido puede ser un portátil o una tableta que comparta con un compañero o un familiar, un equipo de biblioteca o un quiosco público.

>[!BEGINTABS]

>[!TAB Ejemplo 1]

| Área de nombres | Límite |
| --- | --- |
| ID de CRM | 1 |
| Correo electrónico | 1 |
| ECID | N/A |

En este ejemplo, tanto el ID de CRM como el correo electrónico se designan como áreas de nombres únicas. En `timestamp=0`, se incorpora un conjunto de datos de registro CRM y se crean dos gráficos diferentes debido a la configuración de límite. Cada gráfico contiene un ID de CRM y un área de nombres de correo electrónico.

* `timestamp=1`: Jane inicia sesión en su sitio web de comercio electrónico con un ordenador portátil. Jane está representada por su ID de CRM y su correo electrónico, mientras que el explorador web de su portátil que utiliza está representado por un ECID.
* `timestamp=2`: John inicia sesión en el sitio web de comercio electrónico con el mismo equipo portátil. John está representado por su ID de CRM y su correo electrónico, mientras que el explorador web que utilizó ya está representado por un ECID. Debido a que el mismo ECID se vincula a dos gráficos diferentes, el servicio de identidad puede saber que este dispositivo (portátil) es compartido.
* Sin embargo, debido a la configuración de límite que establece un máximo de un área de nombres de ID de CRM y un área de nombres de correo electrónico por gráfico, el algoritmo de optimización de identidad divide el gráfico en dos.
   * Finalmente, como John es el último usuario autenticado, el ECID que representa el portátil permanece vinculado a su gráfico en lugar de al de Jane.

![caso uno del dispositivo compartido](../images/identity-settings/shared-device-case-one.png)

>[!TAB Ejemplo dos]

| Área de nombres | Límite |
| --- | --- |
| ID de CRM | 1 |
| ECID | N/A |

En este ejemplo, el área de nombres de ID de CRM se designa como un área de nombres única.

* `timestamp=1`: Jane inicia sesión en su sitio web de comercio electrónico con un ordenador portátil. Está representada por su ID de CRM y el explorador web del portátil está representado por el ECID.
* `timestamp=2`: John inicia sesión en el sitio web de comercio electrónico con el mismo equipo portátil. Está representado por su ID de CRM y el explorador web que utiliza está representado por el mismo ECID.
   * Este evento vincula dos ID de CRM independientes al mismo ECID, lo que supera el límite configurado de un ID de CRM.
   * Como resultado, el algoritmo de optimización de identidad elimina el vínculo más antiguo, que en este caso es el ID de CRM de Jane que se vinculó en `timestamp=1`.
   * Sin embargo, aunque el ID de CRM de Jane ya no existirá como gráfico en el servicio de identidad, persistirá como perfil en el perfil del cliente en tiempo real. Esto se debe a que un gráfico de identidad debe contener al menos dos identidades vinculadas y, como resultado de la eliminación de los vínculos, el CRM ID de Jane ya no tiene otra identidad a la que vincular.

![shared-device-case-two](../images/identity-settings/shared-device-case-two.png)

>[!ENDTABS]

### Correo electrónico incorrecto

Hay casos en los que un usuario puede introducir valores erróneos en su correo electrónico o números de teléfono.

| Área de nombres | Límite |
| --- | --- |
| ID de CRM | 1 |
| Correo electrónico | 1 |
| ECID | N/A |

En este ejemplo, el ID de CRM y las áreas de nombres de correo electrónico se designan como únicos. Considere el caso de que Jane y John se hayan registrado en su sitio web de comercio electrónico con un valor incorrecto de correo electrónico (por ejemplo, probar<span>@test.com).

* `timestamp=1`: Jane inicia sesión en su sitio web de comercio electrónico utilizando Safari en su iPhone, estableciendo su ID de CRM (información de inicio de sesión) y su ECID (explorador).
* `timestamp=2`: John inicia sesión en el sitio web de comercio electrónico utilizando Google Chrome en su iPhone, estableciendo su CRM ID (información de inicio de sesión) y ECID (explorador).
* `timestamp=3`: su ingeniero de datos ingiere el registro CRM de Jane, lo que provoca que su ID de CRM se vincule al correo electrónico incorrecto.
* `timestamp=4`: el ingeniero de datos ingiere el registro CRM de John, lo que provoca que su ID de CRM se vincule al correo electrónico incorrecto.
   * Esto se convierte en una infracción de los límites configurados, ya que crea un solo gráfico con dos áreas de nombres de ID de CRM.
   * Como resultado, el algoritmo de optimización de identidad elimina el vínculo más antiguo, que en este caso es el vínculo entre la identidad de Jane con el área de nombres de ID de CRM y la identidad con prueba<span>@test.

Con el algoritmo de optimización de identidad, los valores de identidad incorrectos, como correos electrónicos o números de teléfono falsos, no se propagan en varios gráficos de identidad diferentes.

![correo electrónico erróneo](../images/identity-settings/bad-email.png)

### Asociación de evento anónimo

Los ECID almacenan eventos no autenticados (anónimos), mientras que el ID de CRM almacena eventos autenticados. En el caso de los dispositivos compartidos, el ECID (portador de eventos no autenticados) se asocia al **último usuario autenticado**.

Vea el diagrama siguiente para comprender mejor cómo funciona la asociación de eventos anónimos:

* Kevin y Nora comparten una tableta.
   * `timestamp=1`: Kevin inicia sesión en un sitio web de comercio electrónico con su cuenta, lo que establece su ID de CRM (información de inicio de sesión) y un ECID (explorador). En el momento del inicio de sesión, Kevin ahora se considera el último usuario autenticado.
   * `timestamp=2`: Nora inicia sesión en un sitio web de comercio electrónico con su cuenta, lo que establece su ID de CRM (información de inicio de sesión) y el mismo ECID. En el momento del inicio de sesión, Nora ahora se considera el último usuario autenticado.
   * `timestamp=3`: Kevin utiliza la tableta para navegar por el sitio web de comercio electrónico, pero no inicia sesión con su cuenta. La actividad de navegación de Kevin se almacena entonces en el ECID, que a su vez se asocia con Nora porque es el último usuario autenticado. En este punto, Nora posee los eventos anónimos.
      * Hasta que Kevin vuelva a iniciar sesión, el perfil combinado de Nora se asociará a todos los eventos no autenticados almacenados con el ECID (con eventos en los que ECID es la identidad principal).
   * `timestamp=4`: Kevin inicia sesión por segunda vez. En este punto, una vez más se convierte en el último usuario autenticado y ahora también posee los eventos no autenticados:
      * Antes de su inicio de sesión anterior a `timestamp=1`; y
      * Cualquier actividad que él o Nora hicieran mientras navegaban anónimamente entre el primer y el segundo inicio de sesión de Kevin.

![anon-event-association](../images/identity-settings/anon-event-association.png)


## Pasos siguientes

Para obtener más información sobre las reglas de vinculación de gráficos de identidad, lea la siguiente documentación:

* [Resumen de reglas de vinculación de gráficos de identidad](./overview.md)
* [Casos de ejemplo para configurar reglas de vinculación de gráficos de identidad](./example-scenarios.md)
* [Lógica de vinculación de identidad](./identity-linking-logic.md)
* [Servicio de identidad y perfil del cliente en tiempo real](identity-and-profile.md)
