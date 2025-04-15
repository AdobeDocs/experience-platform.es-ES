---
title: Bombora Intent
description: Obtenga información sobre la fuente Bombora Intent en Experience Platform.
last-substantial-update: 2025-03-26T00:00:00Z
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="Edición B2P" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
exl-id: d2e81207-8ef5-4e52-bbac-a2fa262d8d08
source-git-commit: 9ab2c4725d2188f772bde1f7a89db2bb47c7a46b
workflow-type: tm+mt
source-wordcount: '1615'
ht-degree: 1%

---

# [!DNL Bombora Intent]

[!DNL Bombora] es una solución de audiencia completa que se especializa en datos de intención B2B. [!DNL Bombora Intent] es un origen de Adobe Experience Platform que puede usar para conectar su cuenta de [!DNL Bombora] a Experience Platform e integrar los datos de intención de la cuenta.

Con el origen [!DNL Bombora Intent], puede integrar los datos de la intención de la empresa [!DNL Bombora's] para identificar las cuentas que investigan activamente sus productos o servicios. Use [!DNL Bombora] para priorizar las cuentas del mercado a fin de crear segmentos precisos y ejecutar campañas de ABM con hiperobjetivos, asegurándose de que los esfuerzos de marketing se centren en las cuentas que tienen más probabilidades de convertirse. Además, puede aprovechar las estrategias basadas en la intención para optimizar el gasto en publicidad, impulsar la participación y maximizar el ROI.

Lea este documento para obtener información sobre los requisitos previos del origen de [!DNL Bombora].

## Casos de uso {#use-cases}

Lea los siguientes ejemplos de casos de uso que puede aplicar al origen [!DNL Bombora].

### Integración de Demand-Side Platform (DSP)

Como especialista en marketing B2B, puede crear una lista de cuentas en Real-Time CDP, identificar compañías que muestren una intención alta para sus productos y, a continuación, activar esta lista en [!DNL Bombora], que se integra directamente con los DSP, lo que le permite ejecutar campañas de publicidad programáticas dirigidas utilizando datos de [!DNL Bombora's]. Esto garantiza que el gasto en publicidad se centre en las empresas que tienen más probabilidades de realizar una conversión.

### Funciones de Account-Based Marketing (ABM)

Como experto en marketing B2B, puede crear una lista de cuentas basada en las señales de intención de origen y de terceros. Luego puede activar esta lista en [!DNL Bombora], donde las capacidades de ABM le permiten dirigirse específicamente a los empleados de estas cuentas, lo que garantiza que los anuncios lleguen a quienes toman decisiones en lugar de a una audiencia amplia.

### Activación de ABM multicanal

Como especialista en marketing B2B, puede crear una lista de cuentas en Real-Time CDP que identifique las empresas con alta intención y activarla en [!DNL Bombora] para ejecutar campañas de destino en varios canales. En medios sociales de pago, puede publicar anuncios personalizados para profesionales en cuentas de destino en plataformas como [!DNL Linkedin] y [!DNL Facebook].

Con las plataformas de publicidad nativas, puede asegurarse de que el contenido llegue a los responsables de la toma de decisiones en contextos relevantes. También puede ampliar las campañas a TV avanzada y enviar anuncios a cuentas clave. Este enfoque multicanal garantiza una mensajería coherente entre plataformas, maximizando las tasas de participación y conversión.

## Requisitos previos {#prerequisites}

Lea las siguientes secciones para conocer los pasos previos antes de conectar [!DNL Bombora] a Experience Platform.

### LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la página [lista de permitidos de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

### Configuración de permisos en Experience Platform

Debe tener los permisos para **[!UICONTROL Ver fuentes]** y **[!UICONTROL Administrar fuentes]** habilitados en su cuenta para conectar su cuenta de [!DNL Bombora] a Experience Platform. Póngase en contacto con el administrador del producto para obtener los permisos necesarios. Para obtener más información, lea la [guía de la interfaz de usuario de control de acceso](../../../access-control/abac/ui/permissions.md).

### Restricciones de nomenclatura para archivos y directorios

Las restricciones enumeradas a continuación deben tenerse en cuenta al nombrar el archivo o directorio de almacenamiento en la nube:

* Los nombres de componentes de directorio y archivo no pueden superar los 255 caracteres.
* Los nombres de directorio y archivo no pueden terminar con una barra diagonal (`/`). Si se proporciona, se eliminará automáticamente.
* Los siguientes caracteres de URL reservadas deben ser de escape correcto: `! ' ( ) ; @ & = + $ , % # [ ]`
* No se permiten los siguientes caracteres: `" \ / : | < > * ?`.
* No se permiten caracteres de ruta de URL no válidos. Los puntos de código como `\uE000`, si bien son válidos en los nombres de archivo NTFS, no son caracteres Unicode válidos. Además, algunos caracteres ASCII o Unicode, como los caracteres de control (0x00 a 0x1F, \u0081, etc.), tampoco están permitidos. Para las reglas que rigen las cadenas Unicode en HTTP/1.1, consulte [RFC 2616, Section 2.2: Basic Rules](https://www.ietf.org/rfc/rfc2616.txt) y [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
* No se permiten los siguientes nombres de archivo: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carácter de punto (.) y dos caracteres de punto (..).

### Recopilar credenciales necesarias

[!DNL Bombora] en Experience Platform está alojado por [!DNL Google Cloud Storage]. Para autenticar correctamente su cuenta de [!DNL Bombora], debe proporcionar los valores adecuados para las siguientes credenciales:

| Credencial | Descripción |
| --- | --- |
| ID de clave de acceso | Identificador de clave de acceso [!DNL Bombora]. Se trata de una cadena alfanumérica de 61 caracteres que es necesaria para autenticar su cuenta en Experience Platform. |
| Clave de acceso secreta | La clave de acceso secreta [!DNL Bombora]. Es una cadena de 40 caracteres con codificación base 64 necesaria para autenticar su cuenta en Experience Platform. |
| Nombre del segmento | El bloque [!DNL Bombora] del cual se extraerán los datos. |

Para obtener más información sobre estas credenciales, lea la [[!DNL Google Cloud Storage] guía de claves HMAC](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Para obtener información sobre cómo generar su propia clave de acceso, lea la [guía de requisitos previos de la [!DNL Google Cloud Storage] descripción general de origen](../cloud-storage/google-cloud-storage.md#prerequisite-setup-for-connecting-your-google-cloud-storage-account).

## Esquema [!DNL Bombora] {#schema}

Lea esta sección para obtener información sobre el esquema [!DNL Bombora] y la estructura de datos.

El esquema [!DNL Bombora] se llama **Intención de cuenta semanal**. Es la información de intención semanal (investigación anónima del comprador B2B y consumo de contenido) sobre cuentas y temas específicos. Los datos están en formato parquet.

| Nombre del campo | Tipo de datos | Requerido | Clave empresarial | Notas |
| --- | --- | --- | --- | --- |
| `Account_Name` | CADENA | VERDADERO | SÍ | El nombre canónico de la compañía. |
| `Domain` | CADENA | VERDADERO | SÍ | El dominio de la cuenta identificada que muestra intención. |
| `Topic_Id` | CADENA | VERDADERO | SÍ | Identificador del tema [!DNL Bombora]. |
| `Topic_Name` | CADENA | VERDADERO | | Nombre del tema [!DNL Bombora]. |
| `Cluster_Name` | CADENA | VERDADERO | | Nombre de clúster en [!DNL Bombora] para un tema determinado. |
| `Cluster_Id` | CADENA | VERDADERO | | Identificador de clúster asociado a un tema determinado. |
| `Composite_Score` | ENTERO | VERDADERO | | La puntuación compuesta representa el patrón de consumo de un dominio para un tema determinado durante un período de tiempo especificado. La puntuación compuesta se mide entre 0 y 100, donde 100 representa la puntuación más alta posible y 0 representa la puntuación más baja. Una puntuación compuesta de más de 60 representa un aumento en el interés por un dominio en un tema en particular. Esto también se conoce como &quot;oleada&quot;. |
| `Partition_Date` | FECHA | VERDADERO | | La fecha de calendario de una instantánea. Esto se realiza semanalmente, al final de la semana, en formato `mm/dd/yyyy`. |

{style="table-layout:auto"}

>[!TIP]
>
>Cualquier cambio en el esquema se comunicará a Adobe por adelantado. Para admitir una evolución de esquema sin problemas, es esencial mantener la compatibilidad con versiones anteriores. Experience Platform aplica un método de asignación de versiones solo aditivo, lo que garantiza que las actualizaciones del esquema no sean destructivas. Esto significa que los cambios importantes están estrictamente prohibidos y solo se permiten los cambios que mejoran o amplían el esquema existente.

## Conecte su cuenta de [!DNL Bombora] a Experience Platform en la interfaz de usuario

Una vez que hayas completado la configuración de requisitos previos, lee el tutorial de [conexión de tu cuenta de  [!DNL Bombora] a Experience Platform](../../tutorials/ui/create/data-partners/bombora.md) para iniciar la integración.

## Preguntas frecuentes {#faq}

Lea esta sección para obtener respuestas a las preguntas más frecuentes acerca del origen de [!DNL Bombora].

### ¿Necesito tener que tener un contrato existente con [!DNL Bombora] para usar los datos de intención de la cuenta en Real-Time CDP B2B edition?

+++Respuesta

Sí, debe tener un contrato activo con [!DNL Bombora] para acceder y utilizar los datos de intención en Experience Platform y Real-Time CDP B2B edition. La integración aprovecha el acuerdo existente con [!DNL Bombora] para ingerir y activar señales de intención de cuenta en Experience Platform y Real-Time CDP.

+++

### ¿Se admiten campos personalizados de [!DNL Bombora] en esta integración?

+++Respuesta

Actualmente, solo puede utilizar campos estándar de [!DNL Bombora] para la ingesta y activación. Para ver la lista de campos admitidos, lea la [[!DNL Bombora] guía de esquema](#schema) para obtener detalles sobre la disponibilidad del campo.

+++

### ¿Puedo ingerir datos de [!DNL Bombora] en Experience Platform según sea necesario?

+++Respuesta

Sí, puede ingerir datos de [!DNL Bombora] según sea necesario. Puede crear un nuevo flujo de datos para introducir los datos de intención más recientes, siempre y cuando haya datos nuevos de [!DNL Bombora]. Sin embargo, solo puede tener un flujo de datos activo a la vez. Por lo tanto, asegúrese de eliminar el flujo de datos existente antes de crear uno nuevo.

+++

### ¿Cuál es el proceso de validación de los datos por intención y cómo puedo comprobar cuáles están vinculados a una cuenta específica?

+++Respuesta

Para validar los datos por intención y determinar qué señales por intención están vinculadas a cuentas específicas, usa [Adobe Experience Platform Query Service](../../../query-service/home.md) de AccountID.

+++

### ¿Cómo puedo buscar una intención para una compañía específica?

+++Respuesta

Ejecute una consulta SQL en [Query Service](../../../query-service/home.md) para buscar datos por intención con el nombre de la empresa o AccountID. Para ver todos los datos de intención de una empresa específica, puede ejecutar una consulta SQL en el servicio de consultas utilizando el nombre de la empresa o AccountID para recuperar todas las señales de intención asociadas.

+++


### He encontrado un problema con el proceso de coincidencia de cuentas en Experience Platform, ¿qué debo hacer?

+++Respuesta

La resolución depende de la cuestión específica:

* **Dominio de compañía incorrecto o ausente en Experience Platform**: Si el problema se debe a un valor de dominio de compañía incorrecto en los datos de la cuenta, actualice el campo de dominio de compañía en Experience Platform para garantizar una coincidencia precisa.
* **Asignación de campo incorrecta en el flujo de datos**: si el problema se debe a una ruta de campo de dominio de compañía incorrecta en el flujo de datos, actualice la configuración del flujo de datos para hacer referencia a la ruta de campo correcta.

+++

### ¿Cómo elimino los datos de intención en Experience Platform?

+++Respuesta

Debe [eliminar el conjunto de datos](../../../catalog/datasets/user-guide.md#delete-a-dataset) para eliminar los datos por intención en Experience Platform.

+++

### ¿Qué campo se usa para hacer coincidir cuentas de [!DNL Bombora] con Experience Platform?

+++Respuesta

El campo `accountOrganization.domain` se usa para las cuentas coincidentes. Si su organización utiliza un campo personalizado diferente para almacenar el nombre del sitio web, asegúrese de proporcionar la ruta de campo correcta para una asignación precisa.

+++

### ¿Qué sucede cuando se actualiza un dominio de empresa en Experience Platform?

+++Respuesta

Cuando se actualiza un dominio de empresa, el nuevo valor de dominio se aplica en la siguiente ejecución del flujo de datos. Esto garantiza que:

* La ingesta de datos por intención futura utiliza el dominio actualizado para la coincidencia de cuentas.
* Ahora, cualquier señal de intención que no coincida correctamente con la cuenta deseada puede alinearse correctamente.
* No se realizan cambios retroactivos a los datos pasados introducidos; solo los datos nuevos y entrantes reflejarán la actualización.

+++

### ¿Qué es el proceso de coincidencia de dominios?

+++Respuesta

La coincidencia de dominios en Experience Platform se basa en una coincidencia exacta del valor del campo de dominio eliminado. Experience Platform quita automáticamente los prefijos (por ejemplo, https:/<span>/www.) y conserva el dominio de nivel superior (por ejemplo, adobe.com). La coincidencia requiere un valor de dominio exacto, sin compatibilidad con la coincidencia aproximada o los subdominios.

+++

### ¿Dónde puedo usar los datos de intención?

+++Respuesta

Los datos de intención se pueden usar en [Audiencias de cuenta](../../../segmentation/types/account-audiences.md) para mejorar el direccionamiento, la segmentación y la personalización. Al aprovechar las señales de intención, las empresas pueden identificar cuentas que muestran un alto interés en temas específicos y participar en ellas, lo que optimiza el alcance de marketing y ventas.

+++
