---
source-git-commit: 1ab56cf2495238385d726277f6409d2e0c0cb017
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 3%

---
# Fragmentos

## Cuotas y plazos de procesamiento {#quotas}

Las solicitudes de eliminación de registros están sujetas a límites diarios y mensuales de envío de identificadores, determinados por el derecho de licencia de su organización. Estos límites se aplican a solicitudes de eliminación basadas en la interfaz de usuario y la API.

>[!NOTE]
>
>Puede enviar hasta **1.000.000 de identificadores por día**, pero solo si la cuota mensual restante lo permite. Si su límite mensual es inferior a 1 millón, sus envíos diarios no pueden exceder ese límite.

### Derecho de envío mensual por producto {#quota-limits}

En la tabla siguiente se describen los límites de envío de identificadores por producto y nivel de asignación de derechos. Para cada producto, el límite mensual es el menor de dos valores: un límite de identificador fijo o un umbral basado en porcentajes y vinculado al volumen de datos con licencia.

| Producto | Descripción del derecho | Límite mensual (el que sea menor) |
|----------|-------------------------|---------------------------------|
| REAL-TIME CDP o ADOBE JOURNEY OPTIMIZER | Sin el complemento Escudo de privacidad y seguridad o Escudo de atención sanitaria | 2 000 000 de identificadores o el 5 % de la audiencia direccionable |
| REAL-TIME CDP o ADOBE JOURNEY OPTIMIZER | Con el complemento Escudo de privacidad y seguridad o Escudo de atención sanitaria | 15 000 000 de identificadores o el 10 % de la audiencia direccionable |
| Customer Journey Analytics | Sin el complemento Escudo de privacidad y seguridad o Escudo de atención sanitaria | 2 000 000 de identificadores o 100 identificadores por millón de filas de CJA de derechos |
| Customer Journey Analytics | Con el complemento Escudo de privacidad y seguridad o Escudo de atención sanitaria | 15 000 000 de identificadores o 200 identificadores por millón de filas de CJA de derechos |

>[!NOTE]
>
> La mayoría de las organizaciones tendrán límites mensuales más bajos en función de su audiencia direccionable real o de los derechos de fila de CJA.

Las cuotas se restablecen el primer día de cada mes calendario. La cuota no utilizada **no** se transfiere.

>[!NOTE]
>
>Las cuotas se basan en los derechos mensuales con licencia de su organización para **identificadores enviados**. Estas no se aplican mediante protecciones del sistema, pero se pueden supervisar y revisar.
>
>La eliminación de registros es un **servicio compartido**. Su límite mensual refleja el derecho más alto en Real-Time CDP, Adobe Journey Optimizer, Customer Journey Analytics y cualquier complemento de Shield aplicable.

### Tiempos de procesamiento para los envíos de identificadores {#sla-processing-timelines}

Después del envío, las solicitudes de eliminación de registros se ponen en cola y se procesan según su nivel de asignación de derechos.

| Descripción del producto y los derechos | Duración de cola | Tiempo máximo de procesamiento (SLA) |
|------------------------------------------------------------------------------------|---------------------|-------------------------------|
| Sin el complemento Escudo de privacidad y seguridad o Escudo de atención sanitaria | Hasta 15 días | 30 días |
| Con el complemento Escudo de privacidad y seguridad o Escudo de atención sanitaria | Normalmente 24 horas | 15 días |

Si su organización requiere límites más altos, póngase en contacto con su representante de Adobe para obtener una revisión de las autorizaciones.
