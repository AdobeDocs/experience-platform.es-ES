---
title: Resumen de atributos calculados
description: Los atributos calculados son funciones para agregar datos de nivel de evento en atributos de nivel de perfil. Estas funciones se calculan automáticamente para que se puedan utilizar en la segmentación, activación y personalización.
source-git-commit: 7ed473750b673eefd84b8d727043ad6ea35c3a8e
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 1%

---


# Resumen de atributos calculados

La personalización basada en el comportamiento del usuario es un requisito clave para que los especialistas en marketing maximicen el impacto de la personalización. Por ejemplo: personalizar el correo electrónico de marketing con el producto visualizado más recientemente para impulsar la conversión o personalizar la página web en función del total de compras realizadas por los usuarios para conseguir la retención.

Los atributos calculados ayudan a convertir rápidamente los datos de comportamiento del perfil en valores agregados a nivel de perfil sin dependencia de los recursos de ingeniería para lo siguiente:

- Habilitar la personalización personalizada o por lotes con objetivo mediante la activación de acumulados de comportamiento a destinos de Real-time Customer Data Platform y su uso en Adobe Journey Optimizer
- Segmentación de audiencia simplificada con almacenamiento de agregados de comportamiento como atributos de perfil
- Estandarización de los datos de comportamiento de perfil agregados para su uso en distintas plataformas y aplicaciones
- Mejor administración de los datos con consolidación de datos de eventos de perfil antiguos en perspectivas de comportamiento significativas

Estos acumulados se calculan en función de conjuntos de datos de evento de experiencia con perfil habilitado introducidos en Adobe Experience Platform. Cada atributo calculado es un atributo de perfil creado en el esquema de unión de perfiles y se agrupa en el grupo de campos &quot;SystemComputedAttribute&quot; del esquema de unión.

Los casos de uso de ejemplo incluyen:

- Personalización de correos electrónicos de marketing con puntos de recompensa totales para felicitar a los usuarios por su promoción a un nivel superior
- Personalización de las comunicaciones con los usuarios en función de los recuentos y la frecuencia de compra
- Personalización de correos electrónicos de retención basados en fechas de caducidad de suscripción
- Volver a dirigir a los usuarios que vieron un producto, pero no lo compraron, con el último producto visualizado
- Activación de agregados de eventos a través de atributos calculados en un sistema descendente mediante Destinos de Real-Time CDP
- Contraer varias audiencias basadas en eventos en un grupo más condensado de atributos calculados
- Redireccionamiento de usuarios no autenticados fuera del sitio mediante el uso de ID de socios recientes de eventos

Esta guía le ayudará a comprender mejor la función de los atributos calculados dentro de Platform, además de explicar los conceptos básicos de los atributos calculados.

## Explicación de los atributos calculados

Adobe Experience Platform permite importar y combinar fácilmente datos de varias fuentes para generar [!DNL Real-Time Customer Profiles]. Cada perfil contiene información importante relacionada con un individuo, como su información de contacto, preferencias e historial de compras, lo que proporciona una vista del cliente en 360 grados.

Parte de la información recopilada en el perfil se entiende fácilmente al leer los campos de datos directamente (por ejemplo, &quot;nombre&quot;), mientras que otros datos requieren realizar varios cálculos o depender de otros campos y valores para generar la información (por ejemplo, &quot;total de compra de por vida&quot;). Para que estos datos sean más fáciles de entender de un vistazo, [!DNL Platform] permite crear atributos calculados que realizan automáticamente estas referencias y cálculos, devolviendo el valor en el campo correspondiente.

Los atributos calculados incluyen la creación de una expresión, o &quot;regla&quot;, que funciona en los datos entrantes y almacena el valor resultante en un atributo de perfil. Las expresiones se pueden definir de varias formas diferentes, lo que permite especificar en qué eventos se agregan, funciones de agregado o duraciones de retrospectiva.

### Funciones

Los atributos calculados permiten definir acumulados de evento de forma automática mediante el uso de funciones predefinidas. Los detalles de estas funciones se pueden encontrar a continuación:

| Función | Descripción | Tipos de datos admitidos | Ejemplo de uso |
| -------- | ----------- | -------------------- | ------------- |
| SUM | Una función que **sumas** Configure el valor especificado para eventos calificados. | Enteros, Números, Largos | Suma de todas las compras de los últimos 7 días |
| RECUENTO | Una función que **recuentos** el número de eventos que se han producido para la regla determinada. | N/A | Recuento de compras en los últimos 3 meses |
| MIN | Una función que encuentra el **minimum** valor de los eventos calificados. | Enteros, Números, Largos, Marcas De Tiempo | Datos de la primera compra en los últimos 7 días<br/>Cantidad mínima del pedido en las últimas 4 semanas |
| MAX | Una función que encuentra el **maximum** valor de los eventos calificados. | Enteros, Números, Largos, Marcas De Tiempo | Datos de la última compra en los últimos 7 días<br/>Cantidad máxima de pedidos en las últimas 4 semanas |
| MÁS_RECIENTE | Una función que encuentra el valor de atributo especificado del evento cualificado más reciente. Esta función proporciona lo siguiente **ambos** el valor y la marca de tiempo del atributo. | Todos los valores primitivos, Matrices de valores primitivos | Últimos productos vistos en los últimos 7 días |

### Períodos retroactivos

Los atributos calculados se calculan por lotes, lo que permite mantener los agregados actualizados y utilizando los eventos más recientes. Para admitir estos escenarios casi en tiempo real, la frecuencia de actualización varía según el período retrospectivo de evento.

El período de retrospectiva hace referencia a la cantidad de tiempo que se revisa al agregar Eventos de experiencia para el atributo calculado. Este período de tiempo se puede definir en horas, días, semanas o meses.

La frecuencia de actualización hace referencia a la frecuencia con la que se actualizan los atributos calculados. Este valor depende del periodo de retrospectiva y se establece automáticamente.

| Período retroactivo | Frecuencia de actualización |
| --------------- | ----------------- |
| Hasta 24 horas | Por hora |
| Hasta 7 días | Diario |
| Hasta 4 semanas | Semanal |
| Hasta 6 meses | Mensual |

Por ejemplo, si el atributo calculado tiene un período retroactivo de los últimos 7 días, este valor se calculará en función de los valores de los últimos 7 días y, a continuación, se actualizará diariamente.

>[!NOTE]
>
>Tanto las semanas como los meses se consideran **semanas calendario** y **meses naturales** cuando se utiliza en retrospectivas de eventos. La semana natural comienza el **Domingo** y termina en **Sábado** de la semana.

**Actualización rápida** {#fast-refresh}

La actualización rápida permite mantener los atributos actualizados. Al habilitar esta opción, puede actualizar los atributos calculados diariamente, incluso para periodos retrospectivos más largos, lo que le permite reaccionar rápidamente a las actividades del usuario.

>[!NOTE]
>
>Al habilitar la actualización rápida, variarán las duraciones de retrospectiva de evento, ya que el período de retrospectiva se desplaza de forma semanal o mensual, respectivamente.
>
>Si crea un atributo calculado con un período retrospectivo de dos semanas con la actualización rápida habilitada, el período retrospectivo inicial será de dos semanas. Sin embargo, con cada actualización diaria, el período retroactivo incluirá eventos del día adicional. Esta adición de días continuará hasta que comience la siguiente semana del calendario, en la que la ventana retrospectiva se volverá a mostrar y volverá a dos semanas.
>
>Por ejemplo, si hubo un período retrospectivo de dos semanas que comenzó el 15 de marzo (domingo) con la actualización rápida habilitada, con actualización diaria, el período retrospectivo seguirá ampliándose inclusive hasta el 22 de marzo, donde se restablecerá a dos semanas. En resumen, el atributo calculado es **actualizado** diariamente, con el periodo retroactivo en aumento desde **dos** semanas para **tres** semanas durante la semana y, posteriormente, volviendo a **dos** semanas.

## Pasos siguientes

Para obtener más información sobre la creación y administración de atributos calculados, lea la [guía de API de atributos calculados](./api.md) o el [guía de IU de atributos calculados](./ui.md).
