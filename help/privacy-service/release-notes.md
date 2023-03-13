---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Notas de la versión de Privacy Service
description: Últimas notas de la versión de Adobe Experience Platform Privacy Service.
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 5%

---

# [!DNL Privacy Service] notas de la versión

Este documento contiene información sobre las nuevas funciones de Adobe Experience Platform [!DNL Privacy Service], así como mejoras y correcciones de errores significativas.

>[!NOTE]
>
>Las notas de la versión más recientes para otros [!DNL Experience Platform] se pueden encontrar los servicios de [aquí](../release-notes/latest/latest.md).

## 9 de septiembre de 2020

### Nuevas funciones

| Función | Descripción |
| --- | --- |
| Compatibilidad con LGPD (Brasil) | Ahora se pueden crear trabajos de privacidad bajo la ley de Brasil [!DNL Lei Geral de Proteção de Dados] (LGPD). Estos trabajos se rastrean bajo el código de regulación `lgpd_bra`. |

## 8 de abril de 2020

### Nuevas funciones

| Función | Descripción |
| --- | --- |
| Compatibilidad con PDPA | [!DNL Privacy] Ahora, las solicitudes se pueden crear y rastrear según la Ley de Protección de Datos Personales (PDPA) en Tailandia. Al realizar solicitudes de privacidad en la API, la variable `regulation` la matriz acepta el valor &quot;pdpa_tha&quot;. |
| Tipos de área de nombres en la IU | Ahora puede especificar diferentes tipos de áreas de nombres en el Generador de solicitudes en la variable [!DNL Privacy Service] IU. Consulte la [guía del usuario](ui/user-guide.md) para obtener más información. |
| Obsolescencia del punto final anterior | El antiguo extremo de la API (`data/privacy/gdpr`) se ha desaprobado. |

## 14 de enero de 2020

### Nuevas funciones

| Función | Descripción |
| --- | --- |
| [!DNL Privacy Service] cambio de marca | El anteriormente denominado &quot;Servicio RGPD&quot; se ha cambiado a [!DNL Privacy Service] ya que el servicio ha crecido para admitir otras regulaciones además del RGPD. |
| Nuevos extremos de API | Ruta básica para [!DNL Privacy Service] La API se ha actualizado desde `/data/privacy/gdpr` hasta `/data/core/privacy/jobs` |
| Nuevo obligatorio `regulation` propiedad | Al crear nuevos trabajos en [!DNL Privacy Service] API, a `regulation` La propiedad debe proporcionarse en la carga útil de la solicitud para indicar en qué regulación se debe rastrear el trabajo. Los valores aceptados son `gdpr` y `ccpa`. Consulte el documento sobre [trabajos de privacidad](api/privacy-jobs.md) en el [!DNL Privacy Service] Guía de API para obtener más información. |
| Compatibilidad con la autenticación de Adobe Primetime | [!DNL Privacy Service] ahora acepta solicitudes de acceso o eliminación de la autenticación de Adobe Primetime, utilizando `primetimeAuthentication` como su valor de producto. Consulte la [Documentación de autenticación de Primetime](https://tve.helpdocsonline.com/how-to-make-a-privacy-request) para obtener más información. |

### Mejoras

* [!DNL Privacy Service] Mejoras en la IU:
   * Páginas de seguimiento de trabajos independientes para las regulaciones del RGPD y CCPA.
   * Nuevo *Tipo de regulación* para cambiar entre los datos de seguimiento para el RGPD y la CCPA.

## 25 de julio de 2019

### Nuevas funciones

| Función | Descripción |
| --- | --- |
| Solicitar panel de métricas | El nuevo tablero de métricas en la variable [!DNL Privacy Service] La interfaz de usuario proporciona visibilidad de las solicitudes de RGPD enviadas, erróneas y completadas. |
| Generador de solicitudes | Para dar servicio a organizaciones con usuarios técnicos y no técnicos que envían solicitudes de RGPD, se ha añadido la funcionalidad &quot;Crear solicitud&quot; a la interfaz de usuario. La capacidad de envío de archivos JSON sigue disponible en el [!DNL Privacy Service] Interfaz de usuario para las organizaciones que prefieren seguir usándola. |
| Notificaciones de eventos de trabajo de RGPD | Las notificaciones de eventos sobre los estados de trabajos del RGPD son un elemento crítico para muchos flujos de trabajo. Aunque las notificaciones se notificaban anteriormente mediante avisos de correo electrónico individuales, las notificaciones de eventos del RGPD son mensajes que aprovechan los eventos de Adobe I/O, que se envían a un gancho web configurado para facilitar la automatización de las solicitudes de trabajo. [!DNL Privacy Service] Los usuarios de la IU pueden suscribirse a eventos de RGPD de Adobe I/O para recibir actualizaciones cuando se haya completado un producto o el trabajo de RGPD. |

## 18 de abril de 2019

### Mejoras

* Intervalo predeterminado para la tabla de estado en [!DNL Privacy Service] IU modificada a un intervalo de 7 días.
* Mejor gestión de excepciones internas.
* Se ha mejorado el rendimiento mediante la introducción del almacenamiento en caché para llamadas internas comunes con tasas de cambio de datos bajas.

### Correcciones de errores

* Se ha añadido la información de registro que falta para las consultas filtradas de `GET /` punto final en la [!DNL Privacy Service] API.

## 11 de abril de 2019

### Mejoras

* Se ha actualizado la interfaz de usuario para admitir nuevas funciones para los clientes de la beta
* Nueva API de métricas para admitir las funciones de la IU 2.0 en la versión beta

## 9 de abril de 2019

### Mejoras

* Se han actualizado todas las llamadas de API de búsqueda (GET) a un intervalo retrospectivo predeterminado de 30 días
* Uso de API restringido para tener un intervalo retrospectivo máximo de 45 días

## 14 de febrero de 2019

### Mejoras

* Aplicar la `include` en cada envío de POST.
* Aplicar la `include` al cargar JSON.

### Correcciones de errores

* Se ha corregido un problema en el cual los clientes no podían cargar [!DNL Privacy Service] IU.
