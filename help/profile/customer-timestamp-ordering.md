---
title: Solicitud de marca horaria del cliente
description: Aprenda a añadir el orden de marcas de hora de los clientes a sus conjuntos de datos para garantizar la coherencia en los datos de perfil.
badgePrivateBeta: label="Beta privada" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: c5789b872be49c3bd4a1ca61a2d44392ebd4a746
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---


# Solicitud de marca de tiempo del cliente

En Adobe Experience Platform, el orden de los datos no se garantiza automáticamente al ingerir datos mediante la transmisión al almacén de perfiles. Al solicitar la marca de tiempo del cliente, puede garantizar que el mensaje más reciente, según la marca de tiempo del cliente proporcionada, se conservará en el almacén de perfiles. Como resultado, esto permite que los datos de perfil sean coherentes y que permanezcan sincronizados con los sistemas de origen.

Para habilitar la solicitud de marca de hora del cliente, deberá utilizar la variable `lastUpdatedDate` dentro del campo [Tipo de datos Atributos de auditoría del sistema de origen externo](../xdm/data-types/external-source-system-audit-attributes.md) y póngase en contacto con el administrador de cuentas técnico de Adobe o con el servicio de atención al cliente de Adobe con su información de zona protegida y conjunto de datos.

## Restricciones

Durante esta versión beta privada, se aplican las siguientes restricciones al utilizar la ordenación de marcas de tiempo del cliente:

- Solo puede utilizar la solicitud de marca de hora del cliente con **atributos de perfil** ingerido con **ingesta por streaming**.
- Solo puede utilizar la solicitud de marca de hora del cliente en **no producción** zonas protegidas.
- Solo puede aplicar pedidos de marca de hora de cliente a **5** conjuntos de datos por zona protegida.
- El `lastUpdatedDate` el campo debe estar en [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) formato.
- Todas las filas de datos introducidas **debe** contener el `lastUpdatedDate` field. Si falta este campo o tiene un formato incorrecto, la ingesta fallará.
- Cualquier conjunto de datos habilitado para el pedido de marcas de tiempo de clientes **debe** ser un nuevo conjunto de datos sin ningún dato introducido anteriormente.
- Para cualquier fragmento de perfil determinado, solo las filas que contienen un `lastUpdatedDate` se incorporarán. Si la fila no contiene un más reciente `lastUpdatedDate`, la fila se descartará.

## Recomendaciones 

Al implementar la solicitud de marca de hora del cliente, tenga en cuenta las siguientes consideraciones:

- Usted es responsable de sincronizar los relojes en todos los sistemas internos que envían datos al almacén de perfiles.
- Debe tener una precisión de milisegundos en las marcas de tiempo con formato ISO 8061.
- El uso de la preparación de datos en coordinación con el pedido de marcas de tiempo del cliente es **muy recomendable**, al mismo tiempo crea una copia de todas las filas ingeridas junto con sus marcas de tiempo, lo que permite una mejor depuración en caso de que surjan problemas.
