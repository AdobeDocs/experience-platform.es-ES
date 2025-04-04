---
keywords: Experience Platform;inicio;temas populares;Conector de Audience Manager;Audience Manager;Audience Manager
solution: Experience Platform
title: Información general sobre Audience Manager Source
description: La fuente de Adobe Audience Manager transmite datos de origen recopilados en Audience Manager a Adobe Experience Platform.
exl-id: be90db33-69e1-4f42-9d1a-4f8f26405f0f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1137'
ht-degree: 1%

---

# fuente de Audience Manager

>[!IMPORTANT]
>
>En la configuración inicial, el origen de Adobe Audience Manager devuelve un mensaje de error que indica que no existe un área de nombres de identidad con un `namespaceCode={VALUE}` determinado. **Nota**: en el back-end, `namespaceCode` se usa para hacer referencia al símbolo de identidad. Para completar la integración, debe:
>
>- [Crear un área de nombres personalizada en el servicio de identidad](../../../identity-service/features/namespaces.md#create-custom-namespaces) con el símbolo de identidad especificado (`VALUE`)
>- Vuelva a introducir los datos.

La fuente de Adobe Audience Manager transmite datos de origen recopilados en Adobe Audience Manager para su activación en Adobe Experience Platform. La fuente de Audience Manager introduce dos tipos de datos en Experience Platform:

- **Datos en tiempo real:** Datos capturados en tiempo real en el servidor de recopilación de datos de Audience Manager. Estos datos se utilizan en Audience Manager para rellenar rasgos basados en reglas y aparecerán en Experience Platform en el tiempo de latencia más corto.
- **Datos de perfil:** Audience Manager usa datos incorporados y en tiempo real para derivar perfiles de clientes. Estos perfiles se utilizan para rellenar gráficos de identidad y rasgos en las realizaciones de segmentos.

La fuente de Audience Manager asigna estos tipos de datos a un esquema del Modelo de datos de experiencia (XDM) y, a continuación, los envía a Experience Platform. Los datos en tiempo real se envían como datos de ExperienceEvent de XDM, mientras que los datos de perfil se envían como datos de perfil individuales de XDM.

Para obtener más información, lea la guía sobre [creación de una conexión de origen de Audience Manager en la interfaz de usuario](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## ¿Qué es el modelo de datos de experiencia (XDM)?

XDM es una especificación documentada públicamente que proporciona un marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.

El cumplimiento de los estándares XDM permite que los datos de experiencia del cliente se incorporen de forma uniforme, lo que facilita la entrega de datos y la recopilación de información.

Para obtener más información sobre cómo se utiliza XDM en Experience Platform, lea la [descripción general del sistema XDM](../../../xdm/home.md). Para obtener más información sobre cómo se estructuran los esquemas XDM entre perfiles y eventos, lea los [conceptos básicos de la composición de esquemas](../../../xdm/schema/composition.md).

## Ejemplos de esquemas XDM

A continuación, se muestran ejemplos de la estructura de Audience Manager asignada a ExperienceEvent y a Perfil individual de XDM en Experience Platform.

### ExperienceEvent: para datos en tiempo real e incorporados

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### Perfil individual de XDM: para datos de perfil

![](images/aam-profile-xdm-for-profile-data.png)

Para obtener información sobre cómo se asignan los campos de Audience Manager a XDM, lea la documentación sobre [campos de asignación de Audience Manager](./mapping/audience-manager.md).

## Administración de datos en Experience Platform

### Conjuntos de datos

Un conjunto de datos es una construcción de almacenamiento y administración para una colección de datos, normalmente una tabla, que contiene un esquema (columnas) y campos (filas) y está disponible mediante una conexión de datos. Los datos de Audience Manager constan de datos en tiempo real, datos de entrada y datos de perfil. Para localizar los conjuntos de datos de Audience Manager, utilice la función de búsqueda de la interfaz de usuario con las convenciones de nomenclatura proporcionadas para cada tipo de datos.

Los conjuntos de datos de Audience Manager están deshabilitados para el perfil de forma predeterminada y los usuarios tienen la capacidad de habilitar o deshabilitar conjuntos de datos en función de sus casos de uso. No se recomienda deshabilitar los conjuntos de datos que se utilizarán para la pertenencia de segmentos al perfil.

>[!NOTE]
>
>AAM Real-time es el único conjunto de datos que va al lago de datos. Todos los demás conjuntos de datos de Audience Manager se dirigen a [!DNL Profile], si están habilitados para [!DNL Profile]. Si no están habilitados para [!DNL Profile], no recibirán ningún dato y se mostrarán como vacíos.

| Nombre del conjunto de datos | Descripción | Clase |
| --- | --- | --- |
| AAM Real-time | Este conjunto de datos contiene datos recopilados por visitas individuales directas en puntos finales de Audience Manager DCS y mapas de identidad para perfiles de Audience Manager. Mantenga este conjunto de datos habilitado para la ingesta de perfiles. | Evento de experiencia |
| Actualizaciones de perfil en tiempo real de AAM | Este conjunto de datos permite la segmentación en tiempo real de rasgos y segmentos de Audience Manager. Incluye información sobre el enrutamiento regional, las características y la pertenencia a segmentos de Edge. Mantenga este conjunto de datos habilitado para la ingesta de perfiles. Los datos no son visibles como lotes en el conjunto de datos. Puede habilitar la opción **[!UICONTROL Perfil]** para ingerir directamente los datos en el perfil. | Registro |
| Datos de dispositivos AAM | Datos del dispositivo con ECID y las correspondientes realizaciones de segmentos acumuladas en Audience Manager. Los datos no son visibles como lotes en el conjunto de datos. Puede habilitar la opción **[!UICONTROL Perfil]** para ingerir directamente los datos en el perfil. | Registro |
| Datos de perfil de dispositivo de AAM | Se utiliza para los diagnósticos del conector Audience Manager. Los datos no son visibles como lotes en el conjunto de datos. Puede habilitar la opción **[!UICONTROL Perfil]** para ingerir directamente los datos en el perfil. | Registro |
| Perfiles autenticados de AAM | Este conjunto de datos contiene perfiles autenticados de Audience Manager. Los datos no son visibles como lotes en el conjunto de datos. Puede habilitar la opción **[!UICONTROL Perfil]** para ingerir directamente los datos en el perfil. | Registro |
| Metadatos de perfiles autenticados de AAM | Se utiliza para los diagnósticos del conector de Audience Manager. Los datos no son visibles como lotes en el conjunto de datos. Puede habilitar la opción **[!UICONTROL Perfil]** para ingerir directamente los datos en el perfil. | Registro |
| Relleno de datos de dispositivos AAM | El conjunto de datos no trae datos de dispositivos anteriores. Contiene ECID y las realizaciones de segmentos correspondientes agregadas en Audience Manager. Los datos no son visibles como lotes en el conjunto de datos. Puede habilitar la opción **[!UICONTROL Perfil]** para ingerir directamente los datos en el perfil. | Registro |
| Relleno de perfiles autenticados de AAM | Que el conjunto de datos traiga datos autenticados en el pasado. Contiene perfiles autenticados de Audience Manager. Los datos no son visibles como lotes en el conjunto de datos. Puede habilitar la opción **[!UICONTROL Perfil]** para ingerir directamente los datos en el perfil. | Registro |

### Conexiones

Adobe Audience Manager crea una conexión en el catálogo: Conexión de Audience Manager. El catálogo es el sistema de registros para la ubicación y el linaje de los datos dentro de Adobe Experience Platform. Una conexión es un objeto Catalog que es una instancia de conectores específica del cliente. Lea la [descripción general del servicio de catálogo](../../../catalog/home.md) para obtener más información sobre el catálogo, las conexiones y los conectores.

### Población de segmentos a impacto de perfil

Los tamaños de población de segmentos tienen un impacto directo en los números de perfil al enviar por primera vez un segmento de Audience Manager a Experience Platform. Esto significa que la selección de todos los segmentos puede causar sobrecargas de perfil que superen el derecho de uso de licencia. Experience Platform también distingue los nuevos datos de los datos históricos para la ingesta de perfiles. Un segmento con 100 identidades basadas en origen creará 100 perfiles. Sin embargo, si la población de ese mismo segmento se elevó a 150 y se ingirió en Experience Platform, el número de perfiles solo aumentará en 50, ya que solo hay 50 perfiles nuevos.

También puede comprobar el uso del perfil que tiene disponible su cuenta a través de [Tablero de uso de licencias](../../../dashboards/guides/license-usage.md).

## ¿Cuál es la latencia esperada para los datos de Audience Manager en Experience Platform?

| Datos de Audience Manager | Tipo | Latencia | Notas |
| --- | --- | --- | --- |
| Datos en tiempo real | Eventos | &lt;25 minutos | Tiempo que transcurre desde que se captura en el nodo Edge de Audience Manager hasta que aparece en el lago de datos. |
| Datos en tiempo real | Actualizaciones de perfil | &lt;10 minutos | Hora de aterrizar en el Perfil del cliente en tiempo real. |
| Datos en tiempo real e incorporados | Actualizaciones de perfil | de 24 a 36 horas | El tiempo transcurre desde que se captura mediante datos de Edge DCS/PCS e incorporados, se procesa en un perfil de usuario y, a continuación, aparece en el Perfil del cliente en tiempo real. Actualmente, estos datos no aterrizan directamente en el lago de datos. Se puede habilitar la opción de perfil para los conjuntos de datos de perfil de Audience Manager para introducir estos datos directamente en el perfil del cliente en tiempo real. |
