---
title: onBeforeLinkClickSend
description: Llamada de retorno que se ejecuta justo antes de que se envíen los datos de seguimiento de vínculos.
exl-id: 8c73cb25-2648-4cf7-b160-3d06aecde9b4
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# `onBeforeLinkClickSend`

>[!IMPORTANT]
>
>Esta llamada de retorno está obsoleta. Utilice [`clickCollection.filterClickDetails`](clickcollection.md) en su lugar.

La llamada de retorno `onBeforeLinkClickSend` le permite registrar una función de JavaScript que puede alterar los datos de seguimiento de vínculos que envía justo antes de que dichos datos se envíen a Adobe. Permite manipular el objeto `xdm` o `data`, incluida la capacidad de agregar, editar o quitar elementos. También puede cancelar de forma condicional el envío de datos, por ejemplo, con el tráfico de bots del lado del cliente detectado.

Esta devolución de llamada solo se ejecuta si [`clickCollectionEnabled`](clickcollectionenabled.md) está habilitado y `filterClickDetails` no contiene una función registrada.

Si [`onBeforeEventSend`](onbeforeeventsend.md) y `onBeforeLinkClickSend` contienen funciones registradas, `onBeforeLinkClickSend` se ejecuta primero.

>[!WARNING]
>
>Esta llamada de retorno permite el uso de código personalizado. Si algún código que incluya en la llamada de retorno genera una excepción no detectada, se detendrá el procesamiento del evento. Los datos no se envían a Adobe.

## `onBeforeLinkClickSend` y `filterClickDetails`

La llamada de retorno [`clickCollection.filterClickDetails`](clickcollection.md) está diseñada para reemplazar a `onBeforeLinkClickSend`. Adobe recomienda encarecidamente no asignar funciones de devolución de llamada a ambas simultáneamente. Si asigna una función de devolución de llamada tanto a `filterClickDetails` como a `onBeforeLinkClickSend`, la biblioteca utilizará la siguiente lógica:

* Solo `filterClickDetails` se ejecuta; `onBeforeLinkClickSend` no.
* La agrupación de eventos `clickCollection.eventGroupingEnabled` no funciona.
