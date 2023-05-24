---
keywords: Experience Platform;identidad;servicio de identidad;resolución de problemas;protecciones;directrices;límite;
title: Protecciones del servicio de identidad
description: Este documento proporciona información sobre los límites de uso y tasa de los datos del servicio de identidad para ayudarle a optimizar su uso del gráfico de identidad.
exl-id: bd86d8bf-53fd-4d76-ad01-da473a1999ab
source-git-commit: f619bbf2c8d313eabc6444b4bd8c09615a00cc42
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 2%

---

# Protecciones para [!DNL Identity Service] datos

Este documento proporciona información sobre los límites de uso y tasa para [!DNL Identity Service] datos para ayudarle a optimizar el uso del gráfico de identidad. Al revisar las siguientes protecciones, se da por hecho que los datos se han modelado correctamente. Si tiene preguntas sobre cómo modelar los datos, póngase en contacto con su representante de servicio de atención al cliente.

## Primeros pasos

Los siguientes servicios de Experience Platform participan en el modelado de datos de identidad:

* [Identidades](home.md): vincule identidades de fuentes de datos dispares a medida que se incorporan en Platform.
* [[!DNL Real-Time Customer Profile]](../profile/home.md): cree perfiles de consumidor unificados con datos de varias fuentes.

## Límites del modelo de datos

Las tablas siguientes proporcionan directrices sobre protecciones para límites estáticos, así como reglas de validación que se deben tener en cuenta para áreas de nombres de identidad.

### Límites estáticos

En la tabla siguiente se describen los límites estáticos aplicados a los datos de identidad.

| Barrera | Límite | Notas |
| --- | --- | --- |
| Número de identidades en un gráfico | 150 | El límite se aplica en el nivel de zona protegida. El gráfico de identidad no se actualizará una vez que se alcance el límite. **Nota**: el número máximo de identidades en un gráfico de identidades **para un perfil combinado individual** es 50. Los perfiles combinados basados en gráficos de identidad con más de 50 identidades se excluyen del perfil del cliente en tiempo real. Para obtener más información, lea la guía de [protecciones para datos de perfil](../profile/guardrails.md). |
| Número de identidades en un registro XDM | 20 | El número mínimo de registros XDM necesarios es de dos. |
| Número de áreas de nombres personalizadas | Ninguna | No hay límites en el número de áreas de nombres personalizadas que puede crear. |
| Número de gráficos | Ninguna | No hay límites en la cantidad de gráficos de identidad que se pueden crear. |
| Número de caracteres de un nombre para mostrar o un símbolo de identidad | Ninguna | No hay límites en el número de caracteres de un nombre para mostrar o un símbolo de identidad. |

### Validación del valor de identidad

En la tabla siguiente se describen las reglas existentes que debe seguir para garantizar una validación correcta del valor de identidad.

| Área de nombres | Regla de validación | Comportamiento del sistema cuando se infringe la regla |
| --- | --- | --- |
| ECID | <ul><li>El valor de identidad de un ECID debe ser exactamente de 38 caracteres.</li><li>El valor de identidad de un ECID debe constar solo de números.</li></ul> | <ul><li>Si el valor de identidad de ECID no es exactamente de 38 caracteres, se omite el registro.</li><li>Si el valor de identidad de ECID contiene caracteres no numéricos, se omite el registro.</li></ul> |
| No ECID | El valor de identidad no puede superar los 1024 caracteres. | Si el valor de identidad supera los 1024 caracteres, se omite el registro. |

### Ingesta del área de identidad

A partir del 31 de marzo de 2023, el servicio de identidad bloqueará la ingesta de Adobe Analytics ID (AAID) para nuevos clientes. Esta identidad se suele introducir a través de [fuente de Adobe Analytics](../sources/connectors/adobe-applications/analytics.md) y el [fuente de Adobe Audience Manager](../sources//connectors/adobe-applications/audience-manager.md) y es redundante porque el ECID representa el mismo explorador web. Si desea cambiar esta configuración predeterminada, póngase en contacto con el equipo de la cuenta de Adobe.

## Pasos siguientes

Consulte la siguiente documentación para obtener más información sobre [!DNL Identity Service]:

* [Información general del [!DNL Identity Service]](home.md)
* [Visualizador de gráficos de identidad](ui/identity-graph-viewer.md)
