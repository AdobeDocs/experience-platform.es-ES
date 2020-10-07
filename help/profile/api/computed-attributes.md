---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
title: 'Atributos calculados: API de Perfil del cliente en tiempo real'
topic: guide
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '2403'
ht-degree: 1%

---


# (Alfa) Extremo de atributos calculados

>[!IMPORTANT]
>
>La funcionalidad de atributo calculada descrita en este documento se encuentra actualmente en alfa y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

Los atributos calculados permiten calcular automáticamente el valor de los campos en función de otros valores, cálculos y expresiones. Los atributos calculados funcionan en el nivel de perfil, lo que significa que se pueden acumulados valores en todos los registros y eventos.

Cada atributo calculado contiene una expresión, o &quot;regla&quot;, que evalúa los datos entrantes y almacena el valor resultante en un atributo de perfil o en un evento. Estos cálculos le ayudan a responder fácilmente preguntas relacionadas con aspectos como el valor de compra de por vida, el tiempo entre compras o la cantidad de aperturas de aplicaciones, sin necesidad de realizar cálculos complejos manualmente cada vez que se necesita la información.

Esta guía le ayudará a comprender mejor los atributos calculados dentro de Adobe Experience Platform e incluye ejemplos de llamadas de API para realizar operaciones CRUD básicas mediante el `/config/computedAttributes` punto final.

## Primeros pasos

El punto final de API utilizado en esta guía forma parte de la API [de Perfil del cliente en tiempo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)real. Antes de continuar, consulte la guía [de](getting-started.md) introducción para ver los vínculos a la documentación relacionada, una guía para leer las llamadas de la API de muestra en este documento e información importante sobre los encabezados necesarios para realizar llamadas con éxito a cualquier [!DNL Experience Platform] API.

## Explicación de los atributos calculados

Adobe Experience Platform le permite importar y combinar fácilmente datos de múltiples fuentes para poder generarlos [!DNL Real-time Customer Profiles]. Cada perfil contiene información importante relacionada con un individuo, como su información de contacto, preferencias e historial de compras, lo que proporciona una vista de 360 grados del cliente.

Parte de la información recopilada en el perfil se puede entender fácilmente al leer los campos de datos directamente (por ejemplo, &quot;nombre&quot;), mientras que otros datos requieren realizar varios cálculos o basarse en otros campos y valores para generar la información (por ejemplo, &quot;total de compras de duración&quot;). Para facilitar la comprensión de estos datos de un vistazo, [!DNL Platform] permite crear atributos calculados que realizan automáticamente estas referencias y cálculos, devolviendo el valor en el campo correspondiente.

Los atributos calculados incluyen la creación de una expresión, o &quot;regla&quot;, que funciona con los datos entrantes y almacena el valor resultante en un atributo o evento de perfil. Las expresiones se pueden definir de varias formas diferentes, lo que le permite especificar que una regla evalúe únicamente los eventos entrantes, los datos de evento y perfil entrantes o los eventos de evento, perfil e historial entrantes.

### Casos de uso

Los casos de uso para atributos calculados pueden ir desde cálculos simples a referencias muy complejas. Estos son algunos ejemplos de casos de uso para atributos calculados:

1. **[!UICONTROL Porcentajes]:** Un atributo simple calculado podría incluir tomar dos campos numéricos en un registro y dividirlos para crear un porcentaje. Por ejemplo, puede tomar el número total de correos electrónicos enviados a un individuo y dividirlos por el número de correos electrónicos que se abre el individuo. Al consultar el campo de atributo calculado resultante, se mostraría rápidamente el porcentaje de correos electrónicos totales abiertos por el individuo.
1. **[!UICONTROL Uso]de la aplicación:** Otro ejemplo incluye la capacidad de acumulado del número de veces que un usuario abre la aplicación. Al rastrear el número total de aperturas de aplicaciones, en función de eventos abiertos individuales, puede enviar ofertas o mensajes especiales a los usuarios en su 100° período de apertura, lo que estimula una mayor participación con su marca.
1. **[!UICONTROL Valores]acumulados:** La recopilación de totales en curso, como un valor de compra de por vida para un cliente, puede ser muy difícil. Esto requiere actualizar el total histórico cada vez que se produce un nuevo evento de compra. Un atributo calculado le permite hacerlo mucho más fácilmente manteniendo el valor de duración en un solo campo que se actualiza automáticamente después de cada evento de compra exitoso relacionado con el cliente.

## Configurar un atributo calculado

Para configurar un atributo calculado, primero debe identificar el campo que contendrá el valor de atributo calculado. Este campo se puede crear con una mezcla para agregar el campo a un esquema existente o seleccionando un campo que ya haya definido en un esquema.

>[!NOTE]
>
>No se pueden agregar atributos calculados a los campos dentro de mezclas definidas por Adobe. El campo debe estar dentro de la `tenant` Área de nombres, lo que significa que debe ser un campo definido y agregado a un esquema.

Para definir correctamente un campo de atributo calculado, el esquema debe estar activado [!DNL Profile] y aparecer como parte del esquema de unión de la clase en la que se basa el esquema. Para obtener más información sobre esquemas y uniones [!DNL Profile]habilitados, consulte la sección de la guía para [!DNL Schema Registry] desarrolladores sobre la [activación de un esquema para Perfil y visualización de esquemas](../../xdm/api/getting-started.md)de unión. También se recomienda examinar la [sección sobre uniones](../../xdm/schema/composition.md) en la documentación básica sobre la composición del esquema.

El flujo de trabajo de este tutorial utiliza un esquema [!DNL Profile]habilitado y sigue los pasos para definir una nueva combinación que contenga el campo de atributo calculado y garantizar que sea la Área de nombres correcta. Si ya tiene un campo que se encuentra en la Área de nombres correcta dentro de un esquema con Perfil habilitado, puede continuar directamente con el paso para [crear un atributo](#create-a-computed-attribute)calculado.

### Vista de un esquema

Los pasos siguientes utilizan la interfaz de usuario de Adobe Experience Platform para localizar un esquema, agregar una mezcla y definir un campo. Si prefiere utilizar la [!DNL Schema Registry] API, consulte la guía [para desarrolladores de](../../xdm/api/getting-started.md) Esquema Registry para ver los pasos sobre cómo crear una mezcla, agregar una mezcla a un esquema y habilitar un esquema para su uso con [!DNL Real-time Customer Profile].

En la interfaz de usuario, haga clic en **[!UICONTROL Esquemas]** en el carril izquierdo y utilice la barra de búsqueda de la ficha **[!UICONTROL Examinar]** para encontrar rápidamente el esquema que desea actualizar.

![](../images/computed-attributes/Schemas-Browse.png)

Una vez localizado el esquema, haga clic en su nombre para abrir el [!DNL Schema Editor] lugar donde puede realizar modificaciones en el esquema.

![](../images/computed-attributes/Schema-Editor.png)

### Crear una mezcla

Para crear una nueva mezcla, haga clic en **[!UICONTROL Añadir]** junto a **[!UICONTROL Mezclinas]** en la sección **[!UICONTROL Composición]** en la parte izquierda del editor. Esto abre el cuadro de diálogo **[!UICONTROL Añadir mezcla]** , donde puede ver las mezclas existentes. Haga clic en el botón de radio para **[!UICONTROL Crear nueva mezcla]** para definir la nueva mezcla.

Asigne un nombre y una descripción a la mezcla y haga clic en **[!UICONTROL Añadir mezcla]** cuando la haya completado.

![](../images/computed-attributes/Add-mixin.png)

### Añadir un campo de atributo calculado en el esquema

Su nueva mezcla debe aparecer ahora en la sección &quot;[!UICONTROL Mezclas]&quot; en &quot;[!UICONTROL Composición]&quot;. Haga clic en el nombre de la mezcla y aparecerán varios botones de campo **** Añadir en la sección **[!UICONTROL Estructura]** del editor.

Seleccione **[!UICONTROL Añadir campo]** junto al nombre del esquema para agregar un campo de nivel superior, o bien puede seleccionar agregar el campo en cualquier lugar dentro del esquema que prefiera.

Después de hacer clic en **[!UICONTROL Añadir campo]** , se abre un nuevo objeto, denominado por su ID de inquilino, que muestra que el campo está en la Área de nombres correcta. Dentro de ese objeto, aparece un campo **** Nuevo. Esto sucede si el campo en el que se va a definir el atributo calculado.

![](../images/computed-attributes/New-field.png)

### Configurar el campo

Mediante la sección Propiedades **[!UICONTROL del]** campo a la derecha del editor, proporcione la información necesaria para el nuevo campo, incluido su nombre, nombre para mostrar y tipo.

>[!NOTE]
>
>El tipo del campo debe ser del mismo tipo que el valor del atributo calculado. Por ejemplo, si el valor del atributo calculado es una cadena, el campo que se está definiendo en el esquema debe ser una cadena.

Cuando termine, haga clic en **[!UICONTROL Aplicar]** y aparecerá el nombre del campo, así como su tipo en la sección **[!UICONTROL Estructura]** del editor.

![](../images/computed-attributes/Apply.png)

### Habilitar esquema para [!DNL Profile]

Antes de continuar, asegúrese de que el esquema esté habilitado para [!DNL Profile]. Haga clic en el nombre del esquema en la sección **[!UICONTROL Estructura]** del editor para que aparezca la ficha Propiedades **[!UICONTROL del]** Esquema. Si el control deslizante del **[!UICONTROL Perfil]** es azul, el esquema se ha activado para [!DNL Profile].

>[!NOTE]
>
>La activación de un esquema para [!DNL Profile] no se puede deshacer, por lo que si hace clic en el control deslizante una vez activado, no tendrá que correr el riesgo de deshabilitarlo.

![](../images/computed-attributes/Profile.png)

Ahora puede hacer clic en **[!UICONTROL Guardar]** para guardar el esquema actualizado y continuar con el resto del tutorial con la API.

### Crear un atributo calculado {#create-a-computed-attribute}

Ahora, con el campo de atributo calculado identificado y la confirmación de que el esquema está habilitado para [!DNL Profile], puede configurar un atributo calculado.

Comience por realizar una solicitud de POST al extremo con un cuerpo de solicitud que contenga los detalles del atributo calculado que desea crear. `/config/computedAttributes`

**Formato API**

```http
POST /config/computedAttributes
```

**Solicitud**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name" : "birthdayCurrentMonth",
        "path" : "_{TENANT_ID}",
        "description" : "Computed attribute to capture if the customer birthday is in the current month.",
        "expression" : {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "person.birthDate.getMonth() = currentMonth()"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| Propiedad | Descripción |
|---|---|
| `name` | El nombre del campo de atributo calculado, como una cadena. |
| `path` | Ruta al campo que contiene el atributo calculado. Esta ruta se encuentra dentro del `properties` atributo del esquema y NO debe incluir el nombre del campo en la ruta. Al escribir la ruta, omita los múltiples niveles de `properties` atributos. |
| `{TENANT_ID}` | Si no está familiarizado con su ID de inquilino, consulte los pasos para encontrar su ID de inquilino en la guía para desarrolladores de [Esquema Registry](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | Descripción del atributo calculado. Esto resulta especialmente útil una vez que se han definido varios atributos calculados, ya que ayudará a otros miembros de la organización de IMS a determinar el atributo calculado correcto que se debe utilizar. |
| `expression.value` | Una expresión válida [!DNL Profile Query Language] (PQL). Para obtener más información sobre PQL y vínculos a consultas compatibles, lea la descripción general [de](../../segmentation/pql/overview.md)PQL. |
| `schema.name` | La clase en la que se basa el esquema que contiene el campo de atributo calculado. Ejemplo: `_xdm.context.experienceevent` para un esquema basado en la clase ExperienceEvent XDM. |

**Respuesta**

Un atributo calculado creado correctamente devuelve el estado HTTP 200 (OK) y un cuerpo de respuesta que contiene los detalles del atributo computado recién creado. Estos detalles incluyen un único, de sólo lectura, generado por el sistema `id` que puede utilizarse para hacer referencia al atributo calculado durante otras operaciones de API.

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "birthdayCurrentMonth",
    "path": "_{TENANT_ID}",
    "positionPath": [
        "_{TENANT_ID}"
    ],
    "description": "Computed attribute to capture if the customer birthday is in the current month.",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "person.birthDate.getMonth() = currentMonth()"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "string"
    },
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
    "dependencies": [],
    "dependents": [],
    "active": true,
    "type": "ComputedAttribute",
    "createEpoch": 1572555223,
    "updateEpoch": 1572555225
}
```

| Propiedad | Descripción |
|---|---|
| `id` | ID único, de sólo lectura, generado por el sistema que se puede utilizar para hacer referencia al atributo calculado durante otras operaciones de API. |
| `imsOrgId` | La organización de IMS relacionada con el atributo calculado debe coincidir con el valor enviado en la solicitud. |
| `sandbox` | El objeto sandbox contiene detalles del entorno limitado en el que se configuró el atributo calculado. Esta información se obtiene a partir del encabezado del simulador para pruebas enviado en la solicitud. Para obtener más información, consulte la descripción general [de los](../../sandboxes/home.md)entornos limitados. |
| `positionPath` | Matriz que contiene el campo desconstruido `path` al que se envió la solicitud. |
| `returnSchema.meta:xdmType` | Tipo del campo en el que se almacenará el atributo calculado. |
| `definedOn` | Una matriz que muestra los esquemas de unión en los que se ha definido el atributo calculado. Contiene un objeto por esquema de unión, lo que significa que puede haber varios objetos dentro de la matriz si el atributo calculado se ha agregado a varios esquemas en función de diferentes clases. |
| `active` | Un valor booleano que muestra si el atributo calculado está activo o no. De forma predeterminada, el valor es `true`. |
| `type` | El tipo de recurso creado, en este caso &quot;ComputedAttribute&quot; es el valor predeterminado. |
| `createEpoch` y `updateEpoch` | Hora a la que se creó y actualizó por última vez el atributo calculado, respectivamente. |


## Acceso a atributos calculados

Al trabajar con atributos calculados mediante la API, hay dos opciones para acceder a atributos calculados que han sido definidas por su organización. La primera es la lista de todos los atributos calculados; la segunda es la vista de un atributo calculado específico por su único `id`.

Los pasos para enumerar todos los atributos calculados y para ver un atributo calculado específico se describen en las secciones siguientes.

### Atributos calculados de lista {#list-computed-attributes}

La organización de IMS puede crear varios atributos calculados y realizar una solicitud de GET al extremo permite realizar la lista de todos los atributos calculados existentes para la organización. `/config/computedAttributes`

**Formato API**

```http
GET /config/computedAttributes
```

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

Una respuesta correcta incluye un `_page` atributo que proporciona el número total de atributos calculados (`totalCount`) y el número de atributos calculados en la página (`pageSize`).

La respuesta también incluye una `children` matriz compuesta por uno o más objetos, cada uno de los cuales contiene los detalles de un atributo calculado. Si su organización no tiene atributos calculados, la matriz `totalCount` y `pageSize` `children` será 0 (cero) y la matriz estará vacía.

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "2afcf410-450e-4a39-984d-2de99ab58877",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "birthdayCurrentMonth",
            "path": "person._{TENANT_ID}",
            "positionPath": [
                "person",
                "_{TENANT_ID}"
            ],
            "description": "Computed attribute to capture if the customer birthday is in the current month.",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "person.birthDate.getMonth() = currentMonth()"
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "returnSchema": {
                "meta:xdmType": "string"
            },
            "definedOn": [
                {
                    "meta:resourceType": "unions",
                    "meta:containerId": "tenant",
                    "$ref": "https://ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
            "dependencies": [],
            "dependents": [],
            "active": true,
            "type": "ComputedAttribute",
            "createEpoch": 1572555223,
            "updateEpoch": 1572555225
        },
        {
            "id": "ae0c6552-cf49-4725-8979-116366e8e8d3",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "productDownloads",
            "path": "_{TENANT_ID}",
            "positionPath": [
                "_{TENANT_ID}"
            ],
            "description": "Calculate total product downloads.",
            "expression": {
                "type" : "PQL", 
                "format" : "pql/text", 
                "value":  "let Y = xEvent[_coresvc.event.subType = \"DOWNLOAD\"].groupBy(_coresvc.attributes[name = \"product\"].value).map({
                  \"downloaded\": this.head()._coresvc.attributes[name = \"product\"].head().value,
                  \"downloadsSum\": this.count(),
                  \"downloadsToday\": this[timestamp occurs today].count(),
                  \"downloadsPast30Days\": this[timestamp occurs < 30 days before now].count(),
                  \"downloadsPast60Days\": this[timestamp occurs < 60 days before now].count(),
                  \"downloadsPast90Days\": this[timestamp occurs < 90 days before now].count() }) in { \"uniqueProductDownloadSum\": Y.count(), \"products\": Y }"
            },
            "returnSchema": {
                "meta:xdmType": "string"
            },
            "definedOn": [
                {
                    "meta:resourceType": "unions",
                    "meta:containerId": "tenant",
                    "$ref": "https://ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "schema": {
                "name": "_xdm.context.profile"
            },
            "encodedDefinedOn": "\u001f?\b\u0000\u0000\u0000\u0000\u0000\u0000\u0000?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?\u0005\u00008{?E:\u0000\u0000\u0000",
            "dependencies": [],
            "dependents": [],
            "active": true,
            "type": "ComputedAttribute",
            "createEpoch": 1571945277,
            "updateEpoch": 1571945280
        }
    ],
    "_links": {
        "next": {}
    }
}
```

| Propiedad | Descripción |
|---|---|
| `_page.totalCount` | El número total de atributos calculados definidos por la organización de IMS. |
| `_page.pageSize` | El número de atributos calculados devueltos en esta página de resultados. Si `pageSize` es igual a `totalCount`, significa que solo hay una página de resultados y se han devuelto todos los atributos calculados. Si no son iguales, hay páginas adicionales de resultados a las que se puede acceder. Consulte `_links.next` para obtener más información. |
| `children` | Matriz compuesta de uno o varios objetos, cada uno de los cuales contiene los detalles de un único atributo calculado. Si no se han definido atributos calculados, la `children` matriz está vacía. |
| `id` | Un valor único, de sólo lectura, generado por el sistema y asignado automáticamente a un atributo calculado cuando se crea. Para obtener más información sobre los componentes de un objeto de atributo calculado, consulte la sección sobre la [creación de un atributo](#create-a-computed-attribute) calculado anteriormente en este tutorial. |
| `_links.next` | Si se devuelve una sola página de atributos calculados, `_links.next` es un objeto vacío, como se muestra en la respuesta de ejemplo anterior. Si su organización tiene muchos atributos calculados, se devolverán en varias páginas a las que puede acceder realizando una solicitud de GET al `_links.next` valor. |

### Vista de un atributo calculado {#view-a-computed-attribute}

También puede realizar una vista de un atributo calculado específico mediante una solicitud de GET al extremo e incluyendo el ID de atributo calculado en la ruta de la solicitud. `/config/computedAttributes`

**Formato API**

```http
GET /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parámetro | Descripción |
|---|---|
| `{ATTRIBUTE_ID}` | ID del atributo calculado que desea vista. |

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/2afcf410-450e-4a39-984d-2de99ab58877 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "birthdayCurrentMonth",
    "path": "_{TENANT_ID}",
    "positionPath": [
        "_{TENANT_ID}"
    ],
    "description": "Computed attribute to capture if the customer birthday is in the current month.",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "person.birthDate.getMonth() = currentMonth()"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "string"
    },
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
    "dependencies": [],
    "dependents": [],
    "active": true,
    "type": "ComputedAttribute",
    "createEpoch": 1572555223,
    "updateEpoch": 1572555225
}
```

## Actualizar un atributo calculado

En caso de que necesite actualizar un atributo calculado existente, esto se puede hacer haciendo una solicitud de PATCH al extremo e incluyendo el ID del atributo calculado que desea actualizar en la ruta de la solicitud. `/config/computedAttributes`

**Formato API**

```http
PATCH /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parámetro | Descripción |
|---|---|
| `{ATTRIBUTE_ID}` | ID del atributo calculado que desea actualizar. |

**Solicitud**

Esta solicitud utiliza el formato [Parche](http://jsonpatch.com/) JSON para actualizar el &quot;valor&quot; del campo &quot;expresión&quot;.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'\
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \  
  -d '[
        {
          "op": "add",
          "path": "/expression",
          "value": 
          {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "{NEW_EXPRESSION_VALUE}"
          }
        }
      ]'
```

| Propiedad | Descripción |
|---|---|
| `{NEW_EXPRESSION_VALUE}` | Una expresión válida [!DNL Profile Query Language] (PQL). Para obtener más información sobre PQL y vínculos a consultas compatibles, lea la descripción general [de](../../segmentation/pql/overview.md)PQL. |

**Respuesta**

Una actualización correcta devuelve el estado HTTP 204 (sin contenido) y un cuerpo de respuesta vacío. Si desea confirmar que la actualización se ha realizado correctamente, puede realizar una solicitud de GET para vista del atributo calculado por su ID.

## Eliminar un atributo calculado

También es posible eliminar un atributo calculado mediante la API. Esto se lleva a cabo realizando una solicitud de DELETE al extremo e incluyendo el ID del atributo calculado que desea eliminar en la ruta de la solicitud. `/config/computedAttributes`

>[!NOTE]
>
>Tenga cuidado al eliminar un atributo calculado, ya que puede estar en uso en más de un esquema y la operación de DELETE no se puede deshacer.

**Formato API**

```http
DELETE /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parámetro | Descripción |
|---|---|
| `{ATTRIBUTE_ID}` | ID del atributo calculado que desea eliminar. |

**Solicitud**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \ 
```

**Respuesta**

Una solicitud de eliminación correcta devuelve Estado HTTP 200 (Aceptar) y un cuerpo de respuesta vacío. Para confirmar que la eliminación se ha realizado correctamente, puede realizar una solicitud de GET para buscar el atributo calculado por su ID. Si se eliminó el atributo, recibirá un error de estado HTTP 404 (no encontrado).

## Pasos siguientes

Ahora que ha aprendido los conceptos básicos de los atributos calculados, está listo para empezar a definirlos para su organización.