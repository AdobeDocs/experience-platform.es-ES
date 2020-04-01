---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Gobierno de datos de la plataforma Adobe Experience
topic: overview
translation-type: tm+mt
source-git-commit: 4a60956ade2d742ac83e138a2921a6a4893e06ef

---


# Información general sobre la administración de datos

Una de las funciones principales de Adobe Experience Platform es reunir datos de varios sistemas empresariales para permitir que los especialistas en marketing identifiquen, comprendan y capten mejor a los clientes. Estos datos pueden estar sujetos a restricciones de uso definidas por su organización o por las regulaciones legales. Por lo tanto, es importante asegurarse de que las operaciones de datos dentro de la plataforma sean compatibles con las políticas de uso de datos.

El Gobierno de datos de la plataforma de experiencia de Adobe le permite administrar los datos de los clientes y garantizar el cumplimiento de las normativas, restricciones y políticas aplicables al uso de los datos. Desempeña un papel clave dentro de la plataforma de experiencias en varios niveles, incluso la catalogación, el linaje de datos, el etiquetado del uso de datos, las políticas de uso de datos y el control del uso de datos para las acciones de marketing.

## Funciones de administración de datos

Como concepto, la gobernanza de los datos no es automática ni se da en un vacío. Lo que comenzó como un papel para un individuo, generalmente reconocido como un supervisor **de** datos, ha crecido considerablemente a medida que se ha expandido el ecosistema de gobernanza de datos. En la actualidad, la gestión de los datos requiere una gestión y supervisión continuas para tener éxito y depende de que los administradores de datos cuenten con herramientas con las que se puedan etiquetar correctamente los datos, se puedan crear políticas de uso y se pueda hacer cumplir el cumplimiento de dichas políticas.

Si bien la gobernanza de los datos debe ser responsabilidad de cada individuo en la organización, aquí hay algunas de las funciones esenciales dentro del ciclo de gobernanza de los datos:

![Funciones de administración de datos](./images/overview/roles.png)

### Administrador de datos

Los administradores de datos son el núcleo de la gobernanza de los datos. Esta función es responsable de interpretar regulaciones, restricciones contractuales y políticas, y de aplicarlas directamente a los datos. Informados por su comprensión de estas regulaciones, restricciones y políticas, el rol de un administrador de datos incluye:

* Revisión de datos, conjuntos de datos y muestras de datos para aplicar y administrar el etiquetado de uso de metadatos.
* Creación de directivas de datos y aplicación de dichas directivas a conjuntos de datos y campos.
* Comunicación de directivas de datos a la organización.

### Especialista en marketing

Los especialistas en mercadotecnia son el punto final del gobierno de los datos. Solicitan datos de la infraestructura de gestión de datos creada por los encargados de la gestión de datos, científicos e ingenieros. Los especialistas en mercadotecnia incluyen una serie de especialidades diferentes en el marco de la mercadotecnia, entre las que se incluyen las siguientes:

* Los analistas de marketing solicitan datos para permitir comprender a los clientes, tanto como individuos como en grupos (también conocidos como segmentos).
* Los especialistas en marketing y los diseñadores de experiencias utilizan los datos para diseñar nuevas experiencias de cliente.


## Marco DULE

El etiquetado y cumplimiento del uso de datos (DULE) es el marco básico para el gobierno de datos de la plataforma de experiencia. DULE simplifica y optimiza el proceso de categorización de datos y creación de políticas de uso de datos. Una vez aplicadas las etiquetas de datos y establecidas las políticas de uso de datos, se pueden evaluar las acciones de marketing para garantizar el uso correcto de los datos.

Existen tres elementos clave en el marco DULE: Etiquetas, políticas y aplicación.

1. **Etiquetas:** Clasifique los datos que reflejen consideraciones relacionadas con la privacidad y las condiciones contractuales para que sean compatibles con las normativas y políticas de organización.
1. **Políticas:** Describa qué tipo o tipos de acciones de mercadotecnia se permiten o no se pueden realizar en datos específicos.
1. **Aplicación:** Utiliza el marco de políticas para asesorar y aplicar políticas en diferentes patrones de acceso a datos.

## Etiquetas de uso de datos

La Administración de datos permite a los administradores de datos aplicar etiquetas de uso en el nivel de base de datos y campo para categorizar los datos según el tipo de directivas que se apliquen.

El marco de trabajo DULE incluye etiquetas de uso de datos predefinidas que pueden utilizarse para categorizar los datos de cuatro maneras:

![Categorías de etiquetas de uso de datos](./images/overview/label-categories.png)

* **Etiquetas de datos del contrato &quot;C&quot;:** Etiquete y categorice los datos que tienen obligaciones contractuales o que están relacionados con políticas de control de datos de clientes.
* **Etiquetas de datos &quot;I&quot; de identidad:** Etiquete y categorice los datos que pueden identificar o comunicarse con una persona específica.
* **Etiquetas De Datos &quot;S&quot; Sensibles:** Etiquete y categorice los datos relacionados con datos confidenciales, como datos geográficos.
* **Etiquetas de datos de RGPD:** Etiquete y categorice los datos que pueden contener identificadores personales para su uso en solicitudes de acceso y/o eliminación de RGPD.

>[!NOTE] Consulte la guía sobre las etiquetas [de uso de datos](labels/reference.md) admitidas para obtener una lista completa de las etiquetas disponibles, así como las definiciones de cada tipo de etiqueta.

Las etiquetas se pueden aplicar en cualquier momento, lo que proporciona flexibilidad en la forma en que se decide gobernar los datos. La práctica recomendada aconseja etiquetar los datos tan pronto como se incorporen a la plataforma de experiencia o tan pronto como los datos estén disponibles en la plataforma.

Consulte la descripción general de las etiquetas [de uso de](./labels/overview.md) datos para obtener instrucciones paso a paso sobre cómo aplicar etiquetas a conjuntos de datos y campos mediante la interfaz de usuario.

## Directivas de uso de datos

Para que las etiquetas de uso de datos admitan de manera efectiva el cumplimiento de los datos, se deben implementar políticas de uso de datos. Las directivas de uso de datos son reglas que describen los tipos de acciones de marketing que puede realizar o que tienen restricciones para realizar en los datos de la plataforma de experiencia.

Un ejemplo de una acción de marketing puede ser el deseo de exportar un conjunto de datos a un servicio de terceros. Si existe una política que indica que determinados tipos de datos, como Información de identificación personal (PII), no se pueden exportar y se ha aplicado una etiqueta &quot;I&quot; (Datos de identidad) al conjunto de datos, recibirá una respuesta del Servicio de directivas que le indicará que se ha violado una política de uso de datos.

### Cómo crear y trabajar con políticas de uso de datos

Una vez aplicadas las etiquetas de uso de datos, los administradores de datos pueden crear políticas mediante la API de servicio de directivas DULE.

Como administrador de datos, puede utilizar la API de servicio de directivas para administrar y evaluar las políticas relacionadas con las acciones de marketing que se realizan en datos que contienen etiquetas DULE. Mediante la API, puede crear y actualizar políticas, determinar el estado de una política y trabajar con acciones de marketing para evaluar si una acción específica infringe una política de uso de datos.

Dentro de la API de servicio de directivas, todas las directivas y acciones de marketing se denominan `core` o `custom` recursos. `core` los recursos son definidos y mantenidos por Adobe, mientras que `custom` los recursos son creados y mantenidos por clientes individuales. Por lo tanto, los `custom` recursos son únicos y visibles únicamente para la organización que los creó.

Para obtener más información sobre cómo realizar las operaciones clave proporcionadas por la API de servicio de directivas DULE, consulte la guía [para desarrolladores de](api/getting-started.md)Policy Service. Para obtener instrucciones paso a paso sobre cómo trabajar con políticas DULE, consulte el tutorial sobre la [creación y evaluación de políticas](policies/create.md)DULE.

## Versiones futuras

El Gobierno de datos admite actualmente el etiquetado DULE en dos niveles (conjunto de datos y campo). La Administración de datos también admite la creación y administración de políticas de uso de datos y acciones de marketing a través de la API del servicio de políticas DULE.

Las versiones posteriores proporcionarán las siguientes funciones:

* Etiquetas de uso de datos personalizadas: Cree nuevas etiquetas y definiciones en función de las necesidades de su organización.
* Aplicación de políticas: Utilice el marco de políticas para asesorar y aplicar políticas en diferentes patrones de acceso a datos.
* Auditoría: Monitorear las actividades de acceso a datos e identificar los problemas de cumplimiento e informar al respecto.

## Pasos siguientes

Este documento proporcionó una introducción de alto nivel sobre la gobernanza de los datos y el marco de trabajo del DULE. Ahora puede continuar con las etiquetas de uso de [datos, la guía](labels/user-guide.md) del usuario y el inicio de agregar etiquetas de uso a los datos de experiencia.

## Apéndice

La siguiente sección proporciona información adicional con respecto a la Administración de datos.

### Terminología de la administración de datos

La siguiente tabla describe los términos clave relacionados con la administración de datos y el marco DULE.

| Término | Definición |
|---|---|
| **Etiquetas de contrato** | Las etiquetas &quot;C&quot; del contrato se utilizan para categorizar los datos que tienen obligaciones contractuales o que están relacionados con las políticas de administración de datos de su organización. |
| **Datos entre sitios** | Los datos entre sitios son la combinación de datos de varios sitios, incluida una combinación de datos en el sitio y datos fuera del sitio o una combinación de datos de varias fuentes fuera del sitio. |
| **Administración de datos** | La gobernanza de los datos abarca las estrategias y tecnologías utilizadas para garantizar que los datos se ajusten a las normativas y políticas institucionales en lo que respecta al uso de los datos. |
| **Administrador de datos** | El administrador de datos es la persona responsable de la administración, supervisión y ejecución de los activos de datos de una organización. Un administrador de datos también garantiza que las políticas de control de datos se salvaguarden y mantienen para cumplir con las regulaciones y políticas de organización del gobierno. |
| **Etiquetas de uso de datos** | Las etiquetas de uso de datos proporcionan a los usuarios la capacidad de categorizar los datos que reflejan consideraciones relacionadas con la privacidad y condiciones contractuales para cumplir con las normativas y políticas corporativas. |
| **Etiquetas de datos** | Las etiquetas se pueden agregar a un conjunto de datos. Todos los campos dentro de un conjunto de datos heredan las etiquetas del conjunto de datos. |
| **DULE** | DULE es un acrónimo de &quot;Etiquetado y aplicación del uso de datos&quot;. Una parte clave de la administración de datos, DULE es una recopilación de características que permite etiquetar el uso de datos y aplicar políticas de acceso a datos para satisfacer las necesidades de gobernanza dentro de una organización. |
| **Etiquetas de campo** | Las etiquetas de campo son etiquetas de control de datos que se heredan de un conjunto de datos o se aplican directamente a un campo.  Las etiquetas de control de datos aplicadas a un campo no se heredan hasta un conjunto de datos. |
| **Geofence** | Una geofence es un límite geográfico virtual, definido por la tecnología GPS o RFID, que permite al software activar una respuesta cuando un dispositivo móvil entra o sale de un área en particular. |
| **Etiquetas de identidad** | Las etiquetas &quot;I&quot; de identidad se utilizan para categorizar los datos que pueden identificar o comunicarse con una persona específica. |
| **Targeting basado en intereses** | La segmentación basada en intereses, también conocida como personalización, se produce si se cumplen las tres condiciones siguientes: los datos recopilados en el sitio se utilizan para hacer inferencias sobre el interés de los usuarios, se utilizan en otro contexto, como en otro sitio o aplicación (fuera del sitio) y se utilizan para seleccionar qué contenido o anuncios se ofrecen en función de esas inferencias. |
| **Acción de mercadotecnia** | Una acción de mercadotecnia, en el contexto del marco de administración de datos, es una acción que realiza un consumidor de datos de la plataforma de experiencia, para la cual es necesario verificar las violaciones de las políticas de uso de datos |
| **Política** | En el marco de administración de datos, una política es una regla que describe qué tipo de acciones de mercadotecnia se permiten o no se permiten realizar en datos específicos. |
| **Etiquetas sensibles** | Las etiquetas &quot;S&quot; confidenciales se utilizan para categorizar los datos que usted y su organización consideran confidenciales. |

## Recursos adicionales   

El siguiente vídeo está diseñado para apoyar su comprensión del Gobierno de datos y describe los aspectos clave del marco de aplicación y etiquetado del uso de datos (DULE).

>[!VIDEO](https://video.tv.adobe.com/v/29708?quality=12&enable10seconds=on&speedcontrol=on)
