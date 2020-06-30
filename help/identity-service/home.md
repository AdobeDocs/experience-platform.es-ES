---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Servicio de ID de Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 6ffdcc2143914e2ab41843a52dc92344ad51bcfb
workflow-type: tm+mt
source-wordcount: '1530'
ht-degree: 0%

---


# [!DNL Identity Service]sobre validación

La entrega de experiencias digitales relevantes requiere una comprensión completa de su cliente. Esto se hace más difícil cuando los datos de los clientes se fragmentan en distintos sistemas, lo que hace que cada cliente individual parezca tener múltiples &quot;identidades&quot;. Adobe Experience Platform [!DNL Identity Service] le ayuda a obtener una mejor vista de su cliente y su comportamiento al unir identidades entre dispositivos y sistemas, permitiéndole ofrecer experiencias digitales personales y impactantes en tiempo real.

## Explicación [!DNL Identity Service]

Cada día, los clientes interactúan con su negocio y establecen una relación de crecimiento continuo con su marca. Un cliente típico puede estar activo en cualquier cantidad de sistemas dentro de la infraestructura de datos de su organización, como los sistemas de comercio electrónico, lealtad y asistencia. Ese mismo cliente también puede participar anónimamente en cualquier número de dispositivos. [!DNL Identity Service] le permite crear una imagen completa de su cliente, agregando datos relacionados que, de otra manera, se podrían ocultar en distintos sistemas.

Veamos un ejemplo cotidiano de la relación de un consumidor con su marca:

Mary tiene una cuenta en su sitio de comercio electrónico donde ha completado algunos pedidos en el pasado. Normalmente usa su laptop personal para comprar, donde inicia sesión cada vez. Sin embargo, durante una de sus visitas usa su tableta para comprar sandalias, pero no realiza un pedido y no inicia sesión.

En este punto, la actividad de Mary aparece como dos perfiles separados: su inicio de sesión en eCommerce y su dispositivo tablet, tal vez identificados por el ID del dispositivo.

Más tarde, Mary reanuda su sesión de tablet y proporciona su dirección de correo electrónico mientras se suscribe a su newsletter. Al hacerlo, la transmisión por secuencias de ingestión añade una nueva identidad como datos de registro dentro de su perfil. Como resultado, [!DNL Identity Service] ahora relaciona la actividad de los dispositivos tablet de Mary con su historial de cuentas de comercio electrónico.

Al hacer clic en su tableta, el contenido objetivo podría reflejar el perfil y la historia completos de Mary, en lugar de una tableta utilizada por un comprador desconocido.

Las relaciones de identidad que [!DNL Identity Service] define y mantiene se aprovechan [!DNL Real-time Customer Profile] para crear una imagen completa de un cliente y sus interacciones con su marca. Para obtener más información, consulte la descripción general [del Perfil del cliente en tiempo](../profile/home.md)real.

### Identidades

Una identidad son datos que son exclusivos de una entidad, por lo general una persona individual. Una identidad como ID de inicio de sesión, ECID o ID de lealtad se denomina identidad **** conocida.

La PII, como la dirección de correo electrónico y el número de teléfono, sirve para identificar directamente a un cliente. Como resultado, la PII se utiliza para hacer coincidir las identidades múltiples de un cliente en todos los sistemas.

**Identidades** desconocidas o anónimas identifican un dispositivo sin identificar a la persona real que lo utiliza. Esta categoría incluye información como la dirección IP de un visitante y la ID de la cookie. Aunque los datos de comportamiento se pueden recopilar desde un dispositivo con identidades desconocidas, la asociación de estas identidades entre dispositivos o medios es limitada hasta que el cliente proporcione PII durante su viaje.

Como se muestra en la imagen siguiente, las identidades conocidas y anónimas son componentes importantes de los gráficos [de](#identity-graphs)identidad, que se analizan más adelante en este documento.

![Asociación de identidad en Platform](./images/identity-service-stitching.png)

Algunos ejemplos de [!DNL Identity Service] implementaciones son:

- Una compañía de telecomunicaciones puede basarse en el valor &quot;número de teléfono&quot;, donde un número de teléfono se referiría a la misma persona de interés en los conjuntos de datos en línea y sin conexión.
- Una compañía minorista puede utilizar &quot;dirección de correo electrónico&quot; en conjuntos de datos sin conexión y ECID en conjuntos de datos en línea debido al alto porcentaje de visitantes anónimos.
- Un banco puede preferir el &quot;número de cuenta&quot; en los conjuntos de datos sin conexión, como las transacciones de sucursales. Pueden depender del &quot;ID de inicio de sesión&quot; en los conjuntos de datos en línea, ya que la mayoría de los visitantes se autenticarían durante su visita.
- Es posible que sus clientes también tengan ID propietarios únicos, como GUID u otros identificadores únicos universales.

### Datos de identidad

Si le preguntaste a una persona &quot;¿Cuál es tu ID?&quot; sin más contexto, les resultaría difícil dar una respuesta útil. Según la misma lógica, un valor de cadena que representa un valor de identidad, ya sea un ID generado por el sistema o una dirección de correo electrónico, solo se completa cuando se proporciona un calificador que proporciona el contexto de valor de cadena: la Área de nombres de identidad.

## Áreas de nombres de identidad y gráficos de identidad

Sus clientes pueden interactuar con su marca mediante una combinación de canales en línea y sin conexión, lo que resulta en el desafío de cómo reconciliar esas interacciones fragmentadas en una sola identidad de cliente.

[!DNL Experience Platform] aborda este desafío a través de dos conceptos: [Áreas de nombres](#identity-namespaces) de identidad y gráficos [](#identity-graphs)de identidad.

### Áreas de nombres de identidad

Cuando el cliente interactúa con la marca en varios canales, como la web, la aplicación móvil, el centro de llamadas o una tienda, puede resultar difícil comprenderlos y ofrecerlos si no puede observar y rastrear su actividad en distintos canales.

Comprender a su cliente en varios dispositivos y inicios de canales reconociéndolos en cada canal. El Adobe Experience Platform lo logra mediante Áreas de nombres de identidad.
Una Área de nombres de identidad es un identificador como el ID del dispositivo o el ID de correo electrónico que se utiliza para proporcionar el contexto desde el que se originan los datos. Las Áreas de nombres de identidad se utilizan para buscar o vincular identidades individuales, y proporcionan contexto para los valores de identidad a fin de evitar conflictos de datos. Por ejemplo: la ID &quot;123456&quot; puede referirse a una persona en el sistema de comercio electrónico y a otra en el sistema de asistencia técnica. Para obtener más información, consulte la descripción general [de la Área de nombres de](./namespaces.md)identidad.

### Gráficos de identidad

Un gráfico de identidad es un mapa de las relaciones entre diferentes Áreas de nombres de identidad, que le proporciona una representación visual de la forma en que el cliente interactúa con la marca en diferentes canales.

Todos los gráficos de identidad del cliente se administran y actualizan [!DNL Identity Service] en forma colectiva en tiempo real, en respuesta a la actividad del cliente.

[!DNL Identity Service] administra un gráfico de identidad visible únicamente por su organización y creado en función de sus datos, denominado gráfico privado. [!DNL Identity Service] aumenta el gráfico privado cuando un registro de datos ingerido contiene más de una identidad, agregando una relación entre las identidades encontradas.

Como ejemplo de los posibles tipos de factores a tener en cuenta al suministrar y etiquetar datos de identidad, el uso de números de teléfono como &quot;teléfono de trabajo&quot; puede resultar en más relaciones de las que se pretenden en el gráfico de identidad. Es posible que muchos empleados se refieran al mismo número de empleados para trabajar, y que &quot;casa&quot; y &quot;móvil&quot; sirvan mejor para mantener las relaciones lo más precisas posible.

## Suministro de datos de identidad a [!DNL Identity Service]

En esta sección se explica cómo se procesan los datos proporcionados a Adobe Experience Platform antes de utilizarlos [!DNL Identity Service] para crear un gráfico de identidad para cada cliente.

### Decidir sobre campos de identidad

Según la estrategia de recopilación de datos de su empresa, los campos de datos que etiquete como identidades determinan qué datos se incluyen en el mapa de identidad. Para obtener el máximo beneficio del Adobe Experience Platform y las identidades de cliente más completas posibles, debe cargar datos en línea y sin conexión.

- Los datos en línea son datos que describen la presencia y el comportamiento en línea, como nombres de usuario y direcciones de correo electrónico.

- Los datos sin conexión se refieren a datos que no están directamente relacionados con la presencia en línea, como los ID de sistemas CRM. Este tipo de datos hace que sus identidades sean más sólidas y admite la cohesión de los datos en los distintos sistemas.

### Crear Áreas de nombres de identidad adicionales

Aunque [!DNL Experience Platform] oferta una variedad de Áreas de nombres estándar, es posible que necesite crear Áreas de nombres adicionales para categorizar correctamente sus identidades. Para obtener más información, consulte la sección sobre [visualización y creación de Áreas de nombres para su organización](./namespaces.md) en la descripción general de la Área de nombres de identidad.

>[!NOTE] Las Áreas de nombres de identidad son un calificador para las identidades. Como resultado, una vez creada una Área de nombres, no se puede eliminar.

### Incluir datos de identidad en [!DNL Experience Data Model] (XDM)

Como marco estandarizado por el cual [!DNL Platform] organiza los datos de los clientes, [!DNL Experience Data Model] (XDM) permite compartir y entender los datos entre [!DNL Experience Platform] y otros servicios que interactúan con [!DNL Platform]. Para obtener más información, consulte la descripción general [del sistema](../xdm/home.md)XDM.

Los esquemas de registro y serie temporal proporcionan los medios para incluir datos de identidad. A medida que se ingieren datos, el gráfico de identidad creará nuevas relaciones entre fragmentos de datos de diferentes Áreas de nombres si se descubre que comparten datos de identidad comunes.

### Marcado de campos XDM como identidad

Cualquier campo de tipo `string` en esquemas que implemente clases XDM de registros o series temporales puede etiquetarse como campo de identidad. Como resultado, todos los datos ingestados en ese campo se considerarán datos de identidad.

Los campos de identidad también permiten la vinculación de identidades si comparten datos PII comunes.
Por ejemplo, al etiquetar los campos de número de teléfono como campos de identidad, [!DNL Identity Service] se graban automáticamente las relaciones con los demás individuos que utilizan el mismo número de teléfono.

>[!NOTE] La Área de nombres de las identidades resultantes se proporciona en el momento en que se etiqueta el campo.

### Configurar un conjunto de datos para [!DNL Identity Service]

Durante el proceso de inserción de flujo continuo, extrae [!DNL Identity Service ]automáticamente los datos de identidad de los datos de registros y series temporales. Sin embargo, antes de poder ingerir datos, debe habilitarse para [!DNL Identity Service]. Consulte el tutorial sobre la [configuración de un conjunto de datos para el Perfil de clientes en tiempo real y el servicio de identidad mediante API](../profile/tutorials/dataset-configuration.md) para obtener más información.

### Ingresar datos a [!DNL Identity Service]

[!DNL Identity Service] consume datos compatibles con XDM enviados a [!DNL Experience Platform] por ingestión [](../ingestion/batch-ingestion/overview.md) por lotes o por [transmisiones](../ingestion/streaming-ingestion/overview.md).

## Administración de datos

Adobe Experience Platform se creó teniendo en cuenta la privacidad e incluye un marco de administración de datos para proteger los datos PII de sus clientes. Los datos de identidad bajo la Área de nombres &quot;correo electrónico&quot; o &quot;teléfono&quot; están cifrados de forma predeterminada, pero para garantizar que los datos confidenciales se cifran antes de que se mantengan, las etiquetas de uso de datos se pueden aplicar a los datos a medida que se ingieren o cuando llegan [!DNL Platform]. Para obtener más información, lea la información general [sobre el Gobierno](../data-governance/home.md)de datos.

## Pasos siguientes

Ahora que comprendes los conceptos clave de [!DNL Identity Service] y su papel dentro de [!DNL Experience Platform], puedes empezar a aprender a trabajar con tu gráfico de identidad usando el [!DNL Identity Service API](./api/getting-started.md).