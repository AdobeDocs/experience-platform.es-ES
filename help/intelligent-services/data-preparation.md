---
keywords: Experience Platform;home;intelligent services;popular topics
solution: Experience Platform
title: Preparación de datos para su uso en Servicios inteligentes
topic: Intelligent Services
translation-type: tm+mt
source-git-commit: 1d827d1637da05d3d2afc338f48911bb23039949

---


# Preparación de datos para su uso en Servicios inteligentes

Para que los servicios inteligentes puedan descubrir perspectivas a partir de los datos de eventos de marketing, los datos deben enriquecirse y mantenerse semánticamente en una estructura estándar. Los servicios inteligentes aprovechan los esquemas del modelo de datos de experiencia (XDM) para lograr esto. Concretamente, todos los conjuntos de datos que se utilizan en Servicios inteligentes deben cumplir el esquema XDM de los Eventos de experiencias **de consumo (CEE)** .

Este documento proporciona una guía general sobre cómo asignar los datos de eventos de marketing de varios canales a este esquema, esbozando información sobre los campos importantes dentro del esquema para ayudarle a determinar cómo asignar los datos de manera efectiva a su estructura.

## Explicación del esquema de CEE

El esquema Consumer ExperienceEvent describe el comportamiento de una persona en relación con eventos de marketing digital (web o móvil), así como con la actividad comercial en línea o sin conexión. El uso de este esquema es necesario para Servicios Inteligentes debido a sus campos (columnas) semánticamente bien definidos, evitando nombres desconocidos que de otra manera harían que los datos fueran menos claros.

Al igual que todos los esquemas XDM, la mezcla CEE es extensible. En otras palabras, se pueden agregar campos adicionales a la mezcla CEE y, si es necesario, se pueden incluir variaciones diferentes en varios esquemas.

Puede encontrarse un ejemplo completo de la mezcla en el repositorio [XDM](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md)público y debe utilizarse como referencia para los campos clave descritos en la sección siguiente.

### Campos clave

En la tabla siguiente se destacan los campos clave dentro de la mezcla CEE que deben utilizarse para que los servicios inteligentes generen perspectivas útiles, incluidas descripciones y vínculos a documentación de referencia para obtener más ejemplos.

| Campo XDM | Descripción | Referencia |
| --- | --- | --- |
| `xdm:channel` | El canal de marketing relacionado con ExperienceEvent. El campo incluye información sobre el tipo de canal, el tipo de medio y el tipo de ubicación. **Este campo _debe_proporcionarse para que la API de atribución funcione con sus datos**. Consulte la [tabla siguiente](#example-channels) para ver algunas asignaciones de ejemplo. | [esquema de Experience canal](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md) |
| `xdm:productListItems` | Una matriz de artículos que representan los productos seleccionados por un cliente, incluido el SKU del producto, el nombre, el precio y la cantidad. | [esquema de detalles del comercio](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) |
| `xdm:commerce` | Contiene información específica sobre el comercio acerca de ExperienceEvent, incluido el número de orden de compra y la información de pago. | [esquema de detalles del comercio](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) |
| `xdm:web` | Representa los detalles web relacionados con ExperienceEvent, como la interacción, los detalles de la página y el remitente del reenvío. | [esquema de detalles web de ExperienceEvent](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md) |

### canales de ejemplo {#example-channels}

El `xdm:channel` campo representa el canal de marketing relacionado con ExperienceEvent. En la tabla siguiente se proporcionan algunos ejemplos de canales de marketing asignados a XDM:

| Canal | `channel.mediaType` | `channel._type` | `channel.mediaAction` |
| --- | --- | --- | --- |
| Búsqueda de pago | PAGADO | BUSCAR | HAGA CLIC EN |
| Social - Marketing | GANADO | SOCIAL | HAGA CLIC EN |
| Mostrar  | PAGADO | MOSTRAR | HAGA CLIC EN |
| Correo electrónico | PAGADO | CORREO ELECTRÓNICO | HAGA CLIC EN |
| Remitente del reenvío interno | PROPIEDAD | DIRECTO | HAGA CLIC EN |
| Visualización de visualizaciones | PAGADO | MOSTRAR | IMPRESIÓN |
| Redirección de código QR | PROPIEDAD | DIRECTO | HAGA CLIC EN |
| Mensaje de texto SMS | PROPIEDAD | SMS | HAGA CLIC EN |
| Dispositivo móvil | PROPIEDAD | MÓVIL | HAGA CLIC EN |

## Asignación e ingesta de datos

Una vez que haya determinado si los datos de la serie temporal se pueden asignar al esquema de CEE, podrá realizar el inicio del proceso de ingreso de los datos a los servicios inteligentes. Póngase en contacto con los servicios de consultoría de Adobe para ayudarle a asignar los datos al esquema y a incorporarlos al servicio.

Si tiene una suscripción de Adobe Experience Platform y desea asignar e ingestar los datos usted mismo, siga los pasos descritos en la sección siguiente.

### Uso de Adobe Experience Platform

>[!NOTE] Los pasos a continuación requieren una suscripción a la plataforma de experiencia. Si no tiene acceso a Plataforma, vaya a la sección de [próximos pasos](#next-steps) .

En esta sección se describe el flujo de trabajo para asignar e ingestar datos en la plataforma de experiencias para su uso en los servicios inteligentes, incluidos los vínculos a tutoriales para ver los pasos detallados.

#### Crear un esquema y un conjunto de datos de CEE

Cuando esté listo para el inicio de preparar sus datos para la ingestión, el primer paso es crear un nuevo esquema XDM que emplee la mezcla CEE. Los siguientes tutoriales explican el proceso de creación de un nuevo esquema en la interfaz de usuario o la API:

* [Creación de un esquema en la interfaz de usuario](../xdm/tutorials/create-schema-ui.md)
* [Creación de un esquema en la API](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT] Los tutoriales anteriores siguen un flujo de trabajo genérico para crear un esquema. Al elegir una clase para el esquema, debe utilizar la clase **ExperienceEvent de** XDM. Una vez seleccionada esta clase, puede agregar la mezcla CEE al esquema.

Después de agregar la mezcla CEE al esquema, puede agregar otras mezclas según sea necesario para campos adicionales dentro de los datos.

Una vez creado y guardado el esquema, puede crear un nuevo conjunto de datos basado en ese esquema. Los siguientes tutoriales explican el proceso de creación de un nuevo conjunto de datos en la interfaz de usuario o la API:

* [Crear un conjunto de datos en la interfaz de usuario](../catalog/datasets/user-guide.md#create) (siga el flujo de trabajo para usar un esquema existente)
* [Creación de un conjunto de datos en la API](../catalog/datasets/create.md)

#### Asignar y transferir datos

Después de crear un esquema y un conjunto de datos de CEE, puede asignar inicios a las tablas de datos en el esquema e ingerirlos en la plataforma. Consulte el tutorial sobre la [asignación de un archivo CSV a un esquema](../ingestion/tutorials/map-a-csv-file.md) XDM para ver los pasos para realizar esto en la interfaz de usuario. Una vez que se ha rellenado un conjunto de datos, se puede utilizar el mismo conjunto de datos para ingestar archivos de datos adicionales.

## Pasos siguientes {#next-steps}

Este documento proporciona una guía general sobre la preparación de los datos para su uso en Servicios inteligentes. Si necesita asesoramiento adicional en función de su caso de uso, póngase en contacto con la asistencia de consultoría de Adobe.

Una vez que haya rellenado correctamente un conjunto de datos con los datos de experiencia del cliente, puede utilizar Servicios inteligentes para generar perspectivas. Consulte los siguientes documentos para empezar:

* [Información general de Atribución de IA](./attribution-ai/overview.md)
* [Información general sobre el AI del cliente](./customer-ai/overview.md)
