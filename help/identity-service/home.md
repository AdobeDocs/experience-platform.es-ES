---
keywords: Experience Platform;inicio;temas populares;identidad;identidad;gráficos XDM;servicio de identidad;servicio de identidad
solution: Experience Platform
title: Información general del servicio de identidad
description: El servicio de identidad de Adobe Experience Platform le ayuda a obtener una mejor visión de su cliente y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales y impactantes en tiempo real.
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: ad9fb0bcc7bca55da432c72adc94d49e3c63ad6e
workflow-type: tm+mt
source-wordcount: '1839'
ht-degree: 0%

---

# Información general del [!DNL Identity Service]

La entrega de experiencias digitales relevantes requiere una comprensión completa de su cliente. Esto se hace más difícil cuando los datos de sus clientes están fragmentados en distintos sistemas, lo que hace que cada cliente individual parezca tener múltiples &quot;identidades&quot;.

El servicio de identidad de Adobe Experience Platform le ofrece una vista completa de sus clientes y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales e impactantes en tiempo real.

con [!DNL Identity Service], puede:

- Asegúrese de que sus clientes reciban una experiencia coherente, personalizada y relevante a través de cada interacción.
- Reúna varias identidades diferentes de fuentes diferentes y cree una vista completa de sus clientes.
- Utilice un gráfico de identidad para asignar diferentes áreas de nombres de identidad, proporcionando así una representación visual de cómo los clientes interactúan con la marca en los distintos canales.

## Primeros pasos

Antes de sumergirse en los detalles de [!DNL Identity Service], aquí tiene un breve resumen de los términos clave:

| Término | Definición |
| --- | --- |
| Identidad | Una identidad es datos que son exclusivos de una entidad, normalmente de una persona individual. Una identidad, como un ID de inicio de sesión, un ECID o un ID de lealtad, también se denomina &quot;identidad conocida&quot;. |
| ECID | El ID de Experience Cloud (ECID) es un área de nombres de identidad compartida que se utiliza en las aplicaciones de Experience Platform y Adobe Experience Cloud. ECID proporciona una base para la identidad del cliente y se utiliza como ID principal para dispositivos y como nodo base para gráficos de identidad. Consulte la [Información general de ECID](./ecid.md) para obtener más información. |
| Área de nombres de identidad | Un área de nombres de identidad sirve para distinguir el contexto o el tipo de una identidad. Por ejemplo, una identidad distingue &quot;name&quot;<span>@email.com&quot; como dirección de correo electrónico o &quot;443522&quot; como ID de CRM numérico. Las áreas de nombres de identidad se utilizan para buscar identidades individuales y proporcionar el contexto para los valores de identidad. Esto le permite determinar que dos [!DNL Profile] fragmentos que contienen ID principales diferentes, pero que comparten el mismo valor para `email` área de nombres de identidad, de hecho, son la misma persona. Consulte la [información general del área de nombres de identidad](./namespaces.md) para obtener más información. |
| Gráfico de identidad | Un gráfico de identidad es un mapa de relaciones entre distintas identidades, que le permite visualizar y comprender mejor qué identidades de cliente se vinculan entre sí y cómo. Consulte el tutorial en [uso del visor de gráficos de identidad](./ui/identity-graph-viewer.md) para obtener más información. |
| Información de identificación personal (PII) | PII es información que puede identificar directamente a un cliente, como una dirección de correo electrónico o un número de teléfono. Los valores PII suelen utilizarse para hacer coincidir. múltiples identidades de un cliente en diferentes sistemas. |
| Identidades desconocidas o anónimas | Las identidades desconocidas o anónimas son indicadores que aíslan los dispositivos sin identificar a la persona real que utiliza el dispositivo. Las identidades desconocidas y anónimas incluyen información como la dirección IP y el ID de cookie de un visitante. Aunque las identidades anónimas y desconocidas pueden proporcionar datos de comportamiento, están limitadas hasta que un cliente proporcione su PII. |

## ¿Qué es [!DNL Identity Service]?

Cada día, los clientes interactúan con su empresa y establecen una relación cada vez más estrecha con su marca. Un cliente típico puede estar activo en cualquier cantidad de sistemas dentro de la infraestructura de datos de su organización, como su sistema de comercio electrónico, lealtad y asistencia técnica. Ese mismo cliente también puede participar de forma anónima en cualquier número de dispositivos. [!DNL Identity Service] le permite crear una imagen completa de su cliente, agregando datos relacionados que, de lo contrario, se podrían ocultar en distintos sistemas.

Veamos un ejemplo cotidiano de la relación de un consumidor con su marca:

- Mary tiene una cuenta en su sitio de comercio electrónico donde ha completado algunos pedidos en el pasado. Ella suele usar su laptop personal para comprar, donde inicia sesión cada vez. Sin embargo, durante una de sus visitas usa su tableta para comprar sandalias, pero no realiza un pedido y no inicia sesión.
- En este punto, la actividad de Mary aparece como dos perfiles separados:
   - Su inicio de sesión en comercio electrónico
   - Su dispositivo tableta, tal vez identificado por el ID del dispositivo
- Más tarde, Mary reanuda su sesión en la tableta y proporciona su dirección de correo electrónico cuando se suscribe a la newsletter. Al hacerlo, la transmisión por secuencias de ingesta agrega una nueva identidad como datos de registro dentro de su perfil. Como resultado, [!DNL Identity Service] ahora relaciona la actividad del dispositivo tableta de Mary con su historial de cuenta de comercio electrónico.
- Al hacer clic en su tableta, el contenido objetivo podría reflejar el perfil completo y la historia de Mary, en lugar de una tableta usada por un comprador desconocido.

![Vinculación de identidad en la plataforma](./images/identity-service-stitching.png)

Esencialmente, [!DNL Identity Service] le permite crear una imagen completa de su cliente, agregando datos relacionados que, de lo contrario, podrían estar dispersos en distintos sistemas. Las relaciones de identidad que [!DNL Identity Service] el perfil del cliente en tiempo real aprovecha las definiciones y los mantiene para crear una imagen completa de un cliente y sus interacciones con su marca. Para obtener más información, consulte la [Resumen del perfil del cliente en tiempo real](../profile/home.md).

### Casos de uso

Ejemplos de [!DNL Identity Service] las implementaciones incluyen:

- Una empresa de telecomunicaciones puede confiar en el valor &quot;número de teléfono&quot;, en el que un número de teléfono hace referencia a la misma persona de interés tanto en los conjuntos de datos en línea como sin conexión.
- Una empresa minorista puede utilizar &quot;dirección de correo electrónico&quot; en conjuntos de datos sin conexión y ECID en conjuntos de datos en línea, debido al alto porcentaje de visitantes anónimos.
- Un banco puede preferir el &quot;número de cuenta&quot; en conjuntos de datos sin conexión, como las transacciones de sucursales. Pueden depender del &quot;ID de inicio de sesión&quot; en los conjuntos de datos en línea, ya que la mayoría de los visitantes se autenticarían durante su visita.
- Los clientes también pueden tener ID propietarios únicos, como GUID u otros identificadores únicos universales.

## Área de nombres de identidad {#identity-namespace}

>[!CONTEXTUALHELP]
>id="platform_identity_namespace"
>title="Espacios de nombres de identidad"
>abstract="Un área de nombres de identidad sirve para distinguir el contexto o el tipo de una identidad. Por ejemplo, una identidad distingue &quot;name&quot;<span>@email.com&quot; como dirección de correo electrónico o &quot;443522&quot; como ID de CRM numérico."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_identity_value"
>title="Valores de identidad"
>abstract="Un valor de identidad es un identificador que representa a un individuo, organización o recurso únicos. El contexto o tipo de identidad que representa el valor se define mediante un área de nombres de identidad correspondiente. Al hacer coincidir los datos de registro en los fragmentos de perfil, el área de nombres y el valor de identidad deben coincidir. Al hacer coincidir los datos de registro en los fragmentos de perfil, el área de nombres y el valor de identidad deben coincidir."
>text="Learn more in documentation"

Si le preguntaste a una persona &quot;¿Cuál es tu ID?&quot; sin más contexto, les resultaría difícil dar una respuesta útil. Con la misma lógica, un valor de cadena que representa un valor de identidad, ya sea un ID generado por el sistema o una dirección de correo electrónico, solo se completa cuando se proporciona con un calificador que proporciona el contexto del valor de cadena: el área de nombres de identidad.

Los clientes pueden interactuar con su marca mediante una combinación de canales en línea y sin conexión, lo que resulta en el desafío de cómo reconciliar esas interacciones fragmentadas en una sola identidad de cliente.

Comprender al cliente en varios dispositivos y canales comienza reconociéndolos en cada canal. Platform logra esto utilizando áreas de nombres de identidad. Un área de nombres de identidad es un identificador como Correo electrónico o Teléfono, que se utiliza para proporcionar contexto adicional a las identidades de los clientes. Las áreas de nombres de identidad se utilizan para buscar o vincular identidades individuales y proporcionar contexto para los valores de identidad. Consulte la [información general del área de nombres de identidad](./namespaces.md) para obtener más información.

## Gráficos de identidad

Un gráfico de identidad es un mapa de relaciones entre diferentes áreas de nombres de identidad, que le permite visualizar y comprender mejor qué identidades de cliente se vinculan entre sí y cómo. Consulte el tutorial en [uso del visor de gráficos de identidad](./ui/identity-graph-viewer.md) para obtener más información.

El siguiente vídeo está diseñado para ayudar a comprender las identidades y los gráficos de identidad.

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

## Proporcionar datos de identidad a [!DNL Identity Service]

En esta sección se explica cómo se procesan los datos proporcionados a Adobe Experience Platform antes de que los utilice [!DNL Identity Service] para crear un gráfico de identidad para cada cliente.

### Decidir sobre campos de identidad

Según la estrategia de recopilación de datos empresariales, los campos de datos que etiquete como identidades determinan qué datos se incluyen en el mapa de identidad. Para obtener el máximo beneficio de Adobe Experience Platform y las identidades de cliente más completas posibles, debe cargar datos en línea y sin conexión.

- Los datos en línea son datos que describen la presencia y el comportamiento en línea, como nombres de usuario y direcciones de correo electrónico.

- Los datos sin conexión se refieren a datos que no están directamente relacionados con la presencia en línea, como los ID de sistemas CRM. Este tipo de datos hace que sus identidades sean más sólidas y admite la cohesión de datos en todos sus sistemas dispares.

### Crear áreas de nombres de identidad adicionales

Aunque el Experience Platform ofrece una variedad de áreas de nombres estándar, es posible que tenga que crear áreas de nombres adicionales para categorizar correctamente las identidades. Para obtener más información, consulte la sección sobre [visualización y creación de áreas de nombres para su organización](./namespaces.md) en la descripción general del área de nombres de identidad.

>[!NOTE]
>
>Las áreas de nombres de identidad son un calificador para las identidades. Como resultado, una vez creado un espacio de nombres, no se puede eliminar.

### Incluir datos de identidad en [!DNL Experience Data Model] (XDM)

Como marco normalizado por el cual [!DNL Platform] organiza los datos de los clientes, [!DNL Experience Data Model] (XDM) permite compartir y comprender los datos entre el Experience Platform y otros servicios que interactúan con [!DNL Platform]. Para obtener más información, consulte [Información general del sistema XDM](../xdm/home.md).

Los esquemas de registros y series temporales proporcionan los medios para incluir datos de identidad. A medida que se incorporan los datos, el gráfico de identidad creará nuevas relaciones entre los fragmentos de datos de diferentes áreas de nombres si se encuentran que comparten datos de identidad comunes.

### Marcado de campos XDM como identidad

Cualquier campo de tipo `string` en esquemas que implementan clases XDM de registros o series temporales, se pueden etiquetar como campos de identidad. Como resultado, todos los datos introducidos en ese campo se considerarán datos de identidad.

>[!NOTE]
>
>Los campos de tipo matriz y asignación no son compatibles y no se pueden marcar ni etiquetar como campos de identidad.

Los campos de identidad también permiten la vinculación de identidades si comparten datos PII comunes.
Por ejemplo, etiquetando los campos de número de teléfono como campos de identidad, [!DNL Identity Service] grafica automáticamente las relaciones con otras personas que se ha descubierto que utilizan el mismo número de teléfono.

>[!NOTE]
>
>El área de nombres de las identidades resultantes se proporciona en el momento en que se etiqueta el campo.

### Configurar un conjunto de datos para [!DNL Identity Service]

Durante el proceso de ingesta de flujo continuo, [!DNL Identity Service ]extrae automáticamente los datos de identidad de los datos de registros y series temporales. Sin embargo, antes de poder introducir los datos, estos deben habilitarse para [!DNL Identity Service]. Consulte el tutorial en  [configuración de un conjunto de datos para perfil de cliente en tiempo real y servicio de identidad mediante API](../profile/tutorials/dataset-configuration.md) para obtener más información.

### Ingesta de datos a [!DNL Identity Service]

[!DNL Identity Service] consume datos compatibles con XDM enviados al Experience Platform por [ingesta por lotes](../ingestion/batch-ingestion/overview.md) o [ingesta de transmisión](../ingestion/streaming-ingestion/overview.md).

El siguiente vídeo está diseñado para admitir su comprensión del servicio de identidad. Este vídeo muestra cómo etiquetar campos de datos como identidades, ingerir datos de identidad y luego verificar que los datos hayan llegado al gráfico privado del servicio de identidad de Adobe Experience Platform.

>[!WARNING]
>
>La variable [!DNL Platform] La interfaz de usuario que se muestra en el siguiente vídeo no está actualizada. Consulte la documentación para obtener las últimas capturas de pantalla y funciones de la interfaz de usuario.

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## Administración de datos

Adobe Experience Platform se creó teniendo en cuenta la privacidad e incluye un marco de control de datos para proteger los datos PII de sus clientes. Los datos de identidad en el espacio de nombres &quot;correo electrónico&quot; o &quot;teléfono&quot; se cifran de forma predeterminada, pero para garantizar que los datos confidenciales se cifran antes de que persistan, las etiquetas de uso de datos se pueden aplicar a los datos a medida que se incorporan o una vez que llegan [!DNL Platform]. Para obtener más información, lea la [Información general sobre la administración de datos](../data-governance/home.md).

## Pasos siguientes

Ahora que comprende los conceptos clave de [!DNL Identity Service] y su función dentro de Experience Platform, puede empezar a aprender a trabajar con el gráfico de identidad mediante el [[!DNL Identity Service API]](./api/getting-started.md).
