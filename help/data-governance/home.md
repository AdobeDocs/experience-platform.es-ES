---
keywords: Experience Platform;inicio;temas populares;DULE;dule
solution: Experience Platform
title: Información general sobre gobernanza de datos
description: Administración de datos de Adobe Experience Platform le permite administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos. Desempeña un papel clave dentro de Experience Platform en varios niveles, incluida la catalogación, el linaje de datos, el etiquetado del uso de los datos, las políticas de uso de los datos y el control del uso de los datos para las acciones de marketing.
exl-id: 00ca6bc2-1c58-4ea2-8bb5-30fd3fa5944a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1624'
ht-degree: 9%

---

# Información general de gobernanza de datos {#data-governance-overview}

>[!CONTEXTUALHELP]
>id="platform_datagovernance_framework"
>title="Obligación de gobernanza de datos"
>abstract="Recuerde: la responsabilidad de adherirse a las políticas de gobernanza de datos de su organización y de cumplir con sus requisitos regulatorios es exclusivamente suya. Experience Platform proporciona herramientas de gobernanza de datos para que administre sus obligaciones con respecto al uso de los datos. Aplique las etiquetas de uso de datos adecuadas antes de consultar o procesar datos. Consulte la documentación para obtener más información sobre las herramientas y las prácticas recomendadas para la gobernanza de datos."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=es" text="Información general de gobernanza de datos"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=es" text="Información general sobre etiquetas de gobernanza de datos"

Una de las funciones principales de Adobe Experience Platform es reunir datos de varios sistemas empresariales para permitir que los especialistas en marketing identifiquen, comprendan y capturen clientes. Estos datos pueden estar sujetos a restricciones de uso definidas por su organización o por la normativa legal. Por lo tanto, es importante asegurarse de que las operaciones de datos dentro de [!DNL Experience Platform] cumplen con las directivas de uso de datos.

Administre los datos de los clientes y garantice el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos con el control de datos de Adobe Experience Platform. La gobernanza de datos desempeña un papel clave dentro de Experience Platform en varios niveles, incluida la catalogación, el linaje de datos, el etiquetado del uso de datos, las políticas de uso de datos y el control del uso de datos para acciones de marketing.

>[!NOTE]
>
>En Experience Platform, el control de datos solo afecta a cómo se utilizan o activan los datos, independientemente de si el usuario realiza la acción. Para obtener información sobre cómo controlar el acceso a campos de datos específicos para determinados usuarios de Experience Platform de su organización, consulte la documentación sobre [control de acceso basado en atributos](../access-control/abac/overview.md).

## Funciones de gobernanza de datos {#data-governance-roles}

Como concepto, la gobernanza de datos no es automática ni se produce en el vacío. Lo que comenzó como un rol para un individuo, generalmente reconocido como administrador de datos, ha crecido considerablemente a medida que el ecosistema de gobernanza de datos se ha expandido. En la actualidad, la gobernanza de datos requiere una administración y una monitorización continuas para tener éxito. La gobernanza eficaz de los datos depende de que los administradores de datos tengan herramientas con las que se puedan etiquetar correctamente los datos, se puedan crear políticas de uso y se pueda aplicar el cumplimiento de esas políticas.

Aunque la gobernanza de datos debe ser responsabilidad de cada individuo en la organización, estas son algunas de las funciones esenciales dentro del ciclo de gobernanza de datos:

![Gráfico para transmitir las cuatro funciones de control de datos, con comillas sobre las obligaciones de cada función.](./images/overview/roles.png)

### Administrador de datos {#data-steward}

Los administradores de datos son el corazón de la gobernanza de datos. Esta función es responsable de interpretar las regulaciones, las restricciones contractuales y las políticas, y de aplicarlas directamente a los datos. Basándose en su comprensión de estas regulaciones, restricciones y políticas, la función de administrador de datos incluye:

* Revisar datos, conjuntos de datos y ejemplos de datos para aplicar y administrar el etiquetado de uso de metadatos.
* Crear directivas de datos y aplicarlas a conjuntos de datos y campos.
* Comunicar directivas de datos a la organización.

### Experto en marketing {#marketer}

Los especialistas en marketing son el punto final de la gobernanza de datos. Solicitan datos de la infraestructura de control de datos creada por administradores de datos, científicos e ingenieros. Los especialistas en marketing abarcan una serie de especialidades diferentes bajo el paraguas del marketing, entre las que se incluyen las siguientes:

* Los analistas de marketing solicitan datos para permitir comprender a los clientes, tanto como individuos como en grupos (también conocidos como segmentos).
* Los especialistas en marketing y los diseñadores de experiencias utilizan datos de para diseñar nuevas experiencias para los clientes.

## Marco de gobernanza de datos {#data-governance-framework}

El marco de trabajo de control de datos simplifica y optimiza el proceso de categorizar los datos y crear políticas de uso de datos. Una vez aplicadas las etiquetas de datos y establecidas las políticas de uso de datos, se pueden evaluar las acciones de marketing para garantizar el uso correcto de los datos.

El marco de trabajo de gobernanza de datos consta de tres elementos clave: etiquetas, políticas y aplicación.

1. **Etiquetas:** Clasifique datos que reflejen consideraciones relacionadas con la privacidad y condiciones contractuales para cumplir con las regulaciones y políticas de la organización.
1. **Directivas:** Describa qué tipos de acciones de marketing se permiten o no se permiten realizar en datos específicos.
1. **Aplicación:** Utiliza el marco de directivas para aconsejar y aplicar directivas en diferentes patrones de acceso a datos.

## Etiquetas de uso de datos {#data-usage-labels}

El control de datos permite a los administradores de datos aplicar etiquetas de uso en el nivel de campo de esquema para categorizar los datos según el tipo de políticas que se apliquen.

El marco de trabajo de control de datos incluye etiquetas de uso de datos predefinidas que se pueden utilizar para categorizar los datos de tres maneras:

![Las tres categorías de etiquetas de uso de datos.](./images/overview/label-categories.png)

* **Etiquetas de datos del contrato &quot;C&quot;:** Etiquete y categorice los datos que tienen obligaciones contractuales o están relacionados con las directivas de control de datos de clientes.
* **Etiquetas de datos de identidad &quot;I&quot;:** Etiquete y categorice los datos que pueden identificar a una persona específica o ponerse en contacto con ella.
* **Etiquetas de datos confidenciales de tipo &quot;S&quot;:** Etiquete y categorice los datos relacionados con datos confidenciales, como datos geográficos.

>[!NOTE]
>
>Consulte la guía de [etiquetas de uso de datos compatibles](labels/reference.md) para obtener una lista completa de las etiquetas disponibles y las definiciones de cada tipo de etiqueta.

Las etiquetas se pueden aplicar en cualquier momento, lo que proporciona flexibilidad en la forma en que se decide administrar los datos. Una práctica recomendada recomienda etiquetar los datos cuando se incorporan en Experience Platform o en cuanto los datos están disponibles en [!DNL Experience Platform].

Consulte la descripción general de [etiquetas de uso de datos](./labels/overview.md) para obtener más información sobre cómo se utilizan las etiquetas de uso de datos para ayudar a aplicar el cumplimiento de la gobernanza de datos.

## Políticas de uso de datos {#data-usage-policies}

Para que las etiquetas de uso de datos respalden con eficacia el cumplimiento, se deben implementar políticas de uso de datos. Las políticas de uso de datos son reglas que describen los tipos de acciones de marketing que se le permite realizar, o que se le restringe, en los datos de Experience Platform.

Un ejemplo de acción de marketing puede ser el deseo de exportar un conjunto de datos a un servicio de terceros. Si existe una política que declare que la información de identificación personal (PII) no se puede exportar y se ha aplicado una etiqueta &quot;I&quot; (datos de identidad) al nivel de campo desde su esquema. A continuación, el Servicio de directivas evita cualquier acción que pueda exportar este conjunto de datos a un destino de terceros. Si se produce uno de estos intentos de acción, el Servicio de directivas envía un mensaje para informarle de que se ha infringido una directiva de uso de datos.


Hay dos tipos de directivas disponibles:

* **[!UICONTROL Política de control de datos]**: Restrinja la activación de datos en función de la acción de marketing que se esté realizando y de las etiquetas de uso de datos que lleven los datos en cuestión.
* **[!UICONTROL Política de consentimiento]**: filtre los perfiles que se pueden activar a [destinos](../destinations/home.md) según las preferencias o el consentimiento de sus clientes.

Una vez aplicadas las etiquetas de uso de datos, los administradores de datos pueden crear directivas mediante la API del servicio de directivas o la interfaz de usuario de Experience Platform. Para obtener más información sobre las políticas de uso de datos y las acciones de marketing, consulte la [descripción general de las políticas](./policies/overview.md).

>[!IMPORTANT]
>
>Todas las políticas de uso de datos (incluidas las políticas principales proporcionadas por Adobe) están desactivadas de forma predeterminada. Para que una directiva individual se tenga en cuenta para la aplicación, debe habilitar manualmente esa directiva.

## Pasos siguientes

Este documento proporciona una introducción de alto nivel a la gobernanza de datos y al marco de trabajo de gobernanza de datos. Ahora puede continuar con la [guía del usuario sobre etiquetas de uso de datos](labels/user-guide.md) y empezar a agregar etiquetas de uso a sus datos de experiencia.

## Apéndice

La siguiente sección proporciona información adicional sobre la gobernanza de datos.

### Terminología de control de datos {#data-governance-terminology}

En la tabla siguiente se describen los términos clave relacionados con la gobernanza de datos y el marco de trabajo de gobernanza de datos.

| Término | Definición |
|---|---|
| **Etiquetas de contrato** | Las etiquetas del contrato &quot;C&quot; se utilizan para categorizar los datos que tienen obligaciones contractuales o están relacionados con las políticas de gobernanza de datos de su organización. |
| **Datos entre sitios** | Los datos entre sitios son la combinación de datos de varios sitios. Los datos entre sitios incluyen datos tanto in situ como externos, o una combinación de datos de varias fuentes externas. |
| **Gobernanza de datos** | La gobernanza de datos abarca las estrategias y tecnologías utilizadas para garantizar que los datos cumplan con las regulaciones y las políticas corporativas con respecto al uso de datos. |
| **Administrador de datos** | El administrador de datos es la persona responsable de la administración, la supervisión y la aplicación de los recursos de datos de una organización. Un administrador de datos también garantiza que las políticas de gobernanza de datos se salvaguarden y mantengan para cumplir con las regulaciones gubernamentales y las políticas de la organización. |
| **Etiquetas de uso de datos** | Las etiquetas de uso de datos permiten a los usuarios categorizar los datos que reflejan consideraciones relacionadas con la privacidad y condiciones contractuales para cumplir con las normativas y las políticas corporativas. |
| **Etiquetas de conjuntos de datos** | Las etiquetas se pueden añadir a un esquema. Todos los campos de un conjunto de datos heredan las etiquetas del esquema. |
| **Etiquetas de campo** | Las etiquetas de campo son etiquetas de control de datos que se heredan de un esquema o se aplican directamente a un campo. Las etiquetas de gobernanza de datos aplicadas a un campo no se heredan hasta el nivel de esquema. |
| **Geoperímetro** | Una geovalla es un límite geográfico virtual, definido por la tecnología GPS o RFID, que permite al software almacenar en déclencheur una respuesta cuando un dispositivo móvil entra o sale de una zona en particular. |
| **Etiquetas de identidad** | Las etiquetas de identidad “I” se utilizan para categorizar datos que pueden identificar o usarse para contactar a una persona específica. |
| **Direccionamiento basado en intereses** | La segmentación basada en intereses, también conocida como personalización, se produce si se cumplen las tres condiciones siguientes:<br>Los datos recopilados en el sitio son,<br><ul><li>Se utiliza para hacer deducciones sobre los intereses de un usuario,</li><li>Se utiliza en otro contexto, como en otro sitio o aplicación (fuera del sitio)</li><li>Se utiliza para seleccionar qué contenido o anuncios se muestran en función de esas deducciones.</li></ul> |
| **Acción de marketing** | Una acción de marketing, en el contexto del marco de trabajo de control de datos, es una acción que realiza un consumidor de datos de Experience Platform, para la que es necesario comprobar si se han infringido las políticas de uso de datos |
| **Directiva** | En el marco de trabajo de gobernanza de datos, una política es una regla que describe qué tipos de acciones de marketing se permiten o no en datos específicos. |
| **Etiquetas de esquema** | Administre las etiquetas para la gobernanza de datos, el consentimiento y el control de acceso en el nivel de esquema. Esto propaga las etiquetas a cada conjunto de datos que utiliza ese esquema. |
| **Etiquetas confidenciales** | Las etiquetas confidenciales &quot;S&quot; se utilizan para categorizar los datos que usted y su organización consideran confidenciales. |

## Recursos adicionales

El siguiente vídeo tiene como objetivo ayudarle a comprender el marco de trabajo de control de datos.

>[!VIDEO](https://video.tv.adobe.com/v/32682?quality=12&enable10seconds=on&speedcontrol=on&captions=spa)

En el siguiente vídeo se explica cómo aplicar etiquetas de uso de datos a los esquemas o a la totalidad de un conjunto de datos en Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/3422794/?learn=on&captions=spa)
