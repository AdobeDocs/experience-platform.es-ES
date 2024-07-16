---
title: Solicitud de marca horaria del cliente
description: Aprenda a añadir el orden de marcas de hora de los clientes a sus conjuntos de datos para garantizar la coherencia en los datos de perfil.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 1cd9f0b5-6334-4815-860a-78596a9cea1a
source-git-commit: 57d42d88ec9a93744450a2a352590ab57d9e5bb7
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Solicitud de marca de tiempo del cliente

En Adobe Experience Platform, el orden de los datos no se garantiza de forma predeterminada al ingerir datos mediante la transmisión de flujo continuo al almacén de perfiles. Al solicitar la marca de tiempo del cliente, puede garantizar que el mensaje más reciente, según la marca de tiempo del cliente proporcionada, se conservará en el almacén de perfiles. Se quitarán todos los mensajes antiguos y **no** estarán disponibles para su uso en servicios posteriores que usen datos de perfil como segmentación y destinos. Como resultado, esto permite que los datos de perfil sean coherentes y que permanezcan sincronizados con los sistemas de origen.

Para habilitar la ordenación de marcas de hora de clientes, use el campo `extSourceSystemAudit.lastUpdatedDate` en el grupo de campos [Atributos de auditoría del sistema de Source externo](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/shared/external-source-system-audit-details.schema.md) y póngase en contacto con el administrador de cuentas técnico de Adobe o con el servicio de atención al cliente de Adobe con la información de la zona protegida y el conjunto de datos.

## Restricciones

Durante esta versión beta privada, se aplican las siguientes restricciones al utilizar la ordenación de marcas de tiempo del cliente:

- Solo puede usar la ordenación de marcas de hora de clientes con **atributos de perfil** ingeridos con **ingesta de transmisión** en el almacén de perfiles.
   - Se han proporcionado **no** garantías de pedido para los datos en el lago de datos o servicio de identidad.
- Solo puede usar la ordenación de marcas de hora del cliente en **zonas protegidas que no sean de producción**.
- Solo puede aplicar el orden de marcas de hora de cliente a **5** conjuntos de datos por zona protegida.
- Usted **no puede** usar actualizaciones de flujo continuo para enviar actualizaciones de fila parciales en un conjunto de datos que tenga habilitada la ordenación de marcas de tiempo de clientes.
- El campo `extSourceSystemAudit.lastUpdatedDate` **debe** tener el formato [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html). Al usar el formato ISO 8601, **debe** ser como una fecha y hora completas con el formato `yyyy-MM-ddTHH:mm:ss.sssZ` (por ejemplo, `2028-11-13T15:06:49.001Z`).
- Todas las filas de datos ingeridos **deben** contener el campo `extSourceSystemAudit.lastUpdatedDate` como un grupo de campos de nivel superior. Esto significa que este campo **no debe** estar anidado en el esquema XDM. Si falta este campo o tiene un formato incorrecto, se ingestará el registro con formato incorrecto **no** y se enviará el mensaje de error correspondiente.
- Cualquier conjunto de datos habilitado para el pedido de marcas de tiempo de clientes **debe** ser un nuevo conjunto de datos sin ningún dato ingerido anteriormente.
- Para cualquier fragmento de perfil determinado, solo se incorporarán las filas que contengan un(a) `extSourceSystemAudit.lastUpdatedDate` más reciente. Se descartarán las filas que contengan un(a) `extSourceSystemAudit.lastUpdatedDate` que sea anterior o de la misma edad.

## Recomendaciones

Al implementar la solicitud de marca de hora del cliente, tenga en cuenta las siguientes consideraciones:

- Usted es responsable de sincronizar los relojes en todos los sistemas internos que envían datos al almacén de perfiles.
- Debe tener una precisión de milisegundos en las marcas de tiempo con formato ISO 8061.
