---
keywords: Experience Platform;inicio;temas populares;identidad;identidad;gráficos XDM;servicio de identidad;servicio de identidad
solution: Experience Platform
title: Información general del servicio de identidad
topic: sobre validación
description: El servicio de ID de Adobe Experience Platform le ayuda a obtener una mejor vista de su cliente y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales e impactantes en tiempo real.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '1733'
ht-degree: 0%

---


# Información general del [!DNL Identity Service]

La entrega de experiencias digitales relevantes requiere una comprensión completa de su cliente. Esto se hace más difícil cuando los datos de sus clientes están fragmentados en distintos sistemas, lo que hace que cada cliente individual parezca tener múltiples &quot;identidades&quot;. Adobe Experience Platform [!DNL Identity Service] le ayuda a obtener una mejor vista de su cliente y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales e impactantes en tiempo real.

## Explicación [!DNL Identity Service]

Cada día, los clientes interactúan con su empresa y establecen una relación cada vez más estrecha con su marca. Un cliente típico puede estar activo en cualquier cantidad de sistemas dentro de la infraestructura de datos de su organización, como su sistema de comercio electrónico, lealtad y asistencia técnica. Ese mismo cliente también puede participar de forma anónima en cualquier número de dispositivos. [!DNL Identity Service] le permite crear una imagen completa de su cliente, agregando datos relacionados que, de lo contrario, se podrían ocultar en distintos sistemas.

Veamos un ejemplo cotidiano de la relación de un consumidor con su marca:

Mary tiene una cuenta en su sitio de comercio electrónico donde ha completado algunos pedidos en el pasado. Ella suele usar su laptop personal para comprar, donde inicia sesión cada vez. Sin embargo, durante una de sus visitas usa su tableta para comprar sandalias, pero no realiza un pedido y no inicia sesión.

En este punto, la actividad de Mary aparece como dos perfiles separados: su inicio de sesión en eCommerce y su dispositivo tableta, tal vez identificado por el ID del dispositivo.

Más tarde, Mary reanuda su sesión en la tableta y proporciona su dirección de correo electrónico cuando se suscribe a la newsletter. Al hacerlo, la transmisión por secuencias de ingesta agrega una nueva identidad como datos de registro dentro de su perfil. Como resultado, [!DNL Identity Service] ahora relaciona la actividad de los dispositivos de tableta de Mary con su historial de cuentas de comercio electrónico.

Al hacer clic en su tableta, el contenido objetivo podría reflejar el perfil completo y la historia de Mary, en lugar de una tableta usada por un comprador desconocido.

[!DNL Real-time Customer Profile] aprovecha las relaciones de identidad que [!DNL Identity Service] define y mantiene para crear una imagen completa de un cliente y sus interacciones con su marca. Para obtener más información, consulte la [Descripción general del perfil del cliente en tiempo real](../profile/home.md).

### Identidades

Una identidad es datos que son exclusivos de una entidad, normalmente de una persona individual. Una identidad como, por ejemplo, un ID de inicio de sesión, un ECID o un ID de lealtad se denomina identidad conocida.

La PII, como la dirección de correo electrónico y el número de teléfono, sirve para identificar directamente a un cliente. Como resultado, la PII se utiliza para hacer coincidir las múltiples identidades de un cliente en todos los sistemas.

Identidades desconocidas o anónimas identifican un dispositivo sin identificar a la persona real que lo utiliza. Esta categoría incluye información como la dirección IP de un visitante y el ID de cookie. Aunque los datos de comportamiento se pueden recopilar de un dispositivo que utiliza identidades desconocidas, la asociación de estas identidades entre dispositivos o medios está limitada hasta que el cliente proporcione PII durante su recorrido.

Como se muestra en la imagen siguiente, las identidades conocidas y anónimas son componentes importantes de los [gráficos de identidad](#identity-graphs), que se tratan más adelante en este documento.

![Vinculación de identidad en la plataforma](./images/identity-service-stitching.png)

Algunos ejemplos de implementaciones de [!DNL Identity Service] son:

- Una empresa de telecomunicaciones puede confiar en el valor &quot;número de teléfono&quot;, en el que un número de teléfono hace referencia a la misma persona de interés tanto en los conjuntos de datos en línea como sin conexión.
- Una empresa minorista puede utilizar &quot;dirección de correo electrónico&quot; en conjuntos de datos sin conexión y ECID en conjuntos de datos en línea, debido al alto porcentaje de visitantes anónimos.
- Un banco puede preferir el &quot;número de cuenta&quot; en conjuntos de datos sin conexión, como las transacciones de sucursales. Pueden depender del &quot;ID de inicio de sesión&quot; en los conjuntos de datos en línea, ya que la mayoría de los visitantes se autenticarían durante su visita.
- Los clientes también pueden tener ID propietarios únicos, como GUID u otros identificadores únicos universales.

### Datos de identidad

Si le preguntaste a una persona &quot;¿Cuál es tu ID?&quot; sin más contexto, les resultaría difícil dar una respuesta útil. Con la misma lógica, un valor de cadena que representa un valor de identidad, ya sea un ID generado por el sistema o una dirección de correo electrónico, solo se completa cuando se proporciona con un calificador que proporciona el contexto del valor de cadena: el área de nombres de identidad.

## Espacios de nombres de identidad y gráficos de identidad

Los clientes pueden interactuar con su marca mediante una combinación de canales en línea y sin conexión, lo que resulta en el desafío de cómo reconciliar esas interacciones fragmentadas en una sola identidad de cliente.

[!DNL Experience Platform] aborda este desafío mediante dos conceptos:  [áreas de ](#identity-namespaces) nombres de identidad y gráficos de  [identidad](#identity-graphs).

El siguiente vídeo está diseñado para ayudar a comprender las identidades y los gráficos de identidad. El siguiente vídeo cubre las tres capacidades de la recopilación de identidades, los gráficos de identidad y las API. También describe cómo se utilizan los algoritmos determinísticos y probabilísticos para construir gráficos de identidad privados y analiza el papel de los gráficos de identidad privados, el gráfico de cooperación del servicio de identidad de Adobe Experience Platform y los gráficos de terceros.

>[!IMPORTANT]
>
> Los gráficos privados probabilísticos aún se están desarrollando y se van a publicar en una fecha posterior.

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

### Espacios de nombres de identidad

Cuando el cliente interactúa con la marca en varios canales, incluidos la web, la aplicación móvil, el centro de llamadas o una tienda, puede resultar difícil entenderlas y servirlas si no puede observar y rastrear su actividad en varios canales.

Comprender al cliente en varios dispositivos y canales comienza reconociéndolos en cada canal. Adobe Experience Platform logra esto utilizando áreas de nombres de identidad.
Un área de nombres de identidad es un identificador como el ID del dispositivo o el ID de correo electrónico que se utiliza para proporcionar el contexto desde el que se originan los datos. Las áreas de nombres de identidad se utilizan para buscar o vincular identidades individuales y proporcionan contexto para los valores de identidad a fin de evitar conflictos de datos. Por ejemplo, el ID &quot;123456&quot; puede referirse a una persona del sistema de comercio electrónico y a otra del sistema de asistencia técnica. Para obtener más información, consulte la [descripción general del área de nombres de identidad](./namespaces.md).

### Gráficos de identidad

Un gráfico de identidad es un mapa de relaciones entre diferentes áreas de nombres de identidad, que proporciona una representación visual de cómo el cliente interactúa con la marca a través de diferentes canales.

[!DNL Identity Service] administra y actualiza todos los gráficos de identidad de los clientes de forma colectiva casi en tiempo real como respuesta a la actividad de los clientes.

[!DNL Identity Service] administra un gráfico de identidad visible solo por su organización y creado en función de sus datos, denominado gráfico privado. [!DNL Identity Service] aumenta el gráfico privado cuando un registro de datos ingerido contiene más de una identidad, añadiendo una relación entre las identidades encontradas.

Como ejemplo de los posibles tipos de factores a tener en cuenta al suministrar y etiquetar datos de identidad, el uso de números de teléfono como &quot;teléfono de trabajo&quot; puede resultar en más relaciones de las que se pretenden en el gráfico de identidad. Es posible que muchos empleados se refieran al mismo número para trabajar, y que &quot;casa&quot; y &quot;móvil&quot; sirvan mejor para mantener las relaciones lo más precisas posible.

Para obtener más información, consulte el tutorial sobre [acceso al visor de gráficos de identidad](./ui/identity-graph-viewer.md)

## Envío de datos de identidad a [!DNL Identity Service]

En esta sección se explica cómo se procesan los datos proporcionados a Adobe Experience Platform antes de que [!DNL Identity Service] los utilice para crear un gráfico de identidad para cada cliente.

### Decidir sobre campos de identidad

Según la estrategia de recopilación de datos empresariales, los campos de datos que etiquete como identidades determinan qué datos se incluyen en el mapa de identidad. Para obtener el máximo beneficio de Adobe Experience Platform y las identidades de cliente más completas posibles, debe cargar datos en línea y sin conexión.

- Los datos en línea son datos que describen la presencia y el comportamiento en línea, como nombres de usuario y direcciones de correo electrónico.

- Los datos sin conexión se refieren a datos que no están directamente relacionados con la presencia en línea, como los ID de sistemas CRM. Este tipo de datos hace que sus identidades sean más sólidas y admite la cohesión de datos en todos sus sistemas dispares.

### Crear áreas de nombres de identidad adicionales

Mientras que [!DNL Experience Platform] ofrece una variedad de áreas de nombres estándar, es posible que necesite crear áreas de nombres adicionales para categorizar adecuadamente sus identidades. Para obtener más información, consulte la sección sobre [visualización y creación de áreas de nombres para su organización](./namespaces.md) en la descripción general del área de nombres de identidad.

>[!NOTE]
>
>Las áreas de nombres de identidad son un calificador para las identidades. Como resultado, una vez creado un espacio de nombres, no se puede eliminar.

### Incluir datos de identidad en [!DNL Experience Data Model] (XDM)

Como marco estandarizado mediante el cual [!DNL Platform] organiza los datos de los clientes, [!DNL Experience Data Model] (XDM) permite compartir y comprender los datos entre [!DNL Experience Platform] y otros servicios que interactúan con [!DNL Platform]. Para obtener más información, consulte [Información general del sistema XDM](../xdm/home.md).

Los esquemas de registros y series temporales proporcionan los medios para incluir datos de identidad. A medida que se incorporan los datos, el gráfico de identidad creará nuevas relaciones entre los fragmentos de datos de diferentes áreas de nombres si se encuentran que comparten datos de identidad comunes.

### Marcado de campos XDM como identidad

Cualquier campo de tipo `string` en esquemas que implementan clases XDM de registros o series temporales puede etiquetarse como campo de identidad. Como resultado, todos los datos introducidos en ese campo se considerarán datos de identidad.

Los campos de identidad también permiten la vinculación de identidades si comparten datos PII comunes.
Por ejemplo, al etiquetar los campos de número de teléfono como campos de identidad, [!DNL Identity Service] graba automáticamente las relaciones con las otras personas que se ha descubierto que utilizan el mismo número de teléfono.

>[!NOTE]
>
>El área de nombres de las identidades resultantes se proporciona en el momento en que se etiqueta el campo.

### Configurar un conjunto de datos para [!DNL Identity Service]

Durante el proceso de ingesta de flujo continuo, [!DNL Identity Service ]extrae automáticamente los datos de identidad de los datos de registros y series temporales. Sin embargo, para poder ingerir datos, estos deben habilitarse para [!DNL Identity Service]. Consulte el tutorial sobre [configuración de un conjunto de datos para el perfil del cliente en tiempo real y el servicio de identidad mediante API](../profile/tutorials/dataset-configuration.md) para obtener más información.

### Ingesta de datos a [!DNL Identity Service]

[!DNL Identity Service] consume datos compatibles con XDM que se envían a  [!DNL Experience Platform] mediante el  [interrogador de ](../ingestion/batch-ingestion/overview.md) lotes o la  [ingesta](../ingestion/streaming-ingestion/overview.md) de flujo continuo.

El siguiente vídeo está diseñado para admitir su comprensión del servicio de identidad. Este vídeo muestra cómo etiquetar campos de datos como identidades, ingerir datos de identidad y luego verificar que los datos hayan llegado al gráfico privado del servicio de identidad de Adobe Experience Platform.

>[!WARNING]
>
>La interfaz de usuario [!DNL Platform] que se muestra en el siguiente vídeo no está actualizada. Consulte la documentación para obtener las últimas capturas de pantalla y funciones de la interfaz de usuario.

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## Administración de datos

Adobe Experience Platform se ha creado teniendo en cuenta la privacidad e incluye un marco de control de datos para proteger los datos PII de sus clientes. Los datos de identidad en el espacio de nombres &quot;correo electrónico&quot; o &quot;teléfono&quot; se cifran de forma predeterminada, pero para garantizar que los datos confidenciales se cifran antes de que persistan, las etiquetas de uso de datos se pueden aplicar a los datos a medida que se incorporan o una vez que llegan a [!DNL Platform]. Para obtener más información, lea la [Información general sobre el control de datos](../data-governance/home.md).

## Pasos siguientes

Ahora que comprende los conceptos clave de [!DNL Identity Service] y su función dentro de [!DNL Experience Platform], puede empezar a aprender a trabajar con el gráfico de identidad utilizando [[!DNL Identity Service API]](./api/getting-started.md).
