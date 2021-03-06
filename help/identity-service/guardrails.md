---
keywords: Experience Platform;identidad;servicio de identidad;solución de problemas;protecciones;directrices;límite;
title: Seguridad para el servicio de identidad
description: Este documento proporciona información sobre el uso y los límites de velocidad de los datos del servicio de identidad para ayudarle a optimizar el uso del gráfico de identidad.
exl-id: bd86d8bf-53fd-4d76-ad01-da473a1999ab
source-git-commit: b07a45e5bb9cae6e147ea790ebb77cb63f8790c1
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 3%

---

# Seguridad para [!DNL Identity Service] data

Este documento proporciona información sobre el uso y los límites de velocidad para [!DNL Identity Service] para optimizar el uso del gráfico de identidad. Al revisar las siguientes barreras, se da por hecho que ha modelado los datos correctamente. Si tiene alguna pregunta sobre cómo modelar sus datos, póngase en contacto con su representante de servicio al cliente.

## Primeros pasos

Los siguientes servicios de Experience Platform participan en el modelado de datos de identidad:

* [Identidades](home.md): Puente identidades de fuentes de datos dispares a medida que se incorporan en Platform.
* [[!DNL Real-time Customer Profile]](../profile/home.md): Cree perfiles de cliente unificados con datos de varias fuentes.

## Límites del modelo de datos

Las tablas siguientes proporcionan directrices sobre protecciones para límites estáticos, así como reglas de validación que se deben tener en cuenta para áreas de nombres de identidad.

### Límites estáticos

La siguiente tabla describe los límites estáticos aplicados a los datos de identidad.

| Seguridad | Límite | Notas |
| --- | --- | --- |
| Número de identidades en un gráfico | 150 | El límite se aplica en el nivel de entorno limitado. El gráfico de identidad no se actualiza una vez que se alcance el límite. |
| Número de identidades en un registro XDM | 20 | El número mínimo de registros XDM necesarios es de dos. |
| Número de áreas de nombres personalizadas | Ninguna | No hay límites en el número de áreas de nombres personalizadas que puede crear. |
| Número de gráficos | Ninguna | No hay límites en el número de gráficos de identidad que puede crear. |
| Número de caracteres de un nombre para mostrar o símbolo de identidad de un espacio de nombres | Ninguna | No hay límites en el número de caracteres de un nombre para mostrar o símbolo de identidad de un espacio de nombres. |

### Validación del valor de identidad

La siguiente tabla describe las reglas existentes que debe seguir para garantizar una validación correcta del valor de identidad.

| Área de nombres | Regla de validación | Comportamiento del sistema cuando se infringe la regla |
| --- | --- | --- |
| ECID | <ul><li>El valor de identidad de un ECID debe tener exactamente 38 caracteres.</li><li>El valor de identidad de un ECID debe constar únicamente de números.</li></ul> | <ul><li>Si el valor de identidad de ECID no es exactamente de 38 caracteres, se omite el registro.</li><li>Si el valor de identidad de ECID contiene caracteres no numéricos, se omite el registro.</li></ul> |
| No ECID | El valor de identidad no puede superar los 1024 caracteres. | Si el valor de identidad supera los 1024 caracteres, se omitirá el registro. |

## Pasos siguientes

Consulte la siguiente documentación para obtener más información sobre [!DNL Identity Service]:

* [Información general del [!DNL Identity Service]](home.md)
* [Visor de gráficos de identidad](ui/identity-graph-viewer.md)
