---
keywords: Experience Platform;inicio;temas populares;monitorizar cuentas;monitorizar flujos de datos;flujos de datos;destinos
description: Los destinos le permiten activar sus datos desde Adobe Experience Platform a innumerables socios externos. Este tutorial proporciona instrucciones sobre cómo monitorizar los flujos de datos de los destinos mediante la interfaz de usuario del Experience Platform.
solution: Experience Platform
title: Monitorizar flujos de datos para destinos en la interfaz de usuario
topic-legacy: overview
type: Tutorial
exl-id: 8eb7bb3c-f2dc-4dbc-9cf5-3d5d3224f5f1
source-git-commit: 1d40ef02bd0bdb48bb999c3308f78824f75e3459
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 0%

---

# Monitorización de flujos de datos para destinos en la interfaz de usuario

Los destinos le permiten activar sus datos desde Adobe Experience Platform a innumerables socios externos. Este tutorial proporciona instrucciones sobre cómo monitorizar los flujos de datos de los destinos mediante la interfaz de usuario del Experience Platform.

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

- [Destinos](../../destinations/home.md): Los destinos son integraciones prediseñadas con aplicaciones de uso común que permiten la activación perfecta de datos de Platform para campañas de marketing multicanal, campañas de correo electrónico, publicidad de destino y muchos otros casos de uso.
- [Simuladores para pruebas](../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

## Monitorizar flujos de datos

En el espacio de trabajo **[!UICONTROL Destinations]** dentro de la interfaz de usuario de Platform, vaya a la pestaña **[!UICONTROL Browse]** y seleccione el nombre de un destino que desea ver.

![](../assets/ui/monitor-destinations/select-destination.png)

Aparecerá una lista de flujos de datos existentes. En esta página hay una lista de flujos de datos visibles, que incluye información sobre su destino, nombre de usuario, número de flujos de datos y estado.

Consulte la siguiente tabla para obtener más información sobre los estados:

| Estado | Descripción |
| ------ | ----------- |
| Habilitado | El estado `Enabled` indica que un flujo de datos está activo y que está incorporando datos según la programación que se proporcionó. |
| Desactivado | El estado `Disabled` indica que un flujo de datos está inactivo y no está incorporando ningún dato. |
| Procesamiento | El estado `Processing` indica que un flujo de datos aún no está activo. Este estado se encuentra a menudo inmediatamente después de crear un nuevo flujo de datos. |
| Error | El estado `Error` indica que se ha interrumpido el proceso de activación de un flujo de datos. |

## El flujo de datos se ejecuta en los destinos de flujo continuo

Para los destinos de flujo continuo, la pestaña [!UICONTROL Dataflow run] proporciona una actualización horaria para los datos de métricas en las ejecuciones de flujo de datos. Las estadísticas más destacadas etiquetadas son para identidades.

Las identidades representan las diferentes facetas de un perfil. Por ejemplo, si un perfil contiene un número de teléfono y una dirección de correo electrónico, ese perfil tendrá dos identidades.

Se muestra una lista de ejecuciones individuales y sus métricas particulares, junto con los siguientes totales de identidades:

- **[!UICONTROL Identidades activadas]**: Recuento total de identidades de perfil creadas o actualizadas para la activación.
- **[!UICONTROL Identidades excluidas]**: Número total de identidades de perfil que se omiten para la activación en función de atributos que faltan y de la infracción de consentimiento.
- **[!UICONTROL Identidades fallidas]**: Número total de identidades de perfil que no se activan en el destino debido a errores.

![](../assets/ui/monitor-destinations/dataflow-runs-stream.png)

Cada ejecución de flujo de datos individual muestra los siguientes detalles:

- **[!UICONTROL Inicio]** de la ejecución del flujo de datos: Hora a la que comenzó la ejecución del flujo de datos.
- **[!UICONTROL Tiempo]** de procesamiento: Cantidad de tiempo que tardó el flujo de datos en procesarse.
- **[!UICONTROL Perfiles recibidos]**: Número total de perfiles recibidos en el flujo de datos.
- **[!UICONTROL Identidades activadas]**: El número total de identidades de perfil que se activaron correctamente en el destino seleccionado.
- **[!UICONTROL Identidades excluidas]**: El número total de identidades de perfil que se excluyen para la activación en función de atributos que faltan y la infracción de consentimiento.
- **[!UICONTROL Identidades]** fallidasEl número total de identidades de perfil que no se activan en el destino debido a errores.
- **[!UICONTROL Tasa]** de activación: El porcentaje de identidades recibidas que se han activado o omitido correctamente. La fórmula siguiente muestra cómo se calcula este valor:
   ![](../assets/ui/monitor-destinations/activation-rate-formula.png)
- **[!UICONTROL Estado]**: Representa el estado en el que se encuentra el flujo de datos:   Completada o  [!UICONTROL Procesamiento].  Completada significa que todas las identidades de la ejecución de flujo de datos correspondiente se incorporaron en el período de una hora.  Procesamiento significa que la ejecución del flujo de datos aún no ha finalizado.

Para ver los detalles de una ejecución de flujo de datos determinada, seleccione la hora de inicio de la ejecución en la lista.

La página de detalles de una ejecución de flujo de datos contiene información adicional como el número de perfiles recibidos, el número de identidades activadas, el número de identidades fallidas y el número de identidades excluidas.

![](../assets/ui/monitor-destinations/dataflow-details-stream.png)

La página de detalles también muestra una lista de identidades que han fallado y las identidades que se excluyeron. Se muestra información sobre las identidades fallidas y excluidas, incluido el código de error, el recuento de identidades y la descripción. De forma predeterminada, la lista muestra las identidades con errores. Para mostrar las identidades omitidas, seleccione la opción **[!UICONTROL Identities excluded]** .

![](../assets/ui/monitor-destinations/dataflow-records-stream.png)

## El flujo de datos se ejecuta en destinos por lotes

Para los destinos por lotes, la pestaña [!UICONTROL Dataflow run] proporciona datos de métricas sobre las ejecuciones del flujo de datos. Se muestra una lista de ejecuciones individuales y sus métricas particulares, junto con los siguientes totales de identidades:

- **[!UICONTROL Identidades activadas]**: Recuento de identidades de perfil individuales activadas correctamente en el destino seleccionado.
- **[!UICONTROL Identidades excluidas]**: Recuento de identidades de perfil individuales excluidas para la activación para el destino seleccionado, en función de atributos que faltan y de la infracción de consentimiento.

![](../assets/ui/monitor-destinations/dataflow-runs-batch.png)

Cada ejecución de flujo de datos individual muestra los siguientes detalles:

- **[!UICONTROL Inicio]** de la ejecución del flujo de datos: Hora a la que comenzó la ejecución del flujo de datos.
- **[!UICONTROL Tiempo]** de procesamiento: Cantidad de tiempo que tardó la ejecución del flujo de datos en procesarse.
- **[!UICONTROL Perfiles recibidos]**: Número total de perfiles recibidos en el flujo de datos. Este valor se actualiza cada 60 minutos.
- **[!UICONTROL Identidades activadas]**: El número total de identidades de perfil que se activaron correctamente en el destino seleccionado.
- **[!UICONTROL Identidades excluidas]**: El número total de identidades de perfil que se excluyen para la activación en función de atributos que faltan y la infracción de consentimiento.
- **[!UICONTROL Estado]**: Representa el estado en el que se encuentra el flujo de datos. Puede ser uno de los tres estados: [!UICONTROL Success], [!UICONTROL Failed] y [!UICONTROL Processing].  Correcto significa que el flujo de datos está activo y que está incorporando datos según la programación proporcionada.  Fallido significa que la activación de datos se ha suspendido debido a errores.  Procesamiento significa que el flujo de datos aún no está activo y se encuentra generalmente cuando se crea un nuevo flujo de datos.

Para ver los detalles de una ejecución de flujo de datos específica, seleccione la hora de inicio de la ejecución en la lista.

>[!NOTE]
>
>Las ejecuciones de flujo de datos se generan en función de la frecuencia de programación del flujo de datos de destino. Se realiza una ejecución de flujo de datos independiente para cada política de combinación aplicada a un segmento.

La página de detalles de un flujo de datos, además de los detalles mostrados en la lista de flujos de datos, muestra información más específica sobre el flujo de datos:

- **[!UICONTROL Tamaño de los datos]**: El tamaño del flujo de datos que se está incorporando.
- **[!UICONTROL Total de archivos]**: El número total de archivos introducidos en el flujo de datos.
- **[!UICONTROL Última actualización]**: La última vez que se actualizó la ejecución del flujo de datos.

![](../assets/ui/monitor-destinations/dataflow-batch.png)

La página de detalles también muestra una lista de identidades que han fallado y las identidades que se excluyeron. Se muestra información sobre las identidades fallidas y excluidas, incluido el código de error y la descripción. De forma predeterminada, la lista muestra las identidades con errores. Para mostrar las identidades excluidas, seleccione la opción **[!UICONTROL Identities excluded]** .

![](../assets/ui/monitor-destinations/dataflow-records-batch.png)


## Pasos siguientes

Al seguir esta guía, ahora sabe cómo monitorizar los flujos de datos tanto para los destinos de lote como de flujo continuo, incluida toda la información relevante, como el tiempo de procesamiento, la tasa de activación y el estado. Para obtener más información sobre los flujos de datos en Platform, lea la [descripción general de los flujos de datos](../home.md). Para obtener más información sobre los destinos, lea la [información general sobre destinos](../../destinations/home.md).