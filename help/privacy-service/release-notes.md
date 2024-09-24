---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Notas de la versión de Privacy Service
description: Las notas de la versión más recientes de Adobe Experience Platform Privacy Service.
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: ht
source-wordcount: '552'
ht-degree: 100%

---

# [!DNL Privacy Service] notas de la versión

Este documento contiene información sobre las nuevas funciones de Adobe Experience Platform [!DNL Privacy Service], así como mejoras y correcciones de errores importantes.

>[!NOTE]
>
>Las notas de la versión más recientes para otros servicios de [!DNL Experience Platform] se encuentran [aquí](../release-notes/latest/latest.md).

## 9 de septiembre de 2020

### Nuevas funciones

| Función | Descripción |
| --- | --- |
| Compatibilidad con LGPD (Brasil) | Ahora se pueden crear trabajos de privacidad en el marco del reglamento [!DNL Lei Geral de Proteção de Dados] (LGPD) de Brasil. El seguimiento de estos trabajos está regulado en el código normativo de `lgpd_bra`. |

## 8 de abril de 2020

### Nuevas funciones

| Función | Descripción |
| --- | --- |
| Compatibilidad con PDPA | Ahora las solicitudes de [!DNL Privacy] se pueden crear y seguir en el marco de la Ley de Protección de Datos Personales (PDPA) de Tailandia. Al realizar solicitudes de privacidad en la API, la matriz de `regulation` acepta el valor “pdpa_tha”. |
| Tipos de espacio de nombres en la IU | Ahora puede especificar diferentes tipos de espacio de nombres en el generador de solicitudes en la interfaz de usuario de [!DNL Privacy Service]. Si desea obtener más información, consulte la [Guía del usuario](ui/user-guide.md). |
| Obsolescencia del punto final anterior | El punto final de API anterior (`data/privacy/gdpr`) ha quedado obsoleto. |

## 14 de enero de 2020

### Nuevas funciones

| Función | Descripción |
| --- | --- |
| Cambio de marca de [!DNL Privacy Service] | El anteriormente denominado “Servicio de RGPD” se ha cambiado a [!DNL Privacy Service] porque el servicio ha crecido para admitir otras regulaciones, además del RGPD. |
| Nuevos puntos finales de API | La ruta base para la API de [!DNL Privacy Service] se ha actualizado de `/data/privacy/gdpr` a `/data/core/privacy/jobs` |
| Nueva propiedad de `regulation` requerida | Al crear nuevos trabajos en la API de [!DNL Privacy Service], se debe proporcionar una propiedad de `regulation` en la carga útil de la solicitud para indicar en qué regulación se debe realizar el seguimiento del trabajo. Los valores aceptados son `gdpr` y `ccpa`. Consulte el documento sobre [trabajos de privacidad](api/privacy-jobs.md) en la guía de la API de [!DNL Privacy Service] para obtener más información. |
| Compatibilidad con la autenticación de Adobe Primetime | [!DNL Privacy Service] ahora acepta las solicitudes de acceso o eliminación de Adobe Primetime Authentication, usando `primetimeAuthentication` como valor de producto. Consulte la [documentación de Primetime Authentication](https://tve.helpdocsonline.com/how-to-make-a-privacy-request) para obtener más información. |

### Mejoras

* Mejoras en la IU de [!DNL Privacy Service]:
   * Páginas de seguimiento de trabajos independientes para las regulaciones RGPD y CCPA.
   * Nuevo menú desplegable *Tipo de regulación* para cambiar entre el seguimiento de datos de RGPD y CCPA.

## 25 de julio de 2019

### Nuevas funciones

| Función | Descripción |
| --- | --- |
| Solicitar panel de control de métricas | El nuevo panel de control de métricas en la interfaz de usuario de [!DNL Privacy Service] proporciona visibilidad sobre las solicitudes de RGPD enviadas, con errores y completadas. |
| Generador de solicitudes | Para dar servicio a organizaciones con usuarios técnicos y no técnicos que envían solicitudes de RGPD, se ha añadido la funcionalidad “Crear solicitud” a la interfaz de usuario. La capacidad de envío de archivos JSON sigue disponible en la interfaz de usuario de [!DNL Privacy Service] para las organizaciones que prefieren seguir utilizándola. |
| Notificaciones de eventos de trabajo de RGPD | Las notificaciones de eventos sobre el estado de los trabajos de RGPD son un elemento esencial para muchos flujos de trabajo. Aunque las notificaciones se notificaban anteriormente mediante avisos de correo electrónico individuales, las notificaciones de eventos de RGPD son mensajes que aprovechan los eventos de Adobe I/O, que se envían a un webhook configurado para facilitar la automatización de las solicitudes de trabajo. Los usuarios de la interfaz de usuario de [!DNL Privacy Service] pueden suscribirse a eventos de RGPD de Adobe I/O para recibir actualizaciones cuando se haya completado un producto o el trabajo de RGPD. |

## 18 de abril de 2019

### Mejoras

* El intervalo predeterminado para la tabla de estado en la interfaz de usuario de [!DNL Privacy Service] se ha modificado a un plazo de 7 días.
* Mejor gestión de excepciones internas.
* Se ha mejorado el rendimiento mediante la introducción del almacenamiento en caché para las llamadas internas comunes con tasas bajas de cambio de datos.

### Correcciones de errores

* Se ha añadido la información de registro que faltaba para las consultas filtradas del punto final `GET /` en la API de [!DNL Privacy Service].

## 11 de abril de 2019

### Mejoras

* Se ha actualizado la interfaz de usuario para admitir nuevas funcionalidades para los clientes beta
* Nueva API de métricas para admitir las funciones de la IU 2.0 en la versión beta

## 9 de abril de 2019

### Mejoras

* Se han actualizado todas las llamadas de API (GET) de consulta a un intervalo retroactivo predeterminado de 30 días
* Se ha restringido el uso de API para tener un intervalo retroactivo máximo de 45 días

## 14 de febrero de 2019

### Mejoras

* Aplicar el campo `include` en cada envío POST.
* Aplicar el campo `include` al cargar JSON.

### Correcciones de errores

* Se ha corregido un problema por el que los clientes no podían cargar la interfaz de usuario de [!DNL Privacy Service].
