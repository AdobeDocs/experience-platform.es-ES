---
title: Atributos derivados
description: Los atributos derivados proporcionan un medio conveniente para generar atributos de su elección que se pueden actualizar en cualquier cadencia normal y, opcionalmente, publicar en los datos del perfil del cliente en tiempo real. Este documento proporciona información general sobre cómo utilizar el servicio de consulta para crear atributos derivados para usarlos con los datos de perfil.
exl-id: 5d52b268-e2a3-411c-8242-3aa32e759937
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---

# Atributos derivados

La función de atributos derivados proporciona un medio conveniente para generar atributos de su elección a partir de otra información disponible en el lago de datos. Estos atributos se pueden actualizar en cualquier cadencia normal y, opcionalmente, publicar en los datos del perfil del cliente en tiempo real. Los atributos derivados abordan la necesidad de crear atributos complejos como decimales, percentiles y cuartiles sobre otros más simples como máximo, recuento y media. Estos atributos se pueden calcular específicamente para un usuario individual o para una entidad comercial. Esto le permite derivar atributos que se pueden acreditar directamente a un identificador, como direcciones de correo electrónico, ID de dispositivo y números de teléfono, y también derivar atributos que están asociados indirectamente a ese usuario o perfil empresarial.

Los atributos derivados son necesarios para una variedad de casos de uso cuando se analizan los datos en el lago de datos. Estos datos se pueden marcar para su uso en el Perfil del cliente en tiempo real y utilizarse en casos de uso descendente, como la creación de audiencias muy específicas. Algunos casos de uso potenciales para esta función pueden incluir:

* Identificación del 10 % más bajo de suscriptores en función de la audiencia por canal. Esto permitiría a los especialistas en marketing dirigirse a una audiencia concreta y vender un nuevo paquete de suscriptores.
* Identificar una audiencia que se encuentra en el 10% superior de los folletos en función de sus millas totales recorridas y que tiene el estado &quot;Volante&quot;. Esta audiencia podría utilizarse para dirigirse selectivamente a la venta de una nueva oferta de tarjeta de crédito.
* Determine la tasa de pérdida en función de la suscripción.
* Identificar el 1% superior de los ingresos de los hogares en una provincia o estado, y proporcionar una medida del número de personas que se han ido de ese grupo colectivo en los últimos &quot;n&quot; meses.

## Atributos derivados complejos

Para crear una clasificación basada en una o más métricas (como ingresos, duración de la audiencia, etc.) en una dimensión en particular (categoría), se necesitan atributos derivados complejos. Los decimales, cuartiles y percentiles permiten flexibilidad y precisión al clasificar datos con atributos derivados.

Un decil es un método para dividir un conjunto de datos clasificados en 10 partes iguales. Cuando los datos se dividen en decimales, se asigna una clasificación de decimales a cada fila del conjunto de datos. Esto permite ordenar los datos en orden descendente o ascendente.

Una clasificación de decimales organiza los datos en orden de menor a mayor y se realiza en una escala del 1 al 10, donde cada número sucesivo corresponde a un aumento de 10 puntos porcentuales.

Los bloques de decimales representan el número de grupos clasificados y se utilizan para asignar una clasificación a una dimensión (categoría) del conjunto de datos. El bloque puede ser un número o una expresión que se evalúa como un valor entero positivo para cada partición. Los bloques no deben tener un valor nulo.

Los cuartiles se utilizan para dividir la distribución por cuatro y los percentiles por 100.

## Atributos derivados analíticos

El servicio de consultas proporciona funciones integradas como la sesionización y el último contacto, entre otras, que puede aplicar a cualquier dato de serie temporal para generar atributos derivados relacionados con el negocio. Tiene la opción de basar estos atributos derivados de análisis en una o más identidades y, opcionalmente, publicar los datos en el Perfil del cliente en tiempo real si es necesario.

Algunos casos de uso potenciales para este tipo de atributo derivado pueden incluir:

* Seguimiento de productos escaneados durante una sesión de usuario que no estaban en existencias.
* Seguimiento de métricas populares como el tamaño, el color o la categoría del producto de los productos que se están explorando o comprando.
* Seguimiento de la fuente de la plataforma que provocó la exploración o compra de un producto.
* Rastrear el último elemento explorado por una identidad.
* Seguimiento de métricas como el número promedio de artículos en un carro de compras, el abandono del carro de compras o la frecuencia de compra promedio.

## Otros atributos derivados

También puede calcular métricas empresariales como atributo derivado y utilizarlas junto con atributos simples como código postal o una métrica agregada como recuento total. Por ejemplo, un recuento total basado en una ciudad o provincia, o un recuento total basado en una categoría comercial y una ciudad o provincia.

## Pasos siguientes y casos de uso

Al leer este documento, tiene una mejor comprensión de cómo los atributos derivados de Query Service facilitan casos de uso complejos para maximizar la utilidad de sus datos. A continuación, debe leer el [caso de uso de atributo derivado basado en deciles](./deciles-use-case.md) para ver cómo se aplica esta función en un escenario real.
