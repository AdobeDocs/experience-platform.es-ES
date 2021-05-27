---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;señalización;detalles de interacción;tipo de datos;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de señalización
topic-legacy: overview
description: Este documento proporciona información general sobre la clase XDM Individual Profile.
exl-id: a3767c8d-a009-49b4-81a4-b084b6e5101a
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 4%

---

#  Tipo Beacondata

 Beaconis es un tipo de datos XDM estándar que describe el dispositivo inalámbrico que comunica información de identidad a aplicaciones móviles a medida que los dispositivos móviles se encuentran dentro del rango.

<img src="../images/data-types/beacon.png" width="450" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `beaconMajor` | Duplicada | Los valores principales identifican y distinguen entre 1 y 65.535 valores enteros sin signo. |
| `beaconMinor` | Duplicada | Los valores menores identifican y distinguen valores enteros individuales y sin signo entre 1 y 65.535. |
| `proximity` | Cadena | Distancia estimada de la señalización. Consulte el [apéndice](#proximity) para conocer los valores y definiciones aceptados. |
| `proximityUUID` | Cadena | Un UUID de proximidad (Universally Unique Identifier) es un tipo especial de identificador utilizado para distinguir señalizaciones en la red de todas las demás señalizaciones en redes fuera de su control. El UUID de proximidad se configura en una señalización, que se transmitirá a dispositivos móviles en un rango para identificar las señalizaciones de una organización. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/beacon-interaction-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/beacon-interaction-details.schema.json)

## Apéndice

La siguiente sección contiene información adicional sobre el tipo de datos [!UICONTROL Beacon].

## Valores aceptados para proximidad {#proximity}

La siguiente tabla describe los valores aceptados para `proximity` y sus significados asociados:

| Valor | Descripción |
| --- | --- |
| `immediate` | En unos pocos centímetros. |
| `near` | A menos de 10 metros. |
| `far` | Buenos a menos de 10 metros. |
| `unknown` | No se pudo determinar la distancia, probablemente debido a una señal débil. |
