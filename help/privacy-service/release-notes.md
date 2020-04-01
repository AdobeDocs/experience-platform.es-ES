---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Notas de la versión de Privacy Service
topic: release notes
translation-type: tm+mt
source-git-commit: d7aa1b4e3e697a504964d6eb485f536065c6718a

---


# Notas de la versión de Privacy Service

Este documento contiene información sobre las nuevas funciones de Adobe Experience Platform Privacy Service, así como mejoras y correcciones de errores importantes.

## 14 de enero de 2020

### Nuevas funciones

| Función | Descripción |
--- | ---
| Cambio de marca de Privacy Service | El llamado anteriormente &quot;Servicio de RGPD&quot; ha sido rebautizado como Servicio de Privacidad ya que el servicio ha crecido para apoyar otras regulaciones además del RGPD. |
| Nuevos extremos de API | La ruta de acceso base para la API de Privacy Service se ha actualizado de `/data/privacy/gdpr` a `/data/core/privacy/jobs` |
| Nueva propiedad requerida `regulation` | Al crear nuevos trabajos en la API de Privacy Service, se debe proporcionar una `regulation` propiedad en la carga útil de la solicitud para indicar en qué regla se debe realizar el seguimiento del trabajo. Los valores aceptados son `gdpr` y `ccpa`. Consulte el documento sobre trabajos [de](api/privacy-jobs.md) privacidad en la guía para desarrolladores de Privacy Service para obtener más información. |
| Compatibilidad con la autenticación Adobe Primetime | Privacy Service ahora acepta solicitudes de acceso/eliminación de la autenticación Adobe Primetime, utilizando `primetimeAuthentication` como valor de producto. See the [Primetime Authentication documentation](http://tve.helpdocsonline.com/how-to-make-a-privacy-request) for more information. |

### Mejoras

* Mejoras en la interfaz de usuario de Privacy Service:
   * Páginas de seguimiento de trabajos independientes para las regulaciones de RGPD y CCPA.
   * Nuevo menú desplegable _de tipo_ de reglamento para cambiar entre los datos de seguimiento del RGPD y del CCPA.

## 25 de julio de 2019

### Nuevas funciones

| Función | Descripción |
--- | ---
| Panel de las métricas de solicitud | El nuevo panel de métricas en la interfaz de usuario de Privacy Service proporciona visibilidad de las solicitudes GDPR enviadas, erróneas y completadas. |
| Generador de solicitudes | Para prestar servicios a organizaciones con usuarios técnicos y no técnicos que envían solicitudes de RGPD, se ha agregado la funcionalidad &quot;Crear solicitud&quot; a la interfaz de usuario. La capacidad de envío de archivos JSON aún está disponible en la interfaz de usuario de Privacy Service para las organizaciones que prefieran seguir usándola. |
| Notificaciones de Evento de trabajos de RGPD | Las notificaciones de Evento sobre los estados de trabajos del RGPD son un elemento crítico para muchos flujos de trabajo. Aunque las notificaciones se enviaban anteriormente mediante avisos de correo electrónico individuales, las notificaciones de evento de GDPR son mensajes que aprovechan los eventos de Adobe I/O, que se envían a un enlace web configurado para facilitar la automatización de las solicitudes de trabajo. Los usuarios de la interfaz de usuario de Privacy Service pueden suscribirse a los eventos GDPR de Adobe I/O para recibir actualizaciones cuando se haya completado un producto o el trabajo GDPR. |

## 18 de abril de 2019

### Mejoras

* Intervalo predeterminado para la tabla de estado en la interfaz de usuario de Privacy Service modificado a un intervalo de 7 días.
* Mejor gestión de excepciones internas.
* Se ha mejorado el rendimiento al introducir el almacenamiento en caché para llamadas internas comunes con bajas tasas de cambio de datos.

### Correcciones de errores

* Se Añadió la información de registro que faltaba para las consultas filtradas del extremo en la API de Privacy Service `GET /` .

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

* Aplique el `include` campo en cada envío POST.
* Aplicar el `include` campo al cargar JSON.

### Correcciones de errores

* Se corrigió un problema en el cual los clientes no podían cargar la interfaz de usuario de Privacy Service.