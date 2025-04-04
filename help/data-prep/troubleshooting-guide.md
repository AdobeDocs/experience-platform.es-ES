---
keywords: Experience Platform;inicio;temas populares;
title: Guía de resolución de problemas de preparación de datos
description: Este documento proporciona respuestas a las preguntas frecuentes acerca de la preparación de datos de Adobe Experience Platform.
exl-id: 810cfb2f-f80a-4aa7-ab3c-beb5de78708e
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1257'
ht-degree: 0%

---

# [!DNL Data Prep] guía de solución de problemas

Este documento proporciona respuestas a las preguntas más frecuentes acerca de Adobe Experience Platform [!DNL Data Prep], así como una guía de solución de problemas para errores comunes. Si tiene preguntas e información de solución de problemas relacionados con las API de Experience Platform en general, consulte la [Guía de solución de problemas de API de Adobe Experience Platform](../landing/troubleshooting.md).

## Preguntas frecuentes

A continuación se muestra una lista de las preguntas más frecuentes acerca de [!DNL Data Prep] y sus respuestas.

### ¿Cómo se resuelven los errores de transformación?

[!DNL Data Prep] localiza todos los errores de transformación en la columna en la que se produjeron. Como resultado, esa columna se anula y el resto de la fila se sigue procesando. Estos problemas de transformación se han registrado como **Advertencias**. Se recomienda revisar las advertencias periódicamente y ajustar la lógica de transformación para tener en cuenta los problemas de transformación. Esto aumentará la calidad de los datos introducidos en Experience Platform.

Si las columnas marcadas como **Requerido** se anulan debido a problemas de transformación, la fila no se ingestará. Cuando la incorporación parcial de datos está habilitada, puede establecer el umbral de dichos rechazos antes de que falle todo el flujo. Si el atributo anulado no afectó a ninguna validación de nivel de esquema, la fila se seguirá introduciendo.

También se rechazará cualquier fila que no sea válida, incluso sin errores de transformación. Por ejemplo, un flujo de ingesta de datos puede tener una asignación de paso a través (sin lógica de transformación) a un campo obligatorio y no hay ningún valor entrante para ese atributo. Esta fila se rechazará.

### ¿Cómo puedo omitir los caracteres especiales de un campo?

Puede aplicar secuencias de escape a los caracteres especiales de un campo usando `${...}`. Sin embargo, este mecanismo no admite archivos JSON que contengan campos con un punto (`.`). Al interactuar con jerarquías, si un atributo secundario tiene un punto (`.`), debe utilizar una barra invertida (`\`) para omitir los caracteres especiales. Por ejemplo, `address` es un objeto que contiene el atributo `street.name`, entonces se puede hacer referencia a este como `address.street\.name` en lugar de `address.street.name`.

### ¿Cuál es la longitud máxima de los campos calculados?

Los campos calculados tienen una longitud máxima de 4096 caracteres.

### Se ha producido un error en la ingesta debido a la validación de un atributo, pero tengo ese atributo correctamente en el archivo. ¿Qué es exactamente lo que está mal?

Asegúrese de que el tipo de datos de cada campo coincida con el tipo definido en el esquema. Además, se deben cumplir restricciones como &quot;Obligatorio&quot;, &quot;enumeración&quot; y &quot;formato&quot;.

Los datos que se están ingiriendo deben cumplir con el esquema del Modelo de datos de experiencia (XDM) definido en Experience Platform. Si el atributo no coincide con el tipo o formato esperado especificado en el esquema, la ingesta fallará.

Si se utilizan las funciones de preparación de datos, asegúrese de que la transformación dé como resultado los atributos adecuados. Puede revisar los atributos durante el proceso de configuración del flujo de trabajo de orígenes. Durante el paso de asignación, seleccione **[!UICONTROL Nuevo tipo de campo]** y luego seleccione **[!UICONTROL Agregar campo calculado]**. A continuación, utilice la interfaz de campo calculado para previsualizar cada función.

### ¿Cómo puedo eliminar los valores de datos incorrectos de los registros de ingesta por lotes o de flujo continuo?

Puede utilizar la interfaz de asignación Preparación de datos para realizar el filtrado a nivel de columna asignando únicamente columnas que tengan datos requeridos. También puede utilizar campos calculados para transformar los datos mediante las funciones de soporte.

El filtrado de nivel de fila solo está disponible actualmente para el [conector de origen de Adobe Analytics](../sources/tutorials/ui/create/adobe-applications/analytics.md#row-level-filtering).

Después de la ingesta, puede utilizar el destilador de datos para limpiar, dar forma y manipular los datos mediante SQL. Sin embargo, este proceso requerirá la eliminación del lote con los registros incorrectos y la reingesta de un nuevo lote creado a partir del resultado del SQL.

>[!IMPORTANT]
>
>* Laca de datos: solo puede eliminar registros que ya se han introducido eliminando y volviendo a ingerir el lote en el que se encuentra el registro.
>
>* Perfil del cliente en tiempo real: puede sobrescribir registros basados en atributos mediante la ingesta de nuevos registros, pero no se pueden eliminar los registros de eventos de experiencia.
>
>* Servicio de identidad: no se pueden eliminar registros directamente en el servicio de identidad. Tendrá que eliminar todo el perfil y volver a cargarlo con los registros correctos mediante la API de eliminación de perfiles.

### ¿Cuáles son las prácticas recomendadas para utilizar campos calculados en datos de GIF?

Puede utilizar las funciones de asignación de preparación de datos durante el paso de asignación de datos de origen al esquema XDM para crear un nuevo campo calculado.

### Cuando se traen datos de Adobe Analytics como fuente, ¿se crea el esquema automáticamente para el perfil?

Los datos de Analytics no se configuran automáticamente para el perfil. Después de configurar el conector de origen, debe entrar en el conjunto de datos y el esquema y habilitarlos para la ingesta de perfiles.

Al crear un flujo de datos de origen de Analytics en una zona protegida de producción, se crean dos flujos de datos:

* Un flujo de datos que rellena los datos históricos del grupo de informes con un retraso de 13 meses en el lago de datos. Este flujo de datos finaliza cuando se completa el relleno.
* Flujo de datos que envía datos en directo al lago de datos y al perfil. Este flujo de datos se ejecuta continuamente.

### ¿Cómo puedo reducir a minúsculas un valor dentro de un objeto de mapa mediante las funciones de preparación de datos?

Puede recuperar el valor mediante la función `map_get_values` y, a continuación, convertirlo en minúsculas mediante la función lower:

```shell
lower(map_get_values(mapObject, 'keyName'))
```

Puede utilizar la misma función para escribir en minúsculas un objeto map. Sin embargo, no puede recorrer un mapa completo y poner cada elemento en minúsculas.

### ¿Puedo utilizar las funciones de preparación de datos de forma anidada?

Sí, puede utilizar una función de preparación de datos dentro de otra función para resolver problemas relacionados con las capacidades complejas de preparación de datos durante la ingesta de datos.

Por ejemplo, si desea definir un campo como nulo en función de una condición específica, puede utilizar la función &quot;if&quot; para comprobar ese campo. Si la función devuelve `true`, puede usar &quot;nullify()&quot; y si devuelve `false`, puede usar el campo correspondiente.

Si marketing_type era el campo, puede utilizar &quot;.equals&quot; para comprobar el valor en el campo marketing_type y esto se puede anidar dentro de una función &quot;if&quot;. Si devuelve `true`, puede usar la función &quot;nullify()&quot; como se muestra a continuación:

```shell
iif(marketing_type.equals("phyMail"), nullify(), marketing_type)
```

A continuación se describen ejemplos de cómo puede anidar las funciones de preparación de datos mediante if, equals y nullify:

| Función | Descripción | Parámetros | Sintaxis | Expresión | Salida de ejemplo |
| --- | --- | --- | --- | --- | --- |
| iif | Evalúa una expresión booleana determinada y devuelve el valor especificado en función del resultado. | <ul><li>EXPRESIÓN: **Requerida** La expresión booleana que se está evaluando.</li><li>TRUE_VALUE: **Requerido** El valor que se devuelve si la expresión se evalúa como true.</li><li>FALSE_VALUE: **Requerido** El valor que se devuelve si la expresión se evalúa como falsa.</li></ul> | iif(EXPRESSION, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |
| igual a | Compara dos cadenas para confirmar si son iguales. Esta función distingue entre mayúsculas y minúsculas. | <ul><li>CADENA1: **Requerida** La primera cadena que desea comparar.</li><li>CADENA2: **Requerida** La segunda cadena que desea comparar. | CADENA1.&#x200B;es igual a( CADENA2) | &quot;cadena1&quot;.&#x200B;igual a&#x200B;(&quot;STRING1&quot;) | falso |
| anular | Establece el valor del atributo en null. Debe utilizarse cuando no desee copiar el campo en el esquema de destino. | | nullify() | nullify() | null |

{style="table-layout:auto"}

A continuación se muestra un ejemplo de cómo se pueden anidar las funciones, suponiendo que el campo que se evalúa es &quot;marketing_type&quot;.

```shell
iif(marketing_type.equals("phyMail"), nullify(), marketing_type)
```

A continuación, dado que tiene los tres campos siguientes:

* marketing_type: (correo electrónico, correo electrónico, push, sms, teléfono)
* total_conents: intervalo de números de 4000 a 5500
* fecha: de febrero a marzo de 2024

Puede utilizar y anidar las tres funciones enumeradas anteriormente para manipular los tres campos:

* iif(marketing_type.equals(&quot;email&quot;), nullify(), iif(marketing_type.equals(&quot;push&quot;), &quot;push-notification&quot;, marketing_type))
* iif(marketing_type.equals(&quot;phyMail&quot;), nullify(), iif(marketing_type.equals(&quot;sms&quot;), &quot;text-message&quot;, marketing_type))
* iif(total_conents > 5000, iif(marketing_type.equals(&quot;phone&quot;), nullify(), marketing_type), &quot;invalid-conents&quot;)
* iif(date.equals(&quot;3/21/24&quot;), iif(marketing_type.equals(&quot;push&quot;), nullify(), marketing_type), &quot;not-March&quot;)
* iif(total_conents &lt; 4500, iif(marketing_type.equals(&quot;sms&quot;), &quot;low-permission-sms&quot;, marketing_type), &quot;high-conents&quot;)
* iif(marketing_type.equals(&quot;email&quot;), iif(total_conents > 5000, nullify(), &quot;email-low-conents&quot;), marketing_type)
* iif(marketing_type.equals(&quot;push&quot;), iif(total_conents &lt; 4500, &quot;low-permission-push&quot;, nullify()), marketing_type)
* iif(total_conents >= 5500, iif(marketing_type.equals(&quot;phyMail&quot;), nullify(), &quot;high-conents&quot;), marketing_type)