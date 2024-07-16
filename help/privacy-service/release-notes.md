---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Notas de la versión de Privacy Service
description: Últimas notas de la versión de Adobe Experience Platform Privacy Service.
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 5%

---

# [!DNL Privacy Service] notas de la versión

Este documento contiene información sobre las nuevas características de Adobe Experience Platform [!DNL Privacy Service], así como mejoras y correcciones de errores significativas.

>[!NOTE]
>
>Las notas de la versión más recientes para otros servicios de [!DNL Experience Platform] se encuentran [aquí](../release-notes/latest/latest.md).

## 9 de septiembre de 2020

### Nuevas características

| Función | Descripción |
| --- | --- |
| Compatibilidad con LGPD (Brasil) | Ahora se pueden crear trabajos de privacidad bajo la regulación [!DNL Lei Geral de Proteção de Dados] (LGPD) de Brasil. Estos trabajos se rastrean bajo el código de regulación `lgpd_bra`. |

## 8 de abril de 2020

### Nuevas características

| Función | Descripción |
| --- | --- |
| Compatibilidad con PDPA | Ahora se pueden crear y rastrear [!DNL Privacy] solicitudes en virtud de la Ley de Protección de Datos Personales (PDPA) en Tailandia. Al realizar solicitudes de privacidad en la API, la matriz `regulation` acepta el valor &quot;pdpa_tha&quot;. |
| Tipos de área de nombres en la IU | Ahora puede especificar diferentes tipos de área de nombres en el Generador de solicitudes en la interfaz de usuario de [!DNL Privacy Service]. Consulte la [guía del usuario](ui/user-guide.md) para obtener más información. |
| Obsolescencia del punto final anterior | El extremo de API anterior (`data/privacy/gdpr`) se ha quedado obsoleto. |

## 14 de enero de 2020

### Nuevas características

| Función | Descripción |
| --- | --- |
| [!DNL Privacy Service] cambio de marca | El anteriormente denominado &quot;Servicio de RGPD&quot; se ha cambiado a [!DNL Privacy Service] a medida que el servicio ha crecido para admitir otras regulaciones además del RGPD. |
| Nuevos extremos de API | La ruta de acceso base para la API [!DNL Privacy Service] se ha actualizado de `/data/privacy/gdpr` a `/data/core/privacy/jobs` |
| Nueva propiedad `regulation` requerida | Al crear nuevos trabajos en la API [!DNL Privacy Service], se debe proporcionar una propiedad `regulation` en la carga de la solicitud para indicar en qué regulación se debe realizar el seguimiento del trabajo. Los valores aceptados son `gdpr` y `ccpa`. Consulte el documento sobre [trabajos de privacidad](api/privacy-jobs.md) en la guía de la API [!DNL Privacy Service] para obtener más información. |
| Compatibilidad con la autenticación de Adobe Primetime | [!DNL Privacy Service] ahora acepta solicitudes de acceso o eliminación de la autenticación de Adobe Primetime, usando `primetimeAuthentication` como valor de producto. Consulte la [documentación de autenticación de Primetime](https://tve.helpdocsonline.com/how-to-make-a-privacy-request) para obtener más información. |

### Mejoras

* [!DNL Privacy Service] mejoras en la IU:
   * Páginas de seguimiento de trabajos independientes para las regulaciones del RGPD y CCPA.
   * Nuevo menú desplegable de *Tipo de regulación* para cambiar entre los datos de seguimiento del RGPD y la CCPA.

## 25 de julio de 2019

### Nuevas características

| Función | Descripción |
| --- | --- |
| Solicitar panel de métricas | El nuevo panel de métricas en la interfaz de usuario de [!DNL Privacy Service] proporciona visibilidad sobre las solicitudes de RGPD enviadas, erróneas y completadas. |
| Generador de solicitudes | Para dar servicio a organizaciones con usuarios técnicos y no técnicos que envían solicitudes de RGPD, se ha añadido la funcionalidad &quot;Crear solicitud&quot; a la interfaz de usuario. La capacidad de envío de archivos JSON sigue disponible en la interfaz de usuario de [!DNL Privacy Service] para las organizaciones que prefieren seguir utilizándola. |
| Notificaciones de eventos de trabajo de RGPD | Las notificaciones de eventos sobre los estados de trabajos del RGPD son un elemento crítico para muchos flujos de trabajo. Aunque las notificaciones se notificaban anteriormente mediante avisos de correo electrónico individuales, las notificaciones de eventos del RGPD son mensajes que aprovechan los eventos de Adobe I/O, que se envían a un gancho web configurado para facilitar la automatización de las solicitudes de trabajo. [!DNL Privacy Service] usuarios de la interfaz de usuario pueden suscribirse a eventos de RGPD de Adobe I/O para recibir actualizaciones cuando se haya completado un producto o el trabajo de RGPD. |

## 18 de abril de 2019

### Mejoras

* Intervalo predeterminado para la tabla de estado en la interfaz de usuario de [!DNL Privacy Service] modificado a un intervalo de 7 días.
* Mejor gestión de excepciones internas.
* Se ha mejorado el rendimiento mediante la introducción del almacenamiento en caché para llamadas internas comunes con tasas de cambio de datos bajas.

### Correcciones de errores

* Se ha agregado la información de registro que falta para las consultas filtradas del extremo `GET /` en la API [!DNL Privacy Service].

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

* Aplicar el campo `include` en cada envío de POST.
* Aplicar el campo `include` al cargar JSON.

### Correcciones de errores

* Se corrigió un problema en el cual los clientes no podían cargar la interfaz de usuario de [!DNL Privacy Service].
