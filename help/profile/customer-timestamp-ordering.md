---
title: Solicitud de marca horaria del cliente
description: Aprenda a añadir el orden de marcas de hora de los clientes a sus conjuntos de datos para garantizar la coherencia en los datos de perfil.
badgePrivateBeta: label="Beta privada" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: f73b7ac38c681ec5161e2b5e7075f31946a6563e
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---


# Solicitud de marca de tiempo del cliente

En Adobe Experience Platform, el orden de los datos no se garantiza de forma predeterminada al ingerir datos mediante la transmisión de flujo continuo al almacén de perfiles. Al solicitar la marca de tiempo del cliente, puede garantizar que el mensaje más reciente, según la marca de tiempo del cliente proporcionada, se conservará en el almacén de perfiles. A continuación, se perderán todos los mensajes antiguos y **no** estar disponible para su uso en servicios descendentes que utilicen datos de perfil como la segmentación y los destinos. Como resultado, esto permite que los datos de perfil sean coherentes y que permanezcan sincronizados con los sistemas de origen.

Para habilitar la solicitud de marcas de hora de cliente, use `extSourceSystemAudit.lastUpdatedDate` dentro del campo [Tipo de datos Atributos de auditoría del sistema de origen externo](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/shared/external-source-system-audit-details.schema.md) y póngase en contacto con el administrador de cuentas técnico de Adobe o con el servicio de atención al cliente de Adobe con su información de zona protegida y conjunto de datos.

## Restricciones

Durante esta versión beta privada, se aplican las siguientes restricciones al utilizar la ordenación de marcas de tiempo del cliente:

- Solo puede utilizar la solicitud de marca de hora del cliente con **atributos de perfil** ingerido con **ingesta por streaming** en el almacén de perfiles.
   - No hay **no** Garantías de pedido previstas para los datos en el lago de datos o el servicio de identidad.
- Solo puede utilizar la solicitud de marca de hora del cliente en **no producción** zonas protegidas.
- Solo puede aplicar pedidos de marca de hora de cliente a **5** conjuntos de datos por zona protegida.
- Usted **no puede** utilice actualizaciones de flujo continuo para enviar actualizaciones de fila parciales en un conjunto de datos que tenga habilitada la ordenación de marcas de tiempo de clientes.
- El `extSourceSystemAudit.lastUpdatedDate` campo **debe** estar en el [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) formato. Cuando se utiliza el formato ISO 8601, es **debe** ser como una fecha y hora completas con el formato `yyyy-MM-ddTHH:mm:ss.sssZ` (por ejemplo, `2028-11-13T15:06:49.001Z`).
- Todas las filas de datos introducidas **debe** contener el `extSourceSystemAudit.lastUpdatedDate` como un grupo de campos de nivel superior. Esto significa que este campo **debe** no se puede anidar dentro del esquema XDM. Si falta este campo o tiene un formato incorrecto, el registro con formato incorrecto **no** y se enviará un mensaje de error correspondiente.
- Cualquier conjunto de datos habilitado para el pedido de marcas de tiempo de clientes **debe** ser un nuevo conjunto de datos sin ningún dato introducido anteriormente.
- Para cualquier fragmento de perfil determinado, solo las filas que contienen un `extSourceSystemAudit.lastUpdatedDate` se incorporarán. Filas que contienen un `extSourceSystemAudit.lastUpdatedDate` que sea mayor o de la misma edad se descartará.

## Recomendaciones 

Al implementar la solicitud de marca de hora del cliente, tenga en cuenta las siguientes consideraciones:

- Usted es responsable de sincronizar los relojes en todos los sistemas internos que envían datos al almacén de perfiles.
- Debe tener una precisión de milisegundos en las marcas de tiempo con formato ISO 8061.
