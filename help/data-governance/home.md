---
keywords: Experience Platform;inicio;temas populares;DULE;programación
solution: Experience Platform
title: Información general sobre la administración de datos
description: La administración de datos de Adobe Experience Platform le permite administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos. Desempeña un papel clave dentro del Experience Platform en varios niveles, incluida la catalogación, el linaje de datos, el etiquetado del uso de los datos, las políticas de uso de los datos y el control del uso de los datos para las acciones de marketing
exl-id: 00ca6bc2-1c58-4ea2-8bb5-30fd3fa5944a
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1479'
ht-degree: 2%

---

# Información general sobre la administración de datos

Una de las funciones principales de Adobe Experience Platform es unir los datos de varios sistemas empresariales para permitir a los especialistas en marketing identificar, comprender y captar mejor a los clientes. Estos datos pueden estar sujetos a restricciones de uso definidas por su organización o por las regulaciones legales. Por lo tanto, es importante garantizar que los datos funcionen dentro de [!DNL Platform] cumplen las directivas de uso de datos.

La administración de datos de Adobe Experience Platform le permite administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos. Desempeña un papel clave en [!DNL Experience Platform] en varios niveles, incluida la catalogación, el linaje de datos, el etiquetado del uso de datos, las políticas de uso de datos y el control del uso de datos para las acciones de marketing.

>[!NOTE]
>
>En Experience Platform, el control de datos solo se refiere al modo en que se utilizan o activan los datos, independientemente de si el usuario realiza la acción. Para obtener información sobre cómo controlar el acceso a campos de datos específicos para determinados usuarios de Platform dentro de su organización, consulte la documentación de [control de acceso basado en atributos](../access-control/abac/overview.md) en su lugar.

## Funciones de administración de datos

Como concepto, el control de datos no es automático ni se produce en un vacío. Lo que comenzó como un papel para un individuo, generalmente reconocido como gestor de datos, ha crecido considerablemente a medida que se ha ampliado el ecosistema de control de datos. En la actualidad, el control de los datos requiere una gestión y supervisión continuas para tener éxito y depende de que los administradores de datos dispongan de herramientas con las que se puedan etiquetar correctamente los datos, se puedan crear políticas de uso y se pueda hacer cumplir esas políticas.

Si bien la gestión de los datos debe ser responsabilidad de cada individuo en la organización, a continuación se presentan algunas de las funciones esenciales dentro del ciclo de gobernanza de los datos:

![Funciones de administración de datos](./images/overview/roles.png)

### Administrador de datos

Los administradores de datos son el núcleo del control de datos. Esta función es responsable de interpretar regulaciones, restricciones contractuales y políticas, y aplicarlas directamente a los datos. Basándose en su comprensión de estas regulaciones, restricciones y políticas, el rol de un gestor de datos incluye:

* Revisión de datos, conjuntos de datos y muestras de datos para aplicar y administrar el etiquetado de uso de metadatos.
* Creación de políticas de datos y aplicación a conjuntos de datos y campos.
* Comunicar las políticas de datos a la organización.

### Experto en marketing

Los especialistas en marketing son el punto final del control de datos. Solicitan datos de la infraestructura de control de datos creada por administradores de datos, científicos e ingenieros. Los especialistas en marketing proponen una serie de especialidades diferentes en el marco del marketing, entre las que se incluyen las siguientes:

* Los analistas de marketing solicitan datos para comprender mejor a los clientes, tanto como individuos como en grupos (también conocidos como segmentos).
* Los especialistas en marketing y los diseñadores de experiencias utilizan los datos para diseñar nuevas experiencias para los clientes.


## Marco de gobernanza de datos

El marco de control de datos simplifica y optimiza el proceso de categorización de datos y creación de políticas de uso de datos. Una vez aplicadas las etiquetas de datos y establecidas las políticas de uso de datos, se pueden evaluar las acciones de marketing para garantizar el uso correcto de los datos.

El marco de control de datos tiene tres elementos clave: Etiquetas, políticas y aplicación.

1. **Etiquetas:** Clasifique los datos que reflejen consideraciones relacionadas con la privacidad y condiciones contractuales para cumplir con las regulaciones y políticas de organización.
1. **Políticas:** Describa qué tipo(s) de acciones de marketing se permiten o no se permite realizar en datos específicos.
1. **Aplicación:** Utiliza el marco de políticas para aconsejar y aplicar políticas en diferentes patrones de acceso a los datos.

## Etiquetas de uso de datos

La administración de datos permite a los administradores de datos aplicar etiquetas de uso en el conjunto de datos y el nivel de campo para categorizar los datos según el tipo de políticas que se apliquen.

El marco de control de datos incluye etiquetas de uso de datos predefinidas que se pueden usar para categorizar los datos de tres maneras:

![Categorías de etiquetas de uso de datos](./images/overview/label-categories.png)

* **Etiquetas de datos del contrato &quot;C&quot;:** Etiquete y categorice los datos que tengan obligaciones contractuales o que estén relacionados con políticas de control de datos de clientes.
* **Etiquetas de datos &quot;I&quot; de identidad:** Etiquete y categorice datos que puedan identificar a una persona específica o ponerse en contacto con ella.
* **Etiquetas de datos &quot;S&quot; confidenciales:** Etiquete y categorice datos relacionados con datos confidenciales, como datos geográficos.

>[!NOTE]
>
>Consulte la guía de [etiquetas de uso de datos compatibles](labels/reference.md) para obtener una lista completa de las etiquetas disponibles, así como las definiciones de cada tipo de etiqueta.

Las etiquetas se pueden aplicar en cualquier momento, lo que proporciona flexibilidad en la forma en que elige administrar los datos. La práctica recomendada alienta el etiquetado de datos en cuanto se incorpora en [!DNL Experience Platform]o en cuanto los datos estén disponibles en [!DNL Platform].

Consulte la descripción general sobre [etiquetas de uso de datos](./labels/overview.md) para obtener más información.

## Políticas de uso de datos

Para que las etiquetas de uso de datos admitan de forma eficaz el cumplimiento de los datos, se deben implementar políticas de uso de datos. Las políticas de uso de datos son reglas que describen los tipos de acciones de marketing que se le permite realizar, o que se le restringe, en los datos de [!DNL Experience Platform].

Un ejemplo de una acción de marketing puede ser el deseo de exportar un conjunto de datos a un servicio de terceros. Si existe una política que indica que la Información de identificación personal (PII) no se puede exportar y se ha aplicado una etiqueta &quot;I&quot; (datos de identidad) al conjunto de datos, [!DNL Policy Service] evita cualquier acción que exporte este conjunto de datos a un destino de terceros. Si se produce uno de estos intentos de acción, el servicio de políticas envía un mensaje para informarle de que se ha violado una política de uso de datos.

Hay dos tipos de políticas disponibles:

* **[!UICONTROL Política de control de datos]**: Restringir la activación de datos en función de la acción de marketing que se realice y las etiquetas de uso de datos que lleven los datos en cuestión.
* **[!UICONTROL Política de consentimiento]**: Filtre los perfiles que se pueden activar en [destinos](../destinations/home.md) según las preferencias o el consentimiento de los clientes.

Una vez aplicadas las etiquetas de uso de datos, los administradores de datos pueden crear políticas utilizando la variable [!DNL Policy Service] API o [!DNL Experience Platform] interfaz de usuario. Para obtener más información sobre las políticas de uso de datos y las acciones de marketing, consulte la [información general sobre políticas](./policies/overview.md).

>[!IMPORTANT]
>
>De forma predeterminada, todas las políticas de uso de datos (incluidas las políticas principales proporcionadas por Adobe) están desactivadas. Para que una directiva individual se considere para su aplicación, debe habilitarla manualmente.

## Pasos siguientes

Este documento ofrecía una introducción de alto nivel a la Administración de datos y al marco de la Administración de datos. Ahora puede continuar con el [guía del usuario de etiquetas de uso de datos](labels/user-guide.md) y empiece a agregar etiquetas de uso a los datos de experiencia.

## Apéndice

La siguiente sección proporciona información adicional con respecto a la Administración de datos.

### Terminología de control de datos

En la tabla siguiente se describen términos clave relacionados con la administración de datos y el marco de la administración de datos.

| Término | Definición |
|---|---|
| **Etiquetas de contrato** | Las etiquetas del contrato &quot;C&quot; se utilizan para categorizar los datos que tienen obligaciones contractuales o que están relacionados con las políticas de control de datos de su organización. |
| **Datos entre sitios** | Los datos entre sitios son la combinación de datos de varios sitios, incluida una combinación de datos en el sitio y datos fuera del sitio o una combinación de datos de varias fuentes fuera del sitio. |
| **Administración de datos** | La gobernanza de los datos abarca las estrategias y tecnologías utilizadas para garantizar que los datos se ajusten a las normas y políticas corporativas con respecto al uso de los datos. |
| **Administrador de datos** | El gestor de datos es la persona responsable de la administración, supervisión y aplicación de los activos de datos de una organización. Un gestor de datos también garantiza que las políticas de control de datos se salvaguarden y se mantengan para cumplir con las regulaciones gubernamentales y las políticas de organización. |
| **Etiquetas de uso de datos** | Las etiquetas de uso de datos proporcionan a los usuarios la capacidad de categorizar los datos que reflejan consideraciones relacionadas con la privacidad y condiciones contractuales para cumplir con las regulaciones y políticas corporativas. |
| **Etiquetas de conjuntos de datos** | Las etiquetas se pueden agregar a un conjunto de datos. Todos los campos dentro de un conjunto de datos heredan las etiquetas del conjunto de datos. |
| **Etiquetas de campos** | Las etiquetas de campo son etiquetas de control de datos que se heredan de un conjunto de datos o se aplican directamente a un campo.  Las etiquetas de control de datos aplicadas a un campo no se heredan de un conjunto de datos. |
| **Geofence** | Una geovalla es un límite geográfico virtual, definido por la tecnología GPS o RFID, que permite al software almacenar en déclencheur una respuesta cuando un dispositivo móvil entra o sale de un área en particular. |
| **Etiquetas de identidad** | Las etiquetas &quot;I&quot; de identidad se utilizan para categorizar los datos que pueden identificar a una persona específica o ponerse en contacto con ella. |
| **Segmentación basada en intereses** | La segmentación basada en intereses, también conocida como personalización, se produce si se cumplen las tres condiciones siguientes: los datos recopilados en el sitio se utilizan para hacer inferencias sobre el interés de un usuario, se utilizan en otro contexto, como en otro sitio o aplicación (fuera del sitio) y se utilizan para seleccionar qué contenido o anuncios se sirven en función de esas inferencias. |
| **Acción de marketing** | Una acción de marketing, en el contexto del marco de control de datos, es una acción que [!DNL Experience Platform] toma del consumidor de datos, para lo cual es necesario comprobar si hay infracciones de las políticas de uso de datos |
| **Directiva** | En el marco de control de datos, una política es una regla que describe qué tipo de acciones de marketing se permiten o no en datos específicos. |
| **Etiquetas confidenciales** | Las etiquetas &quot;S&quot; confidenciales se utilizan para categorizar los datos que usted y su organización consideran confidenciales. |

## Recursos adicionales

El siguiente vídeo pretende comprender mejor el marco de control de datos.

>[!VIDEO](https://video.tv.adobe.com/v/29708?quality=12&enable10seconds=on&speedcontrol=on)

En el siguiente vídeo se presenta una introducción a varias funciones de control de datos de Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/36653?quality=12&enable10seconds=on&speedcontrol=on)
