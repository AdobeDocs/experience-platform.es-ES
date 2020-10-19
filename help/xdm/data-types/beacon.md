---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;beacon;interaction details;datatype;data-type;data type;
solution: Experience Platform
title: Tipo de datos de señalización
topic: overview
description: Este documento proporciona información general sobre la clase de Perfil individual XDM.
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 3%

---


# [!UICONTROL Tipo de datos de señalización]

[!UICONTROL La señalización] es un tipo de datos XDM estándar que describe el dispositivo inalámbrico que comunica información de identidad a las aplicaciones móviles a medida que los dispositivos móviles se encuentran dentro del rango.

<img src="../images/data-types/beacon.png" width="450" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `beaconMajor` | Duplicada | Los valores principales identifican y distinguen un grupo y los valores enteros sin signo entre 1 y 65.535. |
| `beaconMinor` | Duplicada | Los valores menores identifican y distinguen valores enteros individuales y sin signo entre 1 y 65.535. |
| `proximity` | Cadena | Distancia estimada desde la señalización. Consulte el [apéndice](#proximity) para conocer los valores y las definiciones aceptados. |
| `proximityUUID` | Cadena | Un UUID de proximidad (identificador único universal) es un tipo especial de identificador que se utiliza para distinguir las señalizaciones de la red de todas las demás señalizaciones de redes fuera de su control. El UUID de proximidad se configura en una señalización, que se transmitirá a dispositivos móviles en el rango para identificar las señalizaciones de una organización. |

Para obtener más información sobre el tipo de datos, consulte el repositorio público XDM:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/beacon-interaction-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/beacon-interaction-details.schema.json)

## Apéndice

La siguiente sección contiene información adicional sobre el tipo de datos de [!UICONTROL señalización] .

## Valores aceptados para proximidad {#proximity}

La siguiente tabla describe los valores aceptados para `proximity` y sus significados asociados:

| Valor | Descripción |
| --- | --- |
| `immediate` | En unos pocos centímetros. |
| `near` | A menos de 10 metros. |
| `far` | Bueno a menos de 10 metros. |
| `unknown` | No se pudo determinar la distancia, probablemente debido a una señal débil. |