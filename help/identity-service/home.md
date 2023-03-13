---
keywords: Experience Platform;inicio;temas populares;identidad;Identity;gráficos XDM;servicio de identidad;servicio de identidad
solution: Experience Platform
title: Resumen del servicio de identidad
description: El servicio de identidad de Adobe Experience Platform le ayuda a obtener una mejor vista de su cliente y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales impactantes en tiempo real.
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: ad9fb0bcc7bca55da432c72adc94d49e3c63ad6e
workflow-type: tm+mt
source-wordcount: '1839'
ht-degree: 0%

---

# Información general del [!DNL Identity Service]

Para ofrecer experiencias digitales relevantes, es necesario tener una comprensión completa de su cliente. Esto se hace más difícil cuando los datos del cliente se fragmentan en sistemas dispares, lo que provoca que cada cliente individual parezca tener varias &quot;identidades&quot;.

El servicio de identidad de Adobe Experience Platform le ofrece una vista completa de sus clientes y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales impactantes en tiempo real.

Con [!DNL Identity Service], puede:

- Asegúrese de que sus clientes reciban una experiencia coherente, personalizada y relevante mediante cada interacción.
- Combine varias identidades diferentes de fuentes dispares y cree una vista completa de sus clientes.
- Utilice un gráfico de identidad para asignar diferentes áreas de nombres de identidad, lo que le proporciona una representación visual de cómo sus clientes interactúan con su marca en diferentes canales.

## Primeros pasos

Antes de profundizar en los detalles de [!DNL Identity Service], aquí tiene un breve resumen de los términos clave:

| Término | Definición |
| --- | --- |
| Identidad | Una identidad son datos que son únicos para una entidad, normalmente una persona individual. Una identidad, como un ID de inicio de sesión, ECID o ID de fidelidad, también se denomina &quot;identidad conocida&quot;. |
| ECID | El ID de Experience Cloud (ECID) es un área de nombres de identidad compartida que se utiliza en las aplicaciones de Experience Platform y Adobe Experience Cloud. ECID proporciona una base para la identidad del cliente y se utiliza como ID principal para dispositivos y como nodo base para gráficos de identidad. Consulte la [Información general de ECID](./ecid.md) para obtener más información. |
| Área de nombres de identidad | Un área de nombres de identidad sirve para distinguir el contexto o el tipo de una identidad. Por ejemplo, una identidad distingue &quot;nombre&quot;<span>@email.com&quot; como dirección de correo electrónico o &quot;443522&quot; como ID numérico de CRM. Las áreas de nombres de identidad se utilizan para buscar identidades individuales y proporcionar el contexto para los valores de identidad. Esto le permite determinar que dos [!DNL Profile] fragmentos que contienen ID principales diferentes, pero que comparten el mismo valor para `email` área de nombres de identidad, son de hecho, el mismo individuo. Consulte la [información general del área de nombres de identidad](./namespaces.md) para obtener más información. |
| Gráfico de identidad | Un gráfico de identidad es un mapa de relaciones entre identidades diferentes, que le permite visualizar y comprender mejor qué identidades de clientes se vinculan entre sí y cómo. Consulte el tutorial sobre [uso del visualizador de gráficos de identidad](./ui/identity-graph-viewer.md) para obtener más información. |
| Información de identificación personal (PII) | PII es información que puede identificar directamente a un cliente, como una dirección de correo electrónico o un número de teléfono. Los valores PII suelen utilizarse para que coincidan. las identidades múltiples de un cliente en diferentes sistemas. |
| Identidades desconocidas o anónimas | Las identidades desconocidas o anónimas son indicadores que aíslan dispositivos sin identificar a la persona real que utiliza el dispositivo. Las identidades desconocidas y anónimas incluyen información como la dirección IP y el ID de cookie de un visitante. Aunque las identidades desconocidas y anónimas pueden proporcionar datos de comportamiento, están limitadas hasta que un cliente proporcione su PII. |

## ¿Qué es [!DNL Identity Service]?

Cada día, los clientes interactúan con su negocio y establecen una relación de crecimiento continuo con su marca. Un cliente típico puede estar activo en cualquier sistema de la infraestructura de datos de su organización, como los sistemas de comercio electrónico, lealtad y servicio de asistencia. Ese mismo cliente también puede interactuar de forma anónima en cualquier número de dispositivos. [!DNL Identity Service] le permite recopilar una imagen completa de su cliente, agregando datos relacionados que, de lo contrario, podrían aislarse en sistemas dispares.

Considere un ejemplo cotidiano de la relación de un consumidor con su marca:

- Mary tiene una cuenta en su sitio de comercio electrónico en la que ha completado algunos pedidos en el pasado. Normalmente utiliza su portátil personal para ir de compras, donde inicia sesión cada vez. Sin embargo, durante una de sus visitas utiliza su tablet para comprar sandalias, pero no realiza un pedido ni inicia sesión.
- En este punto, la actividad de Mary aparece como dos perfiles separados:
   - Su inicio de sesión en comercio electrónico
   - Su dispositivo tablet, tal vez identificado por el ID del dispositivo
- Más tarde, Mary reanuda su sesión en tablet y proporciona su dirección de correo electrónico mientras se suscribe a su boletín informativo. Al hacerlo, la ingesta de transmisión agrega una nueva identidad como datos de registro dentro de su perfil. Como resultado, [!DNL Identity Service] Ahora, relaciona la actividad de Mary con los dispositivos tablet con el historial de su cuenta de comercio electrónico.
- Al hacer clic en su tableta, el contenido dirigido podría reflejar todo el perfil e historial de Mary, en lugar de solo una tableta utilizada por un comprador desconocido.

![Vinculación de identidad en Platform](./images/identity-service-stitching.png)

Básicamente, [!DNL Identity Service] le permite recopilar una imagen completa de su cliente, agregando datos relacionados que, de lo contrario, podrían estar dispersos en sistemas dispares. Las relaciones de identidad que [!DNL Identity Service] define y mantiene son aprovechadas por el Perfil del cliente en tiempo real para crear una imagen completa de un cliente y sus interacciones con su marca. Para obtener más información, consulte la [Resumen del perfil del cliente en tiempo real](../profile/home.md).

### Casos de uso

Ejemplos de [!DNL Identity Service] Las implementaciones de incluyen:

- Una empresa de telecomunicaciones puede confiar en el valor &quot;número de teléfono&quot;, donde un número de teléfono haría referencia a la misma persona de interés en los conjuntos de datos sin conexión y en línea.
- Una empresa minorista puede utilizar &quot;direcciones de correo electrónico&quot; en conjuntos de datos sin conexión y ECID en conjuntos de datos en línea debido al alto porcentaje de visitantes anónimos.
- Un banco puede preferir el &quot;número de cuenta&quot; en conjuntos de datos sin conexión, como las transacciones de sucursales. Pueden depender del &quot;ID de inicio de sesión&quot; en los conjuntos de datos en línea, ya que la mayoría de los visitantes se autenticarían durante su visita.
- Sus clientes también pueden tener ID propietarios únicos, como GUID u otros identificadores únicos universales.

## Área de nombres de identidad {#identity-namespace}

>[!CONTEXTUALHELP]
>id="platform_identity_namespace"
>title="Áreas de nombres de identidad"
>abstract="Un área de nombres de identidad sirve para distinguir el contexto o el tipo de una identidad. Por ejemplo, una identidad distingue &quot;nombre&quot;<span>@email.com&quot; como dirección de correo electrónico o &quot;443522&quot; como ID numérico de CRM."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_identity_value"
>title="Valores de identidad"
>abstract="Un valor de identidad es un identificador que representa a un individuo, organización o recurso único. El contexto o tipo de identidad que representa el valor se define mediante un área de nombres de identidad correspondiente. Al hacer coincidir los datos de los registros en los fragmentos de perfil, el área de nombres y el valor de identidad deben coincidirAl hacer coincidir los datos de los registros en los fragmentos de perfil, el área de nombres y el valor de identidad deben coincidir."
>text="Learn more in documentation"

Si le pregunta a una persona &quot;¿Cuál es su ID?&quot; sin un contexto más amplio, les resultaría difícil dar una respuesta útil. Según la misma lógica, un valor de cadena que representa un valor de identidad, ya sea un ID generado por el sistema o una dirección de correo electrónico, solo se completa cuando se proporciona con un calificador que da el contexto del valor de cadena: el área de nombres de identidad.

Sus clientes pueden interactuar con su marca a través de una combinación de canales en línea y sin conexión, lo que resulta en el desafío de cómo reconciliar esas interacciones fragmentadas en una sola identidad de cliente.

Para comprender a los clientes en varios dispositivos y canales, comience por reconocerlos en cada canal. Platform logra esto mediante el uso de áreas de nombres de identidad. Un área de nombres de identidad es un identificador, como correo electrónico o teléfono, que se utiliza para proporcionar contexto adicional a las identidades de los clientes. Las áreas de nombres de identidad se utilizan para buscar o vincular identidades individuales y proporcionar contexto para valores de identidad. Consulte la [información general del área de nombres de identidad](./namespaces.md) para obtener más información.

## Gráficos de identidad

Un gráfico de identidad es un mapa de relaciones entre diferentes áreas de nombres de identidad, que le permite visualizar y comprender mejor qué identidades de clientes se vinculan entre sí y cómo. Consulte el tutorial sobre [uso del visualizador de gráficos de identidad](./ui/identity-graph-viewer.md) para obtener más información.

El siguiente vídeo tiene como objetivo ayudarle a comprender las identidades y los gráficos de identidad.

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

## Suministro de datos de identidad a [!DNL Identity Service]

Esta sección describe cómo se procesan los datos proporcionados a Adobe Experience Platform antes de que los utilice [!DNL Identity Service] para crear un gráfico de identidad para cada cliente.

### Decidir sobre los campos de identidad

Según la estrategia de recopilación de datos empresariales, los campos de datos que etiquete como identidades determinan qué datos se incluyen en el mapa de identidad. Para obtener el máximo beneficio de Adobe Experience Platform y las identidades de cliente más completas posibles, debe cargar datos en línea y sin conexión.

- Los datos en línea son datos que describen la presencia y el comportamiento en línea, como nombres de usuario y direcciones de correo electrónico.

- Los datos sin conexión hacen referencia a datos que no están directamente relacionados con la presencia en línea, como los ID de sistemas CRM. Este tipo de datos hace que sus identidades sean más sólidas y admite la cohesión de los datos en sus distintos sistemas.

### Crear áreas de nombres de identidad adicionales

Aunque Experience Platform ofrece una variedad de áreas de nombres estándar, es posible que necesite crear áreas de nombres adicionales para categorizar correctamente sus identidades. Para obtener más información, consulte la sección sobre [ver y crear áreas de nombres para su organización](./namespaces.md) en información general del área de nombres de identidad.

>[!NOTE]
>
>Las áreas de nombres de identidad son un calificador para identidades. Como resultado, una vez creada una Área de nombres, no se puede eliminar.

### Incluir datos de identidad en [!DNL Experience Data Model] (XDM)

Como el marco estandarizado mediante el cual [!DNL Platform] organiza los datos del cliente, [!DNL Experience Data Model] (XDM) permite compartir y comprender los datos entre Experience Platform y otros servicios que interactúan con [!DNL Platform]. Para obtener más información, consulte [Información general del sistema XDM](../xdm/home.md).

Tanto los esquemas de registros como los de series temporales proporcionan los medios para incluir los datos de identidad. A medida que se incorporan los datos, el gráfico de identidad creará nuevas relaciones entre fragmentos de datos de diferentes áreas de nombres si se encuentran para compartir datos de identidad comunes.

### Marcar campos XDM como identidad

Cualquier campo de tipo `string` en los esquemas que implementan las clases XDM de registro o de serie temporal se pueden etiquetar como un campo de identidad. Como resultado, todos los datos introducidos en ese campo se considerarían datos de identidad.

>[!NOTE]
>
>Los campos de tipo matriz y mapa no son compatibles y no se pueden marcar y etiquetar como campos de identidad.

Los campos de identidad también permiten la vinculación de identidades si comparten datos PII comunes.
Por ejemplo, al etiquetar los campos de número de teléfono como campos de identidad, [!DNL Identity Service] grafica automáticamente las relaciones con otras personas que usan el mismo número de teléfono.

>[!NOTE]
>
>El área de nombres de las identidades resultantes se proporciona en el momento en que se etiqueta el campo.

### Configurar un conjunto de datos para [!DNL Identity Service]

Durante el proceso de ingesta por streaming, [!DNL Identity Service ]extrae automáticamente los datos de identidad de los datos de registros y series temporales. Sin embargo, para poder ingerir los datos, debe estar habilitado para [!DNL Identity Service]. Consulte el tutorial sobre  [Configuración de un conjunto de datos para el perfil del cliente en tiempo real y el servicio de identidad mediante API](../profile/tutorials/dataset-configuration.md) para obtener más información.

### Ingesta de datos en [!DNL Identity Service]

[!DNL Identity Service] consume datos compatibles con XDM enviados al Experience Platform por [ingesta por lotes](../ingestion/batch-ingestion/overview.md) o [ingesta por streaming](../ingestion/streaming-ingestion/overview.md).

El siguiente vídeo tiene como objetivo ayudarle a comprender el servicio de identidad. Este vídeo muestra cómo etiquetar campos de datos como identidades, ingerir datos de identidad y luego verificar que los datos hayan llegado al gráfico privado del servicio de identidad de Adobe Experience Platform.

>[!WARNING]
>
>El [!DNL Platform] La interfaz de usuario que se muestra en el siguiente vídeo no está actualizada. Consulte la documentación para obtener las capturas de pantalla y la funcionalidad más recientes de la interfaz de usuario.

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## Gobernanza de datos

Adobe Experience Platform se ha creado teniendo en cuenta la privacidad e incluye un marco de trabajo de control de datos para proteger los datos PII de sus clientes. Los datos de identidad del área de nombres &quot;correo electrónico&quot; o &quot;teléfono&quot; se cifran de forma predeterminada, pero para garantizar que los datos confidenciales se cifren antes de que persistan, se pueden aplicar etiquetas de uso de datos a los datos a medida que se incorporan o una vez que llegan a [!DNL Platform]. Para obtener más información, lea la [Resumen de gobernanza de datos](../data-governance/home.md).

## Pasos siguientes

Ahora que comprende los conceptos clave de [!DNL Identity Service] y su función dentro del Experience Platform, puede empezar a aprender a trabajar con el gráfico de identidades mediante [[!DNL Identity Service API]](./api/getting-started.md).
