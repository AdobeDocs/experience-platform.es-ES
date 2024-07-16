---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;campos;esquemas;esquemas;señalización;detalles de interacción;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de señalización
description: Obtenga información acerca de la clase de perfil individual de XDM.
exl-id: a3767c8d-a009-49b4-81a4-b084b6e5101a
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 17%

---

# Tipo de datos [!UICONTROL Beacon]

[!UICONTROL Beacon] es un tipo de datos XDM estándar que describe el dispositivo inalámbrico que comunica información de identidad a aplicaciones móviles a medida que los dispositivos móviles entran en el rango.

<img src="../images/data-types/beacon.png" width="450" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `beaconMajor` | Duplicada | Los valores mayores identifican y distinguen a un grupo, y los valores enteros sin signo oscilan entre 1 y 65 535. |
| `beaconMinor` | Duplicada | Los valores menores identifican y distinguen a un individuo, y los valores enteros sin signo oscilan entre 1 y 65 535. |
| `proximity` | Cadena | Distancia aproximada desde la baliza. Consulte el [apéndice](#proximity) para ver los valores y definiciones aceptados. |
| `proximityUUID` | Cadena | Un UUID (identificador único universal) de proximidad es un tipo especial de identificador utilizado para distinguir las balizas de su red de todas las demás balizas de redes fuera de su control. El UUID de proximidad se configura en una señalización, que se transmitirá a los dispositivos móviles dentro del alcance para identificar las señalizaciones de una organización. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.schema.json)

## Apéndice

La siguiente sección contiene información adicional sobre el tipo de datos [!UICONTROL Beacon].

## Valores aceptados para proximidad {#proximity}

En la tabla siguiente se describen los valores aceptados para `proximity` y sus significados asociados:

| Valor | Descripción |
| --- | --- |
| `immediate` | En pocos centímetros. |
| `near` | A menos de 10 metros. |
| `far` | A más de 10 metros. |
| `unknown` | No se pudo determinar la distancia, probablemente debido a una señal débil. |
