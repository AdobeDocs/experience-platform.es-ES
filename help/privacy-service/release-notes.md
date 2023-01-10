---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Notas de la versión del Privacy Service
description: Últimas notas de la versión de Adobe Experience Platform Privacy Service.
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 5%

---

# [!DNL Privacy Service] notas de la versión

Este documento contiene información sobre las nuevas funciones de Adobe Experience Platform [!DNL Privacy Service], así como mejoras y correcciones de errores importantes.

>[!NOTE]
>
>Las últimas notas de la versión de otros [!DNL Experience Platform] se pueden encontrar los servicios [here](../release-notes/latest/latest.md).

## 9 de septiembre de 2020

### Nuevas funciones

| Función | Descripción |
| --- | --- |
| Apoyo a LGPD (Brasil) | Ahora se pueden crear trabajos de privacidad bajo la [!DNL Lei Geral de Proteção de Dados] (LGPD). Estos trabajos se rastrean bajo el código de regulación `lgpd_bra`. |

## 8 de abril de 2020

### Nuevas funciones

| Función | Descripción |
| --- | --- |
| Compatibilidad con PDPA | [!DNL Privacy] Ahora se pueden crear solicitudes y realizar seguimientos de las mismas según la Ley de Protección de Datos Personales (PDPA) de Tailandia. Al realizar solicitudes de privacidad en la API, la variable `regulation` array acepta el valor &quot;pdpa_tha&quot;. |
| Tipos de área de nombres en la interfaz de usuario | Ahora puede especificar diferentes tipos de área de nombres en el Creador de solicitudes en el [!DNL Privacy Service] IU. Consulte la [guía del usuario](ui/user-guide.md) para obtener más información. |
| Desaprobación de punto final antiguo | El antiguo extremo de la API (`data/privacy/gdpr`) está en desuso. |

## 14 de enero de 2020

### Nuevas funciones

| Función | Descripción |
| --- | --- |
| [!DNL Privacy Service] cambio de marca | El anteriormente denominado &quot;Servicio de RGPD&quot; se ha cambiado a [!DNL Privacy Service] ya que el servicio ha crecido para admitir otras regulaciones además del RGPD. |
| Nuevos extremos de API | Ruta base para la variable [!DNL Privacy Service] La API se ha actualizado desde `/data/privacy/gdpr` a `/data/core/privacy/jobs` |
| Nuevo obligatorio `regulation` property | Al crear nuevos trabajos en el [!DNL Privacy Service] API, un `regulation` debe proporcionarse en la carga útil de la solicitud para indicar en qué regulación debe rastrearse el trabajo. Los valores aceptados son `gdpr` y `ccpa`. Consulte el documento en [trabajos de privacidad](api/privacy-jobs.md) en el [!DNL Privacy Service] Guía de API para obtener más información. |
| Compatibilidad con la autenticación de Adobe Primetime | [!DNL Privacy Service] ahora acepta solicitudes de acceso/eliminación de la autenticación de Adobe Primetime mediante `primetimeAuthentication` como su valor de producto. Consulte la [Documentación de autenticación de Primetime](https://tve.helpdocsonline.com/how-to-make-a-privacy-request) para obtener más información. |

### Mejoras

* [!DNL Privacy Service] Mejoras en la interfaz de usuario:
   * Separe las páginas de seguimiento de trabajos para las regulaciones del RGPD y la CCPA.
   * Nuevo *Tipo de regulación* para cambiar entre los datos de seguimiento del RGPD y la CCPA.

## 25 de julio de 2019

### Nuevas funciones

| Función | Descripción |
| --- | --- |
| Panel de métricas de solicitud | El nuevo panel de métricas de [!DNL Privacy Service] La interfaz de usuario proporciona visibilidad de las solicitudes de RGPD enviadas, erróneas y completadas. |
| Creador de solicitudes | Para prestar servicios a organizaciones con usuarios técnicos y no técnicos que envían solicitudes de RGPD, se ha añadido la funcionalidad &quot;Crear solicitud&quot; a la interfaz de usuario. La capacidad de envío de archivos JSON aún está disponible en el [!DNL Privacy Service] IU para las organizaciones que prefieran seguir usándola. |
| Notificaciones de eventos de trabajo del RGPD | Las notificaciones de eventos sobre los estados de trabajos del RGPD son un elemento crítico para muchos flujos de trabajo. Aunque las notificaciones se entregaron anteriormente mediante avisos de correo electrónico individuales, las notificaciones de eventos del RGPD son mensajes que aprovechan los eventos de Adobe I/O, que se envían a un enlace web configurado para facilitar la automatización de las solicitudes de trabajo. [!DNL Privacy Service] Los usuarios de la interfaz de usuario pueden suscribirse a los eventos del RGPD de Adobe I/O para recibir actualizaciones cuando se haya completado un producto o el trabajo del RGPD. |

## 18 de abril de 2019

### Mejoras

* Intervalo predeterminado para la tabla de estado en la variable [!DNL Privacy Service] La interfaz de usuario se ha modificado a un intervalo de 7 días.
* Mejor gestión de excepciones internas.
* Se ha mejorado el rendimiento al introducir el almacenamiento en caché para llamadas internas comunes con tasas de cambio de datos bajas.

### Correcciones de errores

* Se ha agregado la información de registro que faltaba para las consultas filtradas para la variable `GET /` en la variable [!DNL Privacy Service] API.

## 11 de abril de 2019

### Mejoras

* Se ha actualizado la interfaz de usuario para admitir nuevas funciones para los clientes de la versión beta
* Nuevas métricas API para admitir las funciones de la IU 2.0 en la versión beta

## 9 de abril de 2019

### Mejoras

* Se han actualizado todas las llamadas a la API de búsqueda (GET) de forma predeterminada a un intervalo retrospectivo de 30 días
* Uso restringido de API para tener un intervalo retroactivo máximo de 45 días

## 14 de febrero de 2019

### Mejoras

* Aplicar la variable `include` en cada envío de POST.
* Aplicar la variable `include` al cargar JSON.

### Correcciones de errores

* Se ha corregido un problema en el cual los clientes no podían cargar el [!DNL Privacy Service] IU.
