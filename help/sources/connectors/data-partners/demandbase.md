---
title: Demandbase Intent
description: Obtenga información acerca del origen de Demandbase Intent en Experience Platform.
last-substantial-update: 2025-03-26T00:00:00Z
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="Edición B2P" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
exl-id: 62dd27e0-b846-4c04-977f-8a3ab99bc464
source-git-commit: 5757bc84a9aeec18eb5fe21d6f02160b2ba55166
workflow-type: tm+mt
source-wordcount: '1480'
ht-degree: 1%

---

# [!DNL Demandbase Intent]

[!DNL Demandbase] es una plataforma de marketing basada en cuentas que puede usar para que las ventas y el marketing B2B tengan éxito. [!DNL Demandbase Intent] es un origen de Adobe Experience Platform que puede usar para conectar su cuenta de [!DNL Demandbase] a Experience Platform e integrar los datos de intención de la cuenta.

Con el origen [!DNL Demandbase], puede identificar cuentas de alto interés basadas en participaciones en tiempo real. Al priorizar las señales de intención más potentes, puede crear segmentos precisos y ofrecer campañas con objetivos hiperdefinidos, lo que garantiza que los esfuerzos de marketing se centren en las cuentas que tienen más probabilidades de convertirse. La activación de estrategias basadas en la intención permite la optimización del gasto en publicidad, una mayor participación y un mayor ROI.

Lea este documento para obtener información sobre los requisitos previos del origen de [!DNL Demandbase].

## Requisitos previos {#prerequisites}

Lea las siguientes secciones para conocer los pasos previos antes de conectar [!DNL Demandbase] a Experience Platform.

### LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la página [lista de permitidos de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

### Configuración de permisos en Experience Platform

Debe tener los permisos para **[!UICONTROL Ver fuentes]** y **[!UICONTROL Administrar fuentes]** habilitados en su cuenta para conectar su cuenta de [!DNL Demandbase] a Experience Platform. Póngase en contacto con el administrador del producto para obtener los permisos necesarios. Para obtener más información, lea la [guía de la interfaz de usuario de control de acceso](../../../access-control/abac/ui/permissions.md).

### Restricciones de nomenclatura para archivos y directorios

Las restricciones enumeradas a continuación deben tenerse en cuenta al nombrar el archivo o directorio de almacenamiento en la nube:

* Los nombres de componentes de directorio y archivo no pueden superar los 255 caracteres.
* Los nombres de directorio y archivo no pueden terminar con una barra diagonal (`/`). Si se proporciona, se eliminará automáticamente.
* Los siguientes caracteres de URL reservadas deben ser de escape correcto: `! ' ( ) ; @ & = + $ , % # [ ]`
* No se permiten los siguientes caracteres: `" \ / : | < > * ?`.
* No se permiten caracteres de ruta de URL no válidos. Los puntos de código como `\uE000`, si bien son válidos en los nombres de archivo NTFS, no son caracteres Unicode válidos. Además, algunos caracteres ASCII o Unicode, como los caracteres de control (0x00 a 0x1F, \u0081, etc.), tampoco están permitidos. Para las reglas que rigen las cadenas Unicode en HTTP/1.1, consulte [RFC 2616, Section 2.2: Basic Rules](https://www.ietf.org/rfc/rfc2616.txt) y [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
* No se permiten los siguientes nombres de archivo: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carácter de punto (.) y dos caracteres de punto (..).

### Recopilar credenciales necesarias

[!DNL Demandbase] en Experience Platform está alojado por [!DNL Google Cloud Storage]. Para autenticar correctamente su cuenta de [!DNL Demandbase], debe proporcionar los valores adecuados para las siguientes credenciales:

| Credencial | Descripción |
| --- | --- |
| ID de clave de acceso | Identificador de clave de acceso [!DNL Demandbase]. Se trata de una cadena alfanumérica de 61 caracteres que es necesaria para autenticar su cuenta en Experience Platform. |
| Clave de acceso secreta | La clave de acceso secreta [!DNL Demandbase]. Es una cadena de 40 caracteres con codificación base 64 necesaria para autenticar su cuenta en Experience Platform. |
| Nombre del segmento | El bloque [!DNL Demandbase] del cual se extraerán los datos. |
| Ruta de carpeta | La ruta a la carpeta a la que desea proporcionar acceso. |

Para obtener más información sobre estas credenciales, lea la [[!DNL Google Cloud Storage] guía de claves HMAC](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Para obtener información sobre cómo generar su propia clave de acceso, lea la [guía de requisitos previos de la [!DNL Google Cloud Storage] descripción general de origen](../cloud-storage/google-cloud-storage.md#prerequisite-setup-for-connecting-your-google-cloud-storage-account).

## Esquema [!DNL Demandbase]

Lea esta sección para obtener información sobre el esquema [!DNL Demandbase] y la estructura de datos.

El esquema [!DNL Demandbase] se llama **Intención de la compañía semanal**. Es la información de intención semanal (búsqueda anónima del comprador B2B y consumo de contenido) de la cuenta y las palabras clave especificadas. Los datos están en formato parquet.

| Nombre del campo | Tipo de datos | Requerido | Clave empresarial | Notas |
| --- | --- | --- | --- | --- |
| `company_id` | CADENA | VERDADERO | SÍ | El ID de empresa canónico. |
| `domain` | CADENA | VERDADERO | SÍ | El dominio identificado de la cuenta que muestra la intención. |
| `start_date` | FECHA | VERDADERO | SÍ | La fecha de inicio en la que se produjo la actividad por intención en el período de duración. |
| `end_date` | FECHA | VERDADERO | SÍ | La fecha de finalización en la que se produjo la actividad por intención en el período de duración. |
| `duration_type` | CADENA | VERDADERO | SÍ | El tipo de duración. Por lo general, este valor puede ser diario, semanal o mensual, según la duración de resumen elegida. Para esta muestra de datos, este valor es `week`. |
| `keyword_set_id` | CADENA | VERDADERO | SÍ | ID del conjunto de palabras clave. Esto es único para un cliente determinado. |
| `keyword_set` | CADENA | VERDADERO | SÍ | El nombre del conjunto de palabras clave. |
| `keyword` | CADENA | VERDADERO | | La palabra clave Intent. |
| `is_trending` | CADENA | VERDADERO | | El estado actual de una tendencia determinada. El estado de tendencia se mide como una ráfaga en la actividad por intención de tratamiento en la última semana en relación con los promedios de las siete semanas anteriores. |
| `intent_strength` | ENUM[CADENA] | VERDADERO | | Una medida cuantificada de la intensidad por intención. Los valores aceptados incluyen: `HIGH`, `MED` y `LOW`. |
| `num_people_researching` | ENTERO | VERDADERO | | Recuento de personas que pertenecen a `company_id` y que investigaron la palabra clave en los últimos siete días. |
| `num_trending_days` | ENTERO | VERDADERO | | El número de días que la palabra clave fue tendencia en una duración determinada. |
| `trending_score` | ENTERO | VERDADERO | | La puntuación de tendencia. |
| `record_id` | CADENA | VERDADERO | | El ID único del registro principal. |
| `partition_date` | FECHA | VERDADERO | | La fecha de calendario de la instantánea. Esto se realiza semanalmente, al final de la semana. |

{style="table-layout:auto"}

>[!TIP]
>
>Cualquier cambio en el esquema se comunicará a Adobe por adelantado. Para admitir una evolución de esquema sin problemas, es esencial mantener la compatibilidad con versiones anteriores. Experience Platform aplica un método de asignación de versiones solo aditivo, lo que garantiza que las actualizaciones del esquema no sean destructivas. Esto significa que los cambios importantes están estrictamente prohibidos y solo se permiten los cambios que mejoran o amplían el esquema existente.

## Conecte su cuenta de [!DNL Demandbase] a Experience Platform en la interfaz de usuario

Una vez que hayas completado la configuración de requisitos previos, lee el tutorial de [conexión de tu cuenta de  [!DNL Demandbase] a Experience Platform](../../tutorials/ui/create/data-partners/demandbase.md) para iniciar la integración.

## Preguntas frecuentes {#faq}

Lea esta sección para obtener respuestas a las preguntas más frecuentes acerca del origen de [!DNL Demandbase].

### ¿Necesito tener que tener un contrato existente con [!DNL Demandbase] para usar los datos de intención de la cuenta en Real-Time CDP B2B edition?

+++Respuesta

Sí, debe tener un contrato activo con [!DNL Demandbase] para acceder y utilizar los datos de intención en Experience Platform y Real-Time CDP B2B edition. La integración aprovecha el acuerdo existente con [!DNL Demandbase] para ingerir y activar señales de intención de cuenta en Experience Platform y Real-Time CDP.

+++

### ¿Se admiten campos personalizados de [!DNL Demandbase] en esta integración?

+++Respuesta

Actualmente, solo puede utilizar campos estándar de [!DNL Demandbase] para la ingesta y activación. Para ver la lista de campos admitidos, lea la [[!DNL Demandbase] guía de esquema](#schema) para obtener detalles sobre la disponibilidad del campo.

+++

### ¿Puedo ingerir datos de [!DNL Demandbase] en Experience Platform según sea necesario?

+++Respuesta

Sí, puede ingerir datos de [!DNL Demandbase] según sea necesario. Puede crear un nuevo flujo de datos para introducir los datos de intención más recientes, siempre y cuando haya datos nuevos de [!DNL Demandbase]. Sin embargo, solo puede tener un flujo de datos activo a la vez. Por lo tanto, asegúrese de eliminar el flujo de datos existente antes de crear uno nuevo.

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

### ¿Qué campo se usa para hacer coincidir cuentas de [!DNL Demandbase] con Experience Platform?

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

Los datos de intención se pueden usar en [Audiencias de cuenta](../../../segmentation/types/account-audiences.md) para mejorar el direccionamiento, la segmentación y la personalización. Al aprovechar las señales de intención, las empresas pueden identificar cuentas que muestran un alto interés en temas específicos y participar en ellas, lo que optimiza el alcance de marketing y ventas

+++
