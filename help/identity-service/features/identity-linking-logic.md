---
title: Lógica de vinculación del servicio de identidad
description: Obtenga información acerca de cómo el servicio de identidad vincula identidades dispares para crear una vista completa de un cliente.
exl-id: 1c958c0e-0777-48db-862c-eb12b2e7a03c
source-git-commit: 2b6700b2c19b591cf4e60006e64ebd63b87bdb2a
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 0%

---

# Lógica de vinculación del servicio de identidad

Se establece un vínculo entre dos identidades cuando coinciden el área de nombres de identidad y los valores de identidad.

Existen dos tipos de identidades que se vinculan:

* **Registros de perfil**: Estas identidades generalmente provienen de sistemas CRM.
* **Eventos de experiencia**: Estas identidades generalmente provienen de la implementación de WebSDK o del origen de Adobe Analytics.

## Significado semántico del establecimiento de vínculos

Una identidad representa una entidad real. Si hay un vínculo establecido entre dos identidades, significa que las dos identidades están asociadas. A continuación se muestran algunos ejemplos que ilustran este concepto:

| Acción | Vínculos establecidos | Significado |
| --- | --- | --- |
| Un usuario final inicia sesión con un equipo. | El ID de CRM y el ECID están vinculados entre sí. | Una persona (ID de CRM) posee un dispositivo con un explorador (ECID). |
| Un usuario final navega de forma anónima usando una iPhone | IDFA está vinculado con ECID. | El dispositivo de hardware de Apple (IDFA), como un iPhone, está asociado al explorador (ECID). |
| Un usuario final inicia sesión con Google Chrome y luego Firefox. | El ID de CRM está vinculado con dos ECID diferentes. | Una persona (CRM ID) está asociada a dos exploradores web (**Nota**: Cada explorador tendrá su propio ECID). |
| Un ingeniero de datos introduce un registro CRM que incluye dos campos marcados como identidad: ID de CRM y correo electrónico. | El ID de CRM y el correo electrónico están vinculados. | Una persona (ID de CRM) está asociada a la dirección de correo electrónico. |

## Explicación de la lógica de vinculación del servicio de identidad

Una identidad consta de un área de nombres de identidad y un valor de identidad.

* Un área de nombres de identidad es el contexto de un valor de identidad determinado para. Algunos ejemplos comunes de áreas de nombres de identidad son ID de CRM, Correo electrónico y Teléfono.
* Un valor de identidad es la cadena que representa una entidad del mundo real. Por ejemplo: &quot;julien<span>@acme.com&quot; puede ser un valor de identidad para un área de nombres de correo electrónico y 555-555-1234 puede ser un valor de identidad correspondiente para un área de nombres de teléfono.

>[!TIP]
>
>El área de nombres de identidad es importante porque, sin ella, el valor de identidad pierde su contexto y no tendrá información suficiente para hacer coincidir correctamente las identidades.

Consulte los siguientes diagramas para obtener una representación visual del funcionamiento de la lógica de vinculación del servicio de ID:

>[!BEGINTABS]

>[!TAB Gráfico existente]

Supongamos que tiene un gráfico de identidad existente con tres identidades vinculadas:

* TELÉFONO:(555)-555-1234
* CORREO ELECTRÓNICO:julien<span>@acme.com
* ID de CRM:60013ABC

![gráfico existente](../images/identity-settings/existing-graph.png)

>[!TAB Datos entrantes]

Se incorporan un par de identidades en el gráfico y este par contiene:

* ID de CRM:60013ABC
* ECID:100066526

![datos entrantes](../images/identity-settings/incoming-data.png)

>[!TAB Se actualizó el gráfico]

El servicio de identidad reconoce que el CRM ID:60013ABC ya existe dentro del gráfico y, por lo tanto, solo vincula el nuevo ECID

![gráfico actualizado](../images/identity-settings/updated-graph.png)

>[!ENDTABS]

## Escenario del cliente

Es ingeniero de datos y está introduciendo el siguiente conjunto de datos CRM (registro de perfil) en Experience Platform.

| ID de CRM** | Teléfono* | Correo electrónico* | Nombre | Apellido |
| --- | --- | --- | --- | --- |
| 60013ABC | 555-555-1234 | julien<span>@acme.com | Julien | Smith |
| 31260XYZ | 777-777-6890 | evan<span>@acme.com | Evan | Smith |

>[!NOTE]
>
>* `**` - Indica un campo marcado como identidad principal.
>* `*`: indica un campo marcado como identidad secundaria.
>
>El servicio de identidad no distingue entre identidad principal y secundaria. Siempre que un campo se marque como identidad, se incorporará al servicio de identidad.

También ha implementado el SDK web y ha introducido un conjunto de datos del SDK web (evento de experiencia) con las siguientes tablas de datos:

| Marca de tiempo | Identidades en el evento* | Evento |
| --- | --- | --- |
| `t=1` | ECID:38652 | Ver página principal |
| `t=2` | ECID:38652, CRM ID:31260XYZ | Búsqueda de zapatos |
| `t=3` | ECID:44675 | Ver página principal |
| `t=4` | ECID:44675, CRM ID: 31260XYZ | Ver historial de compras |

La identidad principal de cada evento se determinará en función de [cómo configure los tipos de elementos de datos](../../tags/extensions/client/web-sdk/data-element-types.md).

>[!NOTE]
>
>* Si selecciona el ID de CRM como principal, los eventos autenticados (eventos con mapa de identidad que contenga el ID de CRM y ECID) tendrán una identidad principal de ID de CRM. Para eventos no autenticados (los eventos con el mapa de identidad que solo contiene ECID) tendrán una identidad principal de ECID. El Adobe recomienda esta opción.
>
>* Si selecciona el ECID como principal, independientemente del estado de autenticación, el ECID se convierte en la identidad principal.

En este ejemplo:

* `t=1`, utilizó un equipo de escritorio (ECID:38652) y para ver la página principal examinar de forma anónima.
* `t=2`, utilizó el mismo equipo de escritorio, inició sesión (CRM ID:31260XYZ) y después buscó zapatos.
   * Una vez que el usuario ha iniciado sesión, el evento envía tanto el ECID como el ID de CRM al servicio de identidad.
* `t=3`, utilizó un equipo portátil (ECID:44675) y navegó de forma anónima.
* `t=4`, utilizó el mismo equipo portátil, inició sesión (CRM ID: 31260XYZ) y después vio el historial de compras.


>[!BEGINTABS]

>[!TAB marca de tiempo=0]

En `timestamp=0`, tiene dos gráficos de identidad para dos clientes diferentes. Ambos están representados por tres identidades vinculadas.

| | ID de CRM | Correo electrónico | Teléfono |
| --- | --- | --- | --- |
| Customer one | 60013ABC | julien<span>@acme.com | 555-555-1234 |
| Cliente dos | 31260XYZ | evan<span>@acme.com | 777-777-6890 |

![marca de tiempo-cero](../images/identity-settings/timestamp-zero.png)

>[!TAB marca de tiempo=1]

En `timestamp=1`, un cliente usa un equipo portátil para visitar el sitio web de comercio electrónico, ver la página principal y examinar de forma anónima. Este evento de exploración anónima se identifica como ECID:38652. Dado que el servicio de identidad solo almacena eventos con al menos dos identidades, esta información no se almacena.

![marca de tiempo-uno](../images/identity-settings/timestamp-one.png)

>[!TAB marca de tiempo=2]

En `timestamp=2`, un cliente usa el mismo equipo portátil para visitar el sitio web de comercio electrónico. Inician sesión con la combinación de nombre de usuario y contraseña y buscan zapatos. El servicio de identidad identifica la cuenta del cliente cuando inicia sesión porque corresponde a su ID de CRM: 31260XYZ. Además, el servicio de identidad relaciona ECID:38562 con CRM ID:31260XYZ, ya que ambos utilizan el mismo explorador en el mismo dispositivo.

![marca de tiempo-dos](../images/identity-settings/timestamp-two.png)

>[!TAB marca de tiempo=3]

En `timestamp=3`, un cliente usa una tableta para visitar el sitio web de comercio electrónico y navegar de forma anónima. Este evento de exploración anónima se identifica como ECID:44675. Dado que el servicio de identidad solo almacena eventos con al menos dos identidades, esta información no se almacena.

![marca de tiempo-tres](../images/identity-settings/timestamp-three.png)

>[!TAB marca de tiempo=4]

En `timestamp=4`, un cliente usa la misma tableta, inicia sesión en su cuenta (CRM ID:31260XYZ) y ve su historial de compras. Este evento vincula su CRM ID:31260XYZ al identificador de cookie asignado a la actividad de navegación anónima, ECID:44675, y vincula ECID:44675 al gráfico de identidad de los dos clientes.

![marca de tiempo-cuatro](../images/identity-settings/timestamp-four.png)

>[!ENDTABS]
