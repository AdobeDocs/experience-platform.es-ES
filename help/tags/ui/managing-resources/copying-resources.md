---
title: Copiar recursos
description: Aprenda a crear un nuevo recurso de etiquetas con la configuración de un recurso de etiquetas existente en Adobe Experience Platform.
exl-id: 7e52ceae-97df-4c64-aba3-4f5ba6018a47
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 94%

---

# Copiar recursos

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

A veces, es conveniente crear un nuevo recurso con la configuración de un recurso existente. En estos casos, puede hacer una copia.

Se pueden copiar propiedades, extensiones, reglas y elementos de datos.

Copiar un recurso crea un duplicado de ese recurso en el destino especificado. Es una acción discreta y única y no existe ninguna relación continua entre el recurso original y las copias que se han realizado.

## Inicio de una copia

Puede iniciar una copia de una extensión consultando las extensiones instaladas, seleccionando la flecha desplegable del botón **[!UICONTROL Configurar]** y seleccionando **[!UICONTROL Copiar]**.

![Copia de la extensión de Analytics](../../images/copy-initiate-extension.png)

Para las propiedades, las reglas y los elementos de datos, simplemente seleccione el recurso que desee copiar y, a continuación, seleccione **[!UICONTROL Copiar]** en el menú de acciones.

![Copia de mi regla de Analytics](../../images/copy-initiate-rule.png)

Si está copiando una regla o un elemento de datos, en el cuadro de diálogo Copiar puede utilizar el menú desplegable para seleccionar una propiedad de destino a la que desee copiar (la configuración predeterminada es la propiedad actual). Las extensiones no se pueden copiar en la misma propiedad, por lo que no proporcionarán esa opción.

>[!NOTE]
>
>No se pueden copiar recursos a otra propiedad si una propiedad está configurada para el desarrollo de extensiones y la otra propiedad no.

Una vez que haya configurado el comportamiento deseado, seleccione **[!UICONTROL Copiar]**.

## Copia de propiedades

Cuando realiza una copia de una propiedad completa, hay algunas cosas que debe comprender sobre el proceso.

* La configuración de la propiedad se copiará exactamente como es (dominios, configuración avanzada, etc.)
* Las reglas, los elementos de datos y las extensiones de la propiedad de origen se copiarán en la nueva propiedad de destino. Los adaptadores, entornos y bibliotecas no se copiarán.
* Las extensiones necesarias (extensiones necesarias para cualquier elemento de datos o componente de regla existente) se copiarán en la propiedad de destino incluso si se han desinstalado de la propiedad de origen.
* Copiar una propiedad puede tardar un tiempo. Esto sucede en segundo plano. Puede supervisar el progreso de la copia o puede continuar con otras tareas mientras sucede.
* Si modifica un recurso individual después de que ya se haya copiado en la propiedad de destino (pero antes de que se haya completado la copia), las nuevas modificaciones no se copiarán.

## Copia de extensiones

Al copiar una extensión a otra propiedad, hay que tener en cuenta determinados puntos importantes.

* Si la propiedad de destino no tiene la extensión instalada, esta se instala con la misma configuración que la propiedad de origen.
* Si la propiedad de destino ya tiene la extensión instalada, solo se copia la configuración.
* Si la propiedad de destino tiene una versión inferior a la de la extensión instalada, se envía un aviso de que debe actualizar la extensión en la propiedad de destino antes de poder realizar la copia. Los desarrolladores de extensiones pueden añadir ajustes a sus extensiones a lo largo del tiempo, por lo que los ajustes de una extensión más reciente no se pueden aplicar de forma fiable a versiones anteriores.
* Si la propiedad de destino tiene una versión superior a la de la extensión instalada, la configuración se copia, pero no se modifica la versión por una anterior. La propiedad de destino mantiene su número de versión actual.

## Copia de reglas y elementos de datos

Una extensión es la encargada de proporcionar todas las reglas y los elementos de datos, por lo que al realizar copias entre las propiedades, Platform debe tener en cuenta estas extensiones subyacentes.

![Copia de una regla a mi propiedad de muestra](../../images/copy-rules-dialog1.png)

El cuadro de diálogo Copiar proporciona una explicación de lo que sucede exactamente antes de comenzar la copia. El cuadro de diálogo anterior es para una regla, pero lo mismo se aplica a los elementos de datos.

1. **Se copian las extensiones requeridas por estas reglas.** Esto le permite saber que las extensiones requeridas van acompañadas de la regla. Estas copias siguen las mismas reglas que las copias de extensión regular descritas anteriormente.
1. **La configuración de extensión NO se copia si la extensión ya está instalada.** Esto significa que si ya existen las extensiones requeridas en la propiedad de destino, la extensión se mantiene sin cambios. Si desea copiar también la configuración de la extensión, puede utilizar el botón **Replace extension settings on destination property** y la explicación se actualiza en consecuencia.
1. **Los elementos de datos requeridos por estas reglas NO se copian.** Esta explicación solo se aplica a las reglas. Las reglas suelen depender de los elementos de datos para funcionar correctamente. Si copia una regla en una propiedad nueva, también debe copiar los elementos de datos necesarios como una acción independiente.
