---
keywords: Experience Platform;inicio;temas populares;DULE;dule
solution: Experience Platform
title: Información general sobre gobernanza de datos
description: Administración de datos de Adobe Experience Platform le permite administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos. Desempeña un papel clave dentro de Experience Platform en varios niveles, incluida la catalogación, el linaje de datos, el etiquetado del uso de los datos, las políticas de uso de los datos y el control del uso de los datos para las acciones de marketing
exl-id: 00ca6bc2-1c58-4ea2-8bb5-30fd3fa5944a
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1479'
ht-degree: 5%

---

# Resumen de gobernanza de datos

Una de las funciones principales de Adobe Experience Platform es reunir datos de varios sistemas empresariales para permitir que los especialistas en marketing identifiquen, comprendan y capturen clientes. Estos datos pueden estar sujetos a restricciones de uso definidas por su organización o por la normativa legal. Por lo tanto, es importante asegurarse de que las operaciones de datos dentro de [!DNL Platform] cumplen con las políticas de uso de datos.

Administración de datos de Adobe Experience Platform le permite administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos. Desempeña un papel clave dentro de [!DNL Experience Platform] en varios niveles, incluida la catalogación, el linaje de datos, el etiquetado de uso de datos, las políticas de uso de datos y el control del uso de datos para acciones de marketing.

>[!NOTE]
>
>En Experience Platform, el control de datos solo afecta a cómo se utilizan o activan los datos, independientemente de si el usuario realiza la acción. Para obtener información sobre cómo controlar el acceso a campos de datos específicos para determinados usuarios de Platform de su organización, consulte la documentación sobre [control de acceso basado en atributos](../access-control/abac/overview.md) en su lugar.

## Funciones de gobernanza de datos

Como concepto, la gobernanza de datos no es automática ni se produce en el vacío. Lo que comenzó como un rol para un individuo, generalmente reconocido como administrador de datos, ha crecido considerablemente a medida que el ecosistema de gobernanza de datos se ha expandido. Actualmente, la gobernanza de datos requiere una administración y una monitorización continuas para tener éxito y depende de que los administradores de datos tengan herramientas con las que se puedan etiquetar correctamente los datos, se puedan crear políticas de uso y se pueda aplicar el cumplimiento de esas políticas.

Aunque la gobernanza de datos debe ser responsabilidad de cada individuo en la organización, estas son algunas de las funciones esenciales dentro del ciclo de gobernanza de datos:

![Funciones de control de datos](./images/overview/roles.png)

### Administrador de datos

Los administradores de datos son el corazón de la gobernanza de datos. Esta función es responsable de interpretar las regulaciones, las restricciones contractuales y las políticas, y de aplicarlas directamente a los datos. Basándose en su comprensión de estas regulaciones, restricciones y políticas, la función de administrador de datos incluye:

* Revisar datos, conjuntos de datos y ejemplos de datos para aplicar y administrar el etiquetado de uso de metadatos.
* Crear directivas de datos y aplicarlas a conjuntos de datos y campos.
* Comunicar directivas de datos a la organización.

### Experto en marketing

Los especialistas en marketing son el punto final de la gobernanza de datos. Solicitan datos de la infraestructura de control de datos creada por administradores de datos, científicos e ingenieros. Los especialistas en marketing abarcan una serie de especialidades diferentes bajo el paraguas del marketing, entre las que se incluyen las siguientes:

* Los analistas de marketing solicitan datos para permitir comprender a los clientes, tanto como individuos como en grupos (también conocidos como segmentos).
* Los especialistas en marketing y los diseñadores de experiencias utilizan datos de para diseñar nuevas experiencias para los clientes.


## Marco de gobernanza de datos

El marco de trabajo de control de datos simplifica y optimiza el proceso de categorizar los datos y crear políticas de uso de datos. Una vez aplicadas las etiquetas de datos y establecidas las políticas de uso de datos, se pueden evaluar las acciones de marketing para garantizar el uso correcto de los datos.

El marco de trabajo de gobernanza de datos consta de tres elementos clave: etiquetas, políticas y aplicación.

1. **Etiquetas:** Clasifique los datos que reflejan consideraciones relacionadas con la privacidad y condiciones contractuales para cumplir con las regulaciones y políticas de la organización.
1. **Políticas:** Describa qué tipo(s) de acciones de marketing se permite o no realizar en datos específicos.
1. **Aplicación:** Utiliza el marco de directivas para aconsejar y aplicar directivas en distintos patrones de acceso a datos.

## Etiquetas de uso de datos

Administración de datos permite a los administradores de datos aplicar etiquetas de uso en el conjunto de datos y en el nivel de campo para categorizar los datos según el tipo de directivas que se apliquen.

El marco de trabajo de control de datos incluye etiquetas de uso de datos predefinidas que se pueden utilizar para categorizar los datos de tres maneras:

![Categorías de etiquetas de uso de datos](./images/overview/label-categories.png)

* **Etiquetas de datos del contrato &quot;C&quot;:** Etiquete y categorice los datos que tienen obligaciones contractuales o están relacionados con las políticas de gobernanza de datos del cliente.
* **Etiquetas de datos de identidad &quot;I&quot;:** Etiquete y categorice datos que puedan identificar o contactar a una persona específica.
* **Etiquetas De Datos &quot;S&quot; Confidenciales:** Etiquete y categorice los datos relacionados con datos confidenciales, como datos geográficos.

>[!NOTE]
>
>Consulte la guía de [etiquetas de uso de datos admitidas](labels/reference.md) para obtener una lista completa de las etiquetas disponibles, así como definiciones para cada tipo de etiqueta.

Las etiquetas se pueden aplicar en cualquier momento, lo que proporciona flexibilidad en la forma en que se decide administrar los datos. Una práctica recomendada recomienda etiquetar los datos en cuanto se incorporen en [!DNL Experience Platform]o en cuanto los datos estén disponibles en [!DNL Platform].

Consulte la información general sobre [etiquetas de uso de datos](./labels/overview.md) para obtener más información.

## Políticas de uso de datos

Para que las etiquetas de uso de datos respalden con eficacia el cumplimiento, deben implementarse políticas de uso de datos. Las políticas de uso de datos son reglas que describen los tipos de acciones de marketing que se le permite realizar, o que se le restringe, en los datos de [!DNL Experience Platform].

Un ejemplo de acción de marketing puede ser el deseo de exportar un conjunto de datos a un servicio de terceros. Si existe una política que diga que la información de identificación personal (PII) no se puede exportar y se ha aplicado una etiqueta &quot;I&quot; (datos de identidad) al conjunto de datos, [!DNL Policy Service] evita cualquier acción que pueda exportar este conjunto de datos a un destino de terceros. Si se produce uno de estos intentos de acción, el Servicio de directivas envía un mensaje para informarle de que se ha infringido una directiva de uso de datos.

Hay dos tipos de directivas disponibles:

* **[!UICONTROL Política de gobernanza de datos]**: Restrinja la activación de datos en función de la acción de marketing que se esté realizando y las etiquetas de uso de datos que lleven los datos en cuestión.
* **[!UICONTROL Política de consentimiento]**: filtre los perfiles que se pueden activar en [destinos](../destinations/home.md) en función del consentimiento o las preferencias de los clientes.

Una vez aplicadas las etiquetas de uso de datos, los administradores de datos pueden crear políticas utilizando [!DNL Policy Service] API para [!DNL Experience Platform] interfaz de usuario. Para obtener más información sobre las políticas de uso de datos y las acciones de marketing, consulte la [información general sobre directivas](./policies/overview.md).

>[!IMPORTANT]
>
>Todas las políticas de uso de datos (incluidas las políticas principales proporcionadas por Adobe) están desactivadas de forma predeterminada. Para que una directiva individual pueda considerarse para su aplicación, debe habilitarla manualmente.

## Pasos siguientes

Este documento proporciona una introducción de alto nivel a la gobernanza de datos y al marco de trabajo de gobernanza de datos. Ahora puede continuar con el [guía del usuario sobre etiquetas de uso de datos](labels/user-guide.md) y empiece a añadir etiquetas de uso a los datos de experiencia.

## Apéndice

La siguiente sección proporciona información adicional sobre la gobernanza de datos.

### Terminología de control de datos

En la tabla siguiente se describen los términos clave relacionados con la gobernanza de datos y el marco de trabajo de gobernanza de datos.

| Término | Definición |
|---|---|
| **Etiquetas de contrato** | Las etiquetas del contrato &quot;C&quot; se utilizan para categorizar los datos que tienen obligaciones contractuales o están relacionados con las políticas de gobernanza de datos de su organización. |
| **Datos entre sitios** | Los datos entre sitios son la combinación de datos de varios sitios, incluida una combinación de datos in situ y datos externos o una combinación de datos de varias fuentes externas. |
| **Gobernanza de datos** | La gobernanza de datos abarca las estrategias y tecnologías utilizadas para garantizar que los datos cumplan con las regulaciones y las políticas corporativas con respecto al uso de datos. |
| **Administrador de datos** | El administrador de datos es la persona responsable de la administración, la supervisión y la aplicación de los recursos de datos de una organización. Un administrador de datos también garantiza que las políticas de gobernanza de datos se salvaguarden y mantengan para cumplir con las regulaciones gubernamentales y las políticas de la organización. |
| **Etiquetas de uso de datos** | Las etiquetas de uso de datos permiten a los usuarios categorizar los datos que reflejan consideraciones relacionadas con la privacidad y condiciones contractuales para cumplir con las normativas y las políticas corporativas. |
| **Etiquetas de conjuntos de datos** | Las etiquetas se pueden añadir a un conjunto de datos. Todos los campos de un conjunto de datos heredan las etiquetas de este. |
| **Etiquetas de campo** | Las etiquetas de campo son etiquetas de control de datos que se heredan de un conjunto de datos o se aplican directamente a un campo.  Las etiquetas de gobernanza de datos aplicadas a un campo no se heredan hasta un conjunto de datos. |
| **Geoperímetro** | Una geovalla es un límite geográfico virtual, definido por la tecnología GPS o RFID, que permite al software almacenar en déclencheur una respuesta cuando un dispositivo móvil entra o sale de una zona en particular. |
| **Etiquetas de identidad** | Las etiquetas de identidad &quot;I&quot; se utilizan para categorizar los datos que pueden identificar o contactar a una persona específica. |
| **Direccionamiento basado en intereses** | La segmentación basada en intereses, también conocida como personalización, se produce si se cumplen las tres condiciones siguientes: los datos recopilados en el sitio se utilizan para hacer deducciones sobre los intereses de un usuario, se utilizan en otro contexto, como en otro sitio o aplicación (fuera del sitio) y se utilizan para seleccionar qué contenido o anuncios se muestran en función de esas deducciones. |
| **Acción de marketing** | Una acción de marketing, en el contexto del marco de trabajo de gobernanza de datos, es una acción que puede [!DNL Experience Platform] toma el consumidor de datos, para lo cual es necesario comprobar si se han infringido las políticas de uso de datos |
| **Directiva** | En el marco de trabajo de gobernanza de datos, una política es una regla que describe qué tipo de acciones de marketing se permiten o no se permiten realizar en datos específicos. |
| **Etiquetas confidenciales** | Las etiquetas confidenciales &quot;S&quot; se utilizan para categorizar los datos que usted y su organización consideran confidenciales. |

## Recursos adicionales

El siguiente vídeo tiene como objetivo ayudarle a comprender el marco de trabajo de control de datos.

>[!VIDEO](https://video.tv.adobe.com/v/29708?quality=12&enable10seconds=on&speedcontrol=on)

El siguiente vídeo ofrece una introducción a varias funciones de control de datos en Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/36653?quality=12&enable10seconds=on&speedcontrol=on)
