---
title: Lógica de vinculación del servicio de identidad
description: Obtenga información acerca de cómo el servicio de identidad vincula identidades dispares para crear una vista completa de un cliente.
hide: true
hidefromtoc: true
badge: Alfa
source-git-commit: 03e4cd440f8627ad837a31e1c017d0b824cafb04
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 4%

---

# Lógica de vinculación del servicio de identidad

>[!IMPORTANT]
>
>Las reglas de vinculación de gráficos de identidad están actualmente en Alpha. La funcionalidad y la documentación están sujetas a cambios.

Se establece un vínculo entre dos identidades cuando coinciden el área de nombres de identidad y los valores de identidad.

Existen dos tipos de identidades que se vinculan:

* **Registros de perfil**: Estas identidades generalmente provienen de sistemas CRM.
* **Eventos de experiencia**: Estas identidades generalmente provienen de la implementación del SDK web o del origen de Adobe Analytics.

## Explicación de la lógica de vinculación del servicio de identidad

Una identidad consta de un área de nombres de identidad y un valor de identidad.

* Un área de nombres de identidad es el contexto de un valor de identidad determinado para. Algunos ejemplos comunes de áreas de nombres de identidad son ID de CRM, Correo electrónico y Teléfono.
* Un valor de identidad es la cadena que representa una entidad del mundo real. Por ejemplo: &quot;julien<span>@acme.com&quot; puede ser un valor de identidad para un área de nombres de correo electrónico, y 555-555-1234 puede ser un valor de identidad correspondiente para un área de nombres de teléfono.

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

>[!TAB Gráfico actualizado]

El servicio de identidad reconoce que el CRM ID:60013ABC ya existe dentro del gráfico y, por lo tanto, solo vincula el nuevo ECID

![gráfico actualizado](../images/identity-settings/updated-graph.png)

>[!ENDTABS]

## Escenario del cliente

Es ingeniero de datos y está introduciendo el siguiente conjunto de datos CRM (registro de perfil) en Experience Platform.

| ID de CRM** | Phone* | Correo electrónico* | Nombre | Apellido |
| --- | --- | --- | --- | --- |
| 60013ABC | 555-555-1234 | julien<span>@acme.com | Julien | Smith |
| 31260XYZ | 777-777-6890 | evan<span>@acme.com | Evan | Smith |

>[!NOTE]
>
>* `**` - Indica un campo marcado como identidad principal.
>* `*` - Indica un campo marcado como identidad secundaria.
>
>El servicio de identidad no distingue entre identidad principal y secundaria. Siempre que un campo se marque como identidad, se incorporará al servicio de identidad.

También ha implementado el SDK web y ha introducido un conjunto de datos del SDK web (evento de experiencia) con las siguientes tablas de datos:

| Marca de tiempo | Identidades en el evento* | Evento |
| --- | --- | --- |
| `t=1` | ECID:38652 | Ver página principal |
| `t=2` | ECID:38652, CRM ID:31260XYZ | Búsqueda de zapatos |
| `t=3` | ECID:44675 | Ver página principal |
| `t=4` | ECID:44675, CRM ID: 31260XYZ | Ver historial de compras |

>[!NOTE]
>
>* `*` : denota un campo marcado como identidad, donde ECID se marca como principal.
>* De forma predeterminada, el identificador de persona (en este caso, el ID de CRM) se designa como identidad principal. Si el identificador de persona no existe, el identificador de cookie (en este caso, el ECID) se convierte en la identidad principal.

En este ejemplo:

* `t=1`, utilizaba un equipo de escritorio (ECID:38652) y para ver la página de inicio exploraba de forma anónima.
* `t=2`, utilizó el mismo equipo de escritorio, inició sesión (CRM ID:31260XYZ) y luego buscó zapatos.
   * Una vez que el usuario ha iniciado sesión, el evento envía tanto el ECID como el ID de CRM al servicio de identidad.
* `t=3`, utilizó un ordenador portátil (ECID:44675) y navegó de forma anónima.
* `t=4`, utilizó el mismo equipo portátil, inició sesión (CRM ID: 31260XYZ) y luego vio el historial de compras.


>[!BEGINTABS]

>[!TAB timestamp=0]

En `timestamp=0`, tiene dos gráficos de identidad para dos clientes diferentes. Ambos están representados por tres identidades vinculadas.

| | ID de CRM | Correo electrónico | Phone |
| --- | --- | --- | --- |
| Customer one | 60013ABC | julien<span>@acme.com | 555-555-1234 |
| Cliente dos | 31260XYZ | evan<span>@acme.com | 777-777-6890 |

![timestamp-zero](../images/identity-settings/timestamp-zero.png)

>[!TAB timestamp=1]

En `timestamp=1`, un cliente utiliza un portátil para visitar su sitio web de comercio electrónico, ver su página de inicio y navegar de forma anónima. Este evento de exploración anónima se identifica como ECID:38652. Dado que el servicio de identidad solo almacena eventos con al menos dos identidades, esta información no se almacena.

![timestamp-one](../images/identity-settings/timestamp-one.png)

>[!TAB timestamp=2]

En `timestamp=2`, un cliente utiliza el mismo portátil para visitar su sitio web de comercio electrónico. Inician sesión con la combinación de nombre de usuario y contraseña y buscan zapatos. El servicio de identidad identifica la cuenta del cliente cuando inicia sesión porque corresponde a su ID de CRM: 31260XYZ. Además, el servicio de identidad relaciona ECID:38562 con CRM ID:31260XYZ, ya que ambos utilizan el mismo explorador en el mismo dispositivo.

![timestamp-two](../images/identity-settings/timestamp-two.png)

>[!TAB timestamp=3]

En `timestamp=3` un cliente utiliza una tableta para visitar su sitio web de comercio electrónico y navegar de forma anónima. Este evento de exploración anónima se identifica como ECID:44675. Dado que el servicio de identidad solo almacena eventos con al menos dos identidades, esta información no se almacena.

![timestamp-third](../images/identity-settings/timestamp-three.png)

>[!TAB timestamp=4]

En `timestamp=4`, un cliente utiliza la misma tableta, inicia sesión en su cuenta (ID de CRM:31260XYZ) y ve su historial de compras. Este evento vincula su CRM ID:31260XYZ al identificador de cookie asignado a la actividad de navegación anónima, ECID:44675, y vincula ECID:44675 al gráfico de identidad de los dos clientes.

![timestamp-four](../images/identity-settings/timestamp-four.png)

>[!ENDTABS]

## Pasos siguientes

Para obtener más información sobre las reglas de vinculación de gráficos de identidad, lea la siguiente documentación:

* [Resumen de reglas de vinculación de gráficos de identidad](./overview.md)
* [Casos de ejemplo para configurar reglas de vinculación de gráficos de identidad](./example-scenarios.md)
* [Servicio de identidad y perfil del cliente en tiempo real](identity-and-profile.md)
