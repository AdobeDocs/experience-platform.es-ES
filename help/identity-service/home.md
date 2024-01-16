---
keywords: Experience Platform;inicio;temas populares;identidad;Identity;gráficos XDM;servicio de identidad;servicio de identidad
solution: Experience Platform
title: Resumen del servicio de identidad
description: El servicio de identidad de Adobe Experience Platform le ayuda a obtener una mejor vista de su cliente y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales impactantes en tiempo real.
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: 484b1c2d37291afd02fe58723121325c837061aa
workflow-type: tm+mt
source-wordcount: '1524'
ht-degree: 2%

---

# Servicio de ID de Adobe Experience Platform

Para ofrecer experiencias digitales relevantes, necesita una representación completa y precisa de las entidades del mundo real que conforman su base de clientes.

Las organizaciones y empresas de hoy en día se enfrentan a un gran volumen de conjuntos de datos dispares: sus clientes individuales están representados por una variedad de identificadores diferentes. Su cliente puede estar vinculado a diferentes exploradores web (Safari, Google Chrome), dispositivos de hardware (teléfonos, portátiles) y otros identificadores de persona (ID de CRM, cuentas de correo electrónico). Esto crea una vista desarticulada del cliente.

Puede solucionar estos desafíos con el servicio de identidad de Adobe Experience Platform y sus capacidades para lo siguiente:

* Generación de un **gráfico de identidad** que vincula identidades dispares, lo que le proporciona una representación visual de cómo un cliente interactúa con su marca en diferentes canales.
* Cree un gráfico para el Perfil del cliente en tiempo real, que luego se utiliza para crear una vista completa del cliente combinando atributos y comportamientos.
* Realice la validación y la depuración utilizando las distintas herramientas.

Este documento proporciona información general sobre el servicio de ID y cómo puede utilizar sus funcionalidades en el contexto de Experience Platform.

## Terminología {#terminology}

Antes de sumergirse en los detalles del servicio de identidad, lea la siguiente tabla para obtener un resumen de los términos clave:

| Término | Definición |
| --- | --- |
| Identidad | Una identidad son datos que son únicos para una entidad. Normalmente, se trata de un objeto del mundo real, como una persona individual, un dispositivo de hardware o un explorador web (representado por una cookie). Una identidad completa consta de dos elementos: un **área de nombres de identidad** y un **valor de identidad**. |
| Espacio de nombre de identidad | Un área de nombres de identidad es el contexto de una identidad determinada. Por ejemplo, un área de nombres de `Email` podría corresponder con **julien<span>@acme.com**. Del mismo modo, un área de nombres de `Phone` podría corresponder con `555-555-1234`. Para obtener más información, lea la [información general del área de nombres de identidad](./namespaces.md) |
| Valor de identidad | Un valor de identidad es una cadena que representa una entidad del mundo real y que se clasifica dentro del servicio de identidad a través de un área de nombres. Por ejemplo, el valor de identidad (cadena) **julien<span>@acme.com** podría clasificarse como un `Email` namespace. |
| Tipo de identidad | Un tipo de identidad es un componente de un área de nombres de identidad. El tipo de identidad designa si los datos de identidad están vinculados en un gráfico de identidad o no. |
| Vínculo | Un vínculo o una vinculación es un método para establecer que dos identidades diferentes representan la misma entidad. Por ejemplo, un vínculo entre &quot;`Email` = julien<span>@acme.com&quot; y &quot;`Phone` = 555-555-1234&quot; significa que ambas identidades representan la misma entidad. Esto sugiere que el cliente que ha interactuado con su marca con la dirección de correo electrónico de Julien<span>@acme.com y el número de teléfono de 555-555-1234 es el mismo. |
| Servicio de identidad | El servicio de identidad es un servicio dentro de Experience Platform que vincula (o desvincula) identidades para mantener gráficos de identidad. |
| Gráfico de identidad | El gráfico de identidad es una colección de identidades que representan a un solo cliente. Para obtener más información, lea la guía de [uso del visualizador de gráficos de identidad](./ui/identity-graph-viewer.md). |
| Perfil del cliente en tiempo real | El perfil del cliente en tiempo real es un servicio de Adobe Experience Platform que: <ul><li>Combina fragmentos de perfiles para crear un perfil basado en un gráfico de identidad.</li><li>Segmenta los perfiles para que luego se puedan enviar al destino para que los active.</li></ul> |
| Perfil | Un perfil es una representación de un sujeto, una organización o un individuo. Un perfil se compone de cuatro elementos: <ul><li>Atributos: los atributos proporcionan información como nombre, edad o sexo.</li><li>Comportamiento: los comportamientos proporcionan información sobre las actividades de un perfil determinado. Por ejemplo, un comportamiento de perfil puede saber si un perfil determinado estaba &quot;buscando sandalias&quot; o &quot;pidiendo camisetas&quot;.</li><li>Identidades: Para un perfil combinado, proporciona información de todas las identidades asociadas con la persona. Las identidades se pueden clasificar en tres categorías: persona (CRMID, correo electrónico, teléfono), dispositivo (IDFA, GAID) y cookie (ECID, AAID).</li><li>Pertenencia a audiencias: Los grupos a los que pertenece el perfil (usuarios fieles, usuarios que viven en California, etc.)</li></ul> |

{style="table-layout:auto"}

## ¿Qué es el servicio de identidad?

![Vinculación de identidad en Platform](./images/identity-service-stitching.png)

En un contexto de empresa a cliente (B2C), los clientes interactúan con su negocio y establecen una relación con su marca. Un cliente típico puede estar activo en cualquier sistema de la infraestructura de datos de su organización. Cualquier cliente dado puede estar activo dentro de sus sistemas de comercio electrónico, lealtad y servicio de asistencia. Ese mismo cliente también puede interactuar de forma anónima o a través de medios autenticados en cualquier número de dispositivos diferentes.

Piense en el siguiente recorrido del cliente:

* Julien ha creado una cuenta en su sitio web de comercio electrónico y ha pedido algunos artículos en el pasado. Julien suele usar su portátil personal para realizar compras e iniciar sesión en su cuenta cada vez que lo usa.
* Sin embargo, durante una de sus visitas a su sitio, utiliza una tableta para buscar sandalias. Durante esta sesión, como utilizó un dispositivo diferente, no inicia sesión ni realiza un pedido.
* En este punto, las actividades de Julien se representan en dos perfiles separados:
   * Su primer perfil es su ID de inicio de sesión en comercio electrónico. Este perfil se utiliza cuando utiliza una combinación de nombre de usuario y contraseña para autenticar su sesión en el sitio de comercio electrónico. Este perfil se identifica mediante un identificador entre dispositivos.
   * Su segundo perfil es su tablet. Este perfil se creó después de que explorara el sitio de comercio electrónico de forma anónima mediante una tableta sin iniciar sesión en su cuenta. Este perfil se identifica mediante un identificador de cookie.
* Más tarde, Julien reanuda su sesión de tableta. Sin embargo, esta vez inicia sesión en su cuenta. Como resultado, el servicio de identidad ahora relaciona la actividad del dispositivo tablet de Julien con su ID de inicio de sesión en comercio electrónico.
* En adelante, el contenido de destino podría reflejar el perfil completo, el historial de compras y la actividad de navegación anónima de Julien.

>[!IMPORTANT]
>
>Puede utilizar el servicio de identidad para vincular identidades y recopilar una imagen completa de su cliente que, de lo contrario, podría estar dispersa en diferentes sistemas.

## ¿Qué hace el servicio de identidad?

El servicio de identidad proporciona las siguientes operaciones para lograr su misión:

* Cree áreas de nombres personalizadas para adaptarlas a las necesidades de su organización.
* Crear, actualizar y ver gráficos de identidad.
* Elimine identidades basadas en conjuntos de datos.
* Eliminar identidades para garantizar el cumplimiento de la normativa.

## Cómo vincula el servicio de identidad las identidades

Se establece un vínculo entre dos identidades cuando coinciden el área de nombres de identidad y los valores de identidad.

Un evento de inicio de sesión típico **envía dos identidades** en el Experience Platform:

* El identificador de persona (como un ID de CRM) que representa a un usuario autenticado.
* El identificador del explorador (como un ECID) que representa el explorador web.

Consideremos el siguiente ejemplo:

* Inicia sesión con la combinación de nombre de usuario y contraseña en un sitio web de comercio electrónico con el ordenador portátil. Este evento lo califica como usuario autenticado, por lo que el servicio de identidad reconoce su ID de CRM.
* Identity Service también reconoce el uso de un explorador para acceder al sitio web de comercio electrónico como un evento. Este evento se representa en el servicio de identidad a través de un ECID.
* Entre bastidores, el servicio de identidad procesa los dos eventos como: `CRM_ID:ABC, ECID:123`.
   * ID de CRM: ABC es el área de nombres y el valor que le representa a usted, como usuario autenticado.
   * ECID: 123 es el área de nombres y el valor que representa el uso del explorador web en el equipo portátil.
* A continuación, si inicia sesión con las mismas credenciales en el mismo sitio web de comercio electrónico, pero utiliza el explorador web del teléfono en lugar del explorador web del portátil, se registra un nuevo ECID en el servicio de identidad.
* El servicio de identidad procesa este nuevo evento en segundo plano como `{CRM_ID:ABC, ECID:456}`, donde CRM_ID: ABC representa su ID de cliente autenticado y ECID:456 representa el explorador web de su dispositivo móvil.

Teniendo en cuenta los escenarios anteriores, el servicio de identidad establece un vínculo entre `{CRM_ID:ABC, ECID:123}`, así como `{CRM_ID:ABC, ECID:456}`. Esto da como resultado un gráfico de identidades en el que &quot;posee&quot; tres identidades: una para el identificador de persona (CRM ID) y dos para los identificadores de cookie (ECID).

## Gráficos de identidad

Un gráfico de identidad es un mapa de relaciones entre diferentes áreas de nombres de identidad, que le permite visualizar y comprender mejor qué identidades de clientes se vinculan entre sí y cómo. Lea el tutorial sobre [uso del visualizador de gráficos de identidad](./ui/identity-graph-viewer.md) para obtener más información.

El siguiente vídeo tiene como objetivo ayudarle a comprender las identidades y los gráficos de identidad.

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

## Explicación de la función del servicio de identidad dentro de la infraestructura de Experience Platform

El servicio de identidad desempeña un papel vital dentro del Experience Platform. Algunas de estas integraciones clave son las siguientes:

* [Esquemas](../xdm/home.md): Dentro de un esquema determinado, los campos de esquema marcados como identidad permiten crear gráficos de identidad.
* [Conjuntos de datos](../catalog/datasets/overview.md): Cuando un conjunto de datos está habilitado para su ingesta en el Perfil del cliente en tiempo real, los gráficos de identidad se generan a partir del conjunto de datos, dado que el conjunto de datos tiene al menos dos campos marcados como identidad.
* [SDK web](../edge/home.md): el SDK web envía eventos de experiencia a Adobe Experience Platform y el servicio de identidad genera un gráfico cuando existen dos o más identidades en el evento.
* [Perfil del cliente en tiempo real](../profile/home.md): Antes de combinar atributos y eventos para un perfil determinado, el perfil del cliente en tiempo real podría hacer referencia al gráfico de identidades.
* [Destinos](../destinations/home.md): los destinos pueden enviar información de perfil a otros sistemas en función de un área de nombres de identidad, como correo electrónico con hash.
* [Coincidencia de segmentos](../segmentation/ui/segment-match/overview.md): la coincidencia de segmentos coincide con dos perfiles en dos zonas protegidas diferentes que tienen el mismo área de nombres de identidad y valor de identidad.
* [Privacy Service](../privacy-service/home.md): Si la solicitud de eliminación incluye `identity`, la combinación de área de nombres y valor de identidad especificada se puede eliminar del servicio de identidad mediante la función de procesamiento de solicitudes de privacidad de Privacy Service.

