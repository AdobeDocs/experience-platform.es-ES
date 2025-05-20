---
title: Guía De Implementación De Reglas De Vinculación De Gráfico De Identidad
description: Conozca los pasos recomendados a seguir al implementar los datos con las configuraciones de reglas de vinculación de gráficos de identidad.
exl-id: 368f4d4e-9757-4739-aaea-3f200973ef5a
source-git-commit: 28eab3488dccdcc6239b9499e875c31ff132fd48
workflow-type: tm+mt
source-wordcount: '1864'
ht-degree: 6%

---

# Guía de implementación para [!DNL Identity Graph Linking Rules]

>[!IMPORTANT]
>
>Este documento supone que está iniciando la implementación en una nueva zona protegida sin ningún dato.

Lea este documento para obtener una guía paso a paso que puede seguir al implementar los datos con el servicio de identidad de Adobe Experience Platform.

Descripción paso a paso:

1. [Completar requisitos previos para la implementación](#prerequisites-for-implementation)
2. [Crear las áreas de nombres de identidad necesarias](#namespace)
3. [Utilice la herramienta de simulación de gráficos para familiarizarse con el algoritmo de optimización de identidad](#graph-simulation)
4. [Utilice la interfaz de usuario de configuración de identidad para designar las áreas de nombres únicas y configurar las clasificaciones de prioridad de las áreas de nombres](#identity-settings)
5. [Creación de un esquema de modelo de datos de experiencia (XDM)](#schema)
6. [Crear un conjunto de datos](#dataset)
7. [Ingesta de datos en Experience Platform](#ingest)

## Requisitos previos para la implementación {#prerequisites-for-implementation}

En esta sección se describen los pasos previos que debe seguir antes de implementar [!DNL Identity Graph Linking Rules] en sus datos.

### Área de nombres única

#### Requisito de área de nombres de persona única {#single-person-namespace-requirement}

Debe asegurarse de que el área de nombres única con la prioridad más alta esté siempre presente en cada perfil. Al hacerlo, el servicio de identidad puede detectar el identificador de persona adecuado en un gráfico determinado.

+++Seleccione esta opción para ver un ejemplo de gráfico sin un área de nombres de identificador de persona individual

Sin un área de nombres única que represente los identificadores de persona, puede terminar con un gráfico que se vincule a identificadores de persona diferentes para el mismo ECID. En este ejemplo, B2BCRM y B2CRM están vinculados al mismo ECID al mismo tiempo. Este gráfico sugiere que Tom, usando su cuenta de inicio de sesión B2C, compartió un dispositivo con Summer, usando su cuenta de inicio de sesión B2B. Sin embargo, el sistema reconocerá que este es un perfil (colapso de gráfico).

![Escenario de gráfico en el que dos identificadores de persona están vinculados al mismo ECID.](../images/graph-examples/multi_namespaces.png)

+++

+++Seleccione esta opción para ver un ejemplo de un gráfico con un área de nombres de identificador de persona única

Dado un área de nombres única (en este caso, un CRMID en lugar de dos áreas de nombres dispares), el servicio de identidad puede discernir el identificador de persona que se asoció por última vez con el ECID. En este ejemplo, como existe un CRMID único, el servicio de identidad puede reconocer un escenario de &quot;dispositivo compartido&quot;, en el que dos entidades comparten el mismo dispositivo.

![Escenario de gráfico de dispositivo compartido, en el que dos identificadores de persona están vinculados al mismo ECID, pero se ha eliminado el vínculo anterior.](../images/graph-examples/crmid_only_multi.png)

+++

### Configuración de prioridad de área de nombres

Si usa el [conector de origen de Adobe Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md) para la ingesta de datos, debe dar a sus ECID una prioridad mayor que la de Adobe Analytics ID (AAID), ya que el servicio de identidad bloquea la AAID. Al priorizar ECID, puede indicar al Perfil del cliente en tiempo real que almacene eventos no autenticados en ECID en lugar de AAID.

### Eventos de experiencia de XDM {#xdm-experience-events}

>[!CONTEXTUALHELP]
>id="platform_identities_linkingrules_xdm"
>title="Asegúrese de tener un solo identificador de persona"
>abstract="Durante el proceso previo a la implementación, debe asegurarse de que los eventos autenticados que el sistema enviará a Experience Platform contengan siempre un **único** identificador de persona, como un CRMID."

Durante el proceso previo a la implementación, debe asegurarse de que los eventos autenticados que el sistema enviará a Experience Platform contengan siempre un **único** identificador de persona, como un CRMID.

* (Recomendado) Eventos autenticados con un identificador de persona único.
* (No recomendado) Eventos autenticados con dos identificadores de persona únicos. Si tiene más de un identificador de persona único, puede encontrar un colapso de gráfico no deseado.
* (No recomendado) Eventos autenticados sin ningún identificador de persona único. Si no tiene ningún identificador de persona único, los eventos no autenticados y autenticados se almacenarán con el ECID.

>[!BEGINTABS]

>[!TAB Eventos autenticados con un identificador de persona]

```json
{
  "_id": "test_id",
  "identityMap": {
      "ECID": [
          {
              "id": "62486695051193343923965772747993477018",
              "primary": false
          }
      ],
      "CRMID": [
          {
              "id": "John",
              "primary": true
          }
      ]
  },
  "timestamp": "2024-09-24T15:02:32+00:00",
  "web": {
      "webPageDetails": {
          "URL": "https://business.adobe.com/",
          "name": "Adobe Business"
      }
  }
}
```

>[!TAB Eventos autenticados con dos identificadores de persona]

Si el sistema envía dos identificadores de persona, la implementación puede fallar en el requisito del área de nombres de una sola persona. Por ejemplo, si identityMap en la implementación del SDK web contiene un CRMID, un customerID y un área de nombres ECID, no hay garantía de que cada evento contenga CRMID y customerID.

**no** debería enviar una carga útil como la siguiente:

```json
{
  "_id": "test_id",
  "identityMap": {
      "ECID": [
          {
              "id": "62486695051193343923965772747993477018",
              "primary": false
          }
      ],
      "CRMID": [
          {
              "id": "John",
              "primary": true
          }
      ],
      "customerID": [
          {
            "id": "Jane",
            "primary": false
          }
      ],
  },
  "timestamp": "2024-09-24T15:02:32+00:00",
  "web": {
      "webPageDetails": {
          "URL": "https://business.adobe.com/",
          "name": "Adobe Business"
      }
  }
}
```

Sin embargo, es importante tener en cuenta que, aunque puede enviar dos identificadores de persona, no hay garantía de que se evite un colapso de gráfico no deseado debido a errores de implementación o datos. Considere el siguiente escenario:

* `timestamp1` = John inicia sesión -> el sistema captura `CRMID: John, ECID: 111`. Sin embargo, `customerID: John` no está presente en esta carga útil de evento.
* `timestamp2` = Jane inicia sesión -> el sistema captura `customerID: Jane, ECID: 111`. Sin embargo, `CRMID: Jane` no está presente en esta carga útil de evento.

Por lo tanto, se recomienda enviar solo un identificador de persona con los eventos autenticados.

En la simulación de gráficos, esta ingesta puede tener el siguiente aspecto:

![Se representa la IU de simulación de gráficos con un gráfico de ejemplo.](../images/implementation/example-graph.png)

>[!TAB Eventos autenticados sin identificadores de persona]

En este ejemplo, puede suponer que el siguiente evento se envió a Experience Platform mientras John (el usuario final) exploraba su sitio web mientras se autenticaba. Sin embargo, a pesar de estar autenticado, Experience Platform no puede identificar a John debido a la falta de identificadores de persona en el evento. Por lo tanto, este evento se interpreta como un usuario anónimo que navega por el sitio web de Adobe Business, en lugar de reconocerlo como una actividad en línea asociada específicamente a John.

```json
{
    "_id": "test_id",
    "identityMap": {
        "ECID": [
            {
                "id": "62486695051193343923965772747993477018",
                "primary": false
            }
        ]
    },
    "timestamp": "2024-09-24T15:02:32+00:00",
    "web": {
        "webPageDetails": {
            "URL": "https://business.adobe.com/",
            "name": "Adobe Business"
        }
    }
}
```

>[!ENDTABS]

## Definición de permisos {#set-permissions}

El primer paso en el proceso de implementación del servicio de identidad es garantizar que la cuenta de Experience Platform se añada a una función que esté aprovisionada con los permisos necesarios. El administrador puede configurar permisos para su cuenta navegando a la interfaz de usuario de permisos en Adobe Experience Cloud. A partir de ahí, la cuenta debe agregarse a una función con los siguientes permisos:

* [!UICONTROL Ver configuración de identidad]: aplique este permiso para poder ver áreas de nombres únicas y su prioridad en la página de exploración del área de nombres de identidad.
* [!UICONTROL Editar configuración de identidad]: aplique este permiso para poder editar y guardar la configuración de identidad.

Para obtener más información sobre los permisos, lea la [guía de permisos](../../access-control/abac/ui/permissions.md).

## Crear sus áreas de nombres de identidad {#namespace}

Si los datos lo requieren, primero debe crear los espacios de nombres adecuados para su organización. Para obtener información sobre cómo crear un área de nombres personalizada, lea la guía sobre [creación de un área de nombres personalizada en la interfaz de usuario](../features/namespaces.md#create-custom-namespaces).

## Uso de la herramienta de simulación de gráficos {#graph-simulation}

A continuación, vaya a la [herramienta de simulación de gráficos](./graph-simulation.md) en el área de trabajo de la interfaz de usuario del servicio de identidad. Puede utilizar la herramienta de simulación de gráficos para simular gráficos de identidad, creados con una variedad de diferentes configuraciones de área de nombres única y prioridad de área de nombres.

Mediante la creación de diferentes configuraciones, puede utilizar la herramienta de simulación de gráficos para aprender y comprender mejor cómo el algoritmo de optimización de identidad y determinadas configuraciones pueden afectar al comportamiento del gráfico.

## Configuración de la identidad {#identity-settings}

Una vez que tengas una mejor idea de cómo deseas que se comporte tu gráfico, ve a la [interfaz de usuario de configuración de identidad](./identity-settings-ui.md) en el área de trabajo de la interfaz de usuario del servicio de identidad. Para acceder a la interfaz de usuario de configuración de identidad, selecciona **[!UICONTROL Identidades]** en el panel de navegación izquierdo y, a continuación, selecciona **[!UICONTROL Configuración]**.

![La página de exploración de identidades con el botón de configuración resaltado.](../images/implementation/settings.png)

Utilice la interfaz de usuario de configuración de identidad para designar las áreas de nombres únicas y configurar las áreas de nombres por orden de prioridad. Una vez que haya terminado de aplicar la configuración, debe esperar al menos seis horas antes de continuar con la ingesta de datos, ya que la nueva configuración tarda al menos seis horas en reflejarse en el servicio de identidad.

Para obtener más información, lea la [guía de interfaz de usuario de configuración de identidad](./identity-settings-ui.md).

## Creación de un esquema XDM {#schema}

Una vez establecidas las áreas de nombres únicas y las prioridades del área de nombres, ahora puede continuar con la configuración necesaria para introducir los datos. En primer lugar, debe crear un esquema XDM. En función de los datos, es posible que tenga que crear un esquema tanto para XDM Individual Profile como para XDM ExperienceEvent.

Para introducir datos en el perfil del cliente en tiempo real, debe asegurarse de que el esquema contenga al menos un campo que se haya designado como identidad principal. Al establecer una identidad principal, puede habilitar un esquema determinado para la ingesta de perfiles.

Para obtener instrucciones sobre cómo crear un esquema, lea la guía sobre [creación de un esquema XDM en la interfaz de usuario](../../xdm/tutorials/create-schema-ui.md).

## Crear un conjunto de datos {#dataset}

A continuación, cree un conjunto de datos para proporcionar una estructura para los datos que va a introducir. Un conjunto de datos es una construcción de almacenamiento y administración para una colección de datos, normalmente una tabla, que contiene un esquema (columnas) y campos (filas). Los conjuntos de datos trabajan en conjunto con esquemas y, para introducir datos en el Perfil del cliente en tiempo real, el conjunto de datos debe estar habilitado para la ingesta de perfiles. Para que el conjunto de datos esté habilitado para el perfil, debe hacer referencia a un esquema que esté habilitado para la ingesta de perfiles.

Para obtener instrucciones sobre cómo crear un conjunto de datos, lea la [guía de IU de conjuntos de datos](../../catalog/datasets/user-guide.md).

## Ingesta de datos {#ingest}

En este punto, debería tener lo siguiente:

* Los permisos necesarios para acceder a las funciones del servicio de identidad.
* Áreas de nombres para sus datos.
* Áreas de nombres únicas designadas y prioridades configuradas para sus áreas de nombres.
* Al menos un esquema XDM. (Según los datos y el caso de uso específico, es posible que deba crear esquemas de perfil y de evento de experiencia).
* Un conjunto de datos basado en el esquema.

Una vez que tenga todos los elementos enumerados arriba, puede empezar a ingerir los datos en Experience Platform. Puede realizar la ingesta de datos de varias formas diferentes. Puede utilizar los siguientes servicios para llevar los datos a Experience Platform:

* [Ingesta por lotes y streaming](../../ingestion/home.md)
* [Recopilación de datos en Experience Platform](../../collection/home.md)
* [Fuentes de Experience Platform](../../sources/home.md)

>[!TIP]
>
>Una vez introducidos los datos, la carga de datos sin procesar del XDM no cambia. Es posible que siga viendo las configuraciones de identidad principales en la interfaz de usuario. Sin embargo, estas configuraciones se sobrescribirán con la configuración de identidad.

Para obtener cualquier comentario, use la opción **[!UICONTROL comentarios de Beta]** en el área de trabajo de la interfaz de usuario del servicio de identidad.

## Validación de los gráficos {#validate}

Utilice el panel de identidad para obtener información sobre el estado de los gráficos de identidad, como el recuento general de identidades y las tendencias del recuento de gráficos, el recuento de identidades por área de nombres y el recuento de gráficos por tamaño de gráfico. También puede utilizar el panel de identidad para ver las tendencias en gráficos con dos o más identidades, organizadas por área de nombres.

Seleccione los puntos suspensivos (`...`) y, a continuación, seleccione **[!UICONTROL Ver más]** para obtener más información y para comprobar que no hay gráficos contraídos.

![Panel de identidad en el área de trabajo de la interfaz de usuario del servicio de identidad.](../images/implementation/identity_dashboard.png)

Utilice la ventana que aparece para ver información sobre los gráficos contraídos. En este ejemplo, tanto el correo electrónico como el teléfono están marcados como un área de nombres única, por lo que no hay gráficos contraídos en la zona protegida.

![Ventana emergente para gráficos con varias identidades.](../images/implementation/graphs.png)

## Apéndice {#appendix}

Lea esta sección para obtener información adicional a la que puede hacer referencia al implementar la configuración de identidad y las áreas de nombres únicas.

### Escenario de ID de inicio de sesión pendiente {#dangling-loginid-scenario}

El siguiente gráfico simula un escenario de ID de inicio de sesión &quot;colgado&quot;. En este ejemplo, dos ID de inicio de sesión diferentes están enlazados al mismo ECID. Sin embargo, `{loginID: ID_C}` no está vinculado al CRMID. Por lo tanto, el servicio de identidad no puede detectar que estos dos ID de inicio de sesión representen dos entidades diferentes.

>[!BEGINTABS]

>[!TAB Id. de inicio de sesión ambiguo]

En este ejemplo, `{loginID: ID_C}` se deja colgado y desenlazado a un CRMID. Por lo tanto, la entidad de la persona a la que se debe asociar este ID de inicio de sesión queda ambigua.

![Ejemplo de gráfico con un escenario &quot;colgado&quot; de loginID.](../images/graph-examples/dangling_example.png)

>[!TAB loginID está vinculado a un CRMID]

En este ejemplo, `{loginID: ID_C}` está vinculado a `{CRMID: Tom}`. Por lo tanto, el sistema puede discernir que este ID de inicio de sesión está asociado con Tom.

![LoginID está vinculado a un CRMID.](../images/graph-examples/id_c_tom.png)

>[!TAB loginID está enlazado a otro CRMID]

En este ejemplo, `{loginID: ID_C}` está vinculado a `{CRMID: Summer}`. Por lo tanto, el sistema puede discernir que este ID de inicio de sesión está asociado con otra entidad de persona, en este caso, Summer.

Este ejemplo también muestra que Tom y Summer son dos entidades de persona distintas que comparten un dispositivo, que se representa mediante `{ECID: 111}`.

![LoginID está vinculado a otro CRMID.](../images/graph-examples/id_c_summer.png)

>[!ENDTABS]

## Pasos siguientes

Para obtener más información sobre [!DNL Identity Graph Linking Rules], lea la siguiente documentación:

* [Información general de [!DNL Identity Graph Linking Rules]](./overview.md)
* [Algoritmo de optimización de identidad](./identity-optimization-algorithm.md)
* [Ejemplos de configuraciones de gráficos](./example-configurations.md)
* [Resolución de problemas y preguntas frecuentes](./troubleshooting.md)
* [Prioridad del área de nombres](./namespace-priority.md)
* [IU de simulación de gráficos](./graph-simulation.md)
* [IU de configuración de identidad](./identity-settings-ui.md)
