---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Notas de la versión del Privacy Service
topic: release notes
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 6%

---


# [!DNL Privacy Service] notas de la versión

Este documento contiene información sobre las nuevas funciones de Adobe Experience Platform [!DNL Privacy Service], así como mejoras y correcciones de errores importantes.

>[!NOTE]
>
>Las últimas notas de la versión de otros [!DNL Experience Platform] servicios se pueden encontrar [aquí](../release-notes/latest/latest.md).

## 9 de septiembre de 2020

### Nuevas funciones

| Función | Descripción |
| --- | --- |
| Apoyo a LGPD (Brasil) | Ahora se pueden crear empleos de privacidad bajo la regulación de Brasil [!DNL Lei Geral de Proteção de Dados] (LGPD, por sus siglas en inglés). Estos trabajos son rastreados bajo el código de regulación `lgpd_bra`. |

## 8 de abril de 2020

### Nuevas funciones

| Función | Descripción |
| --- | --- |
| Compatibilidad con PDPA | [!DNL Privacy] las solicitudes ahora pueden crearse y rastrearse bajo la Ley de Protección de Datos Personales (PDPA) en Tailandia. Al realizar solicitudes de privacidad en la API, la `regulation` matriz acepta el valor &quot;pdpa_tha&quot;. |
| Tipos de Área de nombres en la interfaz de usuario | Ahora puede especificar diferentes tipos de Área de nombres en el Creador de solicitudes en la [!DNL Privacy Service] interfaz de usuario. Consulte la guía [del](ui/user-guide.md) usuario para obtener más información. |
| Desuso de punto final antiguo | El punto final (`data/privacy/gdpr`) de la API anterior ha quedado obsoleto. |

## 14 de enero de 2020

### Nuevas funciones

| Función | Descripción |
| --- | --- |
| [!DNL Privacy Service] renovación de marca | El llamado anteriormente &quot;Servicio de RGPD&quot; ha sido renombrado a [!DNL Privacy Service] medida que el servicio ha crecido para apoyar otras regulaciones además del RGPD. |
| Nuevos extremos de API | La ruta de acceso base para la [!DNL Privacy Service] API se ha actualizado de `/data/privacy/gdpr` a `/data/core/privacy/jobs` |
| Nueva propiedad requerida `regulation` | Al crear nuevos trabajos en la [!DNL Privacy Service] API, se debe proporcionar una `regulation` propiedad en la carga útil de la solicitud para indicar en qué regulación se debe realizar el seguimiento del trabajo. Los valores aceptados son `gdpr` y `ccpa`. Consulte el documento sobre trabajos [de](api/privacy-jobs.md) privacidad en la guía para [!DNL Privacy Service] desarrolladores para obtener más información. |
| Compatibilidad con la autenticación de Adobe Primetime | [!DNL Privacy Service] ahora acepta solicitudes de acceso/eliminación de la autenticación de Adobe Primetime, utilizando `primetimeAuthentication` como valor de producto. See the [Primetime Authentication documentation](http://tve.helpdocsonline.com/how-to-make-a-privacy-request) for more information. |

### Mejoras

* [!DNL Privacy Service] Mejoras en la interfaz de usuario:
   * Páginas de seguimiento de trabajos independientes para las regulaciones de RGPD y CCPA.
   * Nuevo menú desplegable *de tipo* de reglamento para cambiar entre los datos de seguimiento del RGPD y del CCPA.

## 25 de julio de 2019

### Nuevas funciones

| Función | Descripción |
| --- | --- |
| Panel de las métricas de solicitud | El nuevo panel de métricas en la [!DNL Privacy Service] interfaz de usuario proporciona visibilidad de las solicitudes de RGPD enviadas, erróneas y completadas. |
| Generador de solicitudes | Para prestar servicios a organizaciones con usuarios técnicos y no técnicos que envían solicitudes de RGPD, se ha agregado la funcionalidad &quot;Crear solicitud&quot; a la interfaz de usuario. La capacidad de envío de archivos JSON aún está disponible en la interfaz de usuario para las organizaciones que prefieran seguir usándola. [!DNL Privacy Service] |
| Notificaciones de Evento de trabajos de RGPD | Las notificaciones de evento sobre los estados de trabajos del RGPD son un elemento crítico para muchos flujos de trabajo. Aunque las notificaciones se enviaban anteriormente mediante avisos de correo electrónico individuales, las notificaciones de evento de RGPD son mensajes que aprovechan los eventos de Adobe I/O, que se envían a un enlace web configurado para facilitar la automatización de las solicitudes de trabajo. [!DNL Privacy Service] Los usuarios de la interfaz de usuario pueden suscribirse a los eventos GDPR de Adobe I/O para recibir actualizaciones cuando se haya completado un producto o el trabajo GDPR. |

## 18 de abril de 2019

### Mejoras

* El intervalo predeterminado para la tabla de estado en la [!DNL Privacy Service] interfaz de usuario se modificó a un intervalo de 7 días.
* Mejor gestión de excepciones internas.
* Se ha mejorado el rendimiento al introducir el almacenamiento en caché para llamadas internas comunes con bajas tasas de cambio de datos.

### Correcciones de errores

* Se añadió la información de registro que faltaba para las consultas filtradas del `GET /` extremo en la [!DNL Privacy Service] API.

## 11 de abril de 2019

### Mejoras

* Se ha actualizado la interfaz de usuario para admitir nuevas funciones para clientes beta
* Nueva API de métricas para admitir las funciones de la IU 2.0 en la versión beta

## 9 de abril de 2019

### Mejoras

* Se han actualizado todas las llamadas a la API de búsqueda (GET) de forma predeterminada a un intervalo retrospectivo de 30 días
* Uso restringido de API para tener un intervalo de retrospectiva máximo de 45 días

## 14 de febrero de 2019

### Mejoras

* Aplicar el campo en cada envío de POST `include` .
* Aplicar el `include` campo al cargar JSON.

### Correcciones de errores

* Se corrigió un problema en el cual los clientes no podían cargar la [!DNL Privacy Service] interfaz de usuario.