---
title: Finalización de la compatibilidad con etiquetas en Internet Explorer 10 y 11
description: Adobe Experience Platform ya no admite la actualización de etiquetas en Internet Explorer 10 y 11.
exl-id: 35491c80-2a8a-4e07-baa7-a5db373b6852
source-git-commit: 44e056407f5089c927752f00cc6bf173d7640b83
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# Finalización de la compatibilidad con etiquetas en Internet Explorer 10 y 11

A medida que el panorama de la experiencia digital en línea sigue evolucionando, Adobe ya no invierte recursos en admitir Internet Explorer 10 (IE10) e Internet Explorer 11 (IE11) para las etiquetas en Adobe Experience Platform. Aunque el Adobe de no elimina activamente la compatibilidad con IE10 e IE11, el impacto de estos exploradores en las nuevas funciones ya no se tendrá en cuenta en futuras actualizaciones.

## ¿Por qué IE10 e IE11 ya no son compatibles?

Existen cuatro razones por las que las etiquetas ya no son compatibles con IE10 y IE11:

* **Microsoft deja de admitir IE10 y IE11**: en enero de 2020, [Microsoft dejó de admitir IE10](https://docs.microsoft.com/en-us/lifecycle/announcements/internet-explorer-10-end-of-support) para actualizaciones de seguridad y que no fueran de seguridad. En junio de 2022, [Microsoft dejó de admitir IE11](https://docs.microsoft.com/en-us/lifecycle/announcements/internet-explorer-11-end-of-support) en ciertas versiones de Windows.
* **Un sector más amplio está dejando de admitir IE10 y IE11**: a medida que el sector más amplio deja de admitir IE10 y IE11, la capacidad de las etiquetas para mantener la compatibilidad con versiones anteriores de esas tecnologías se ve cada vez más obstaculizada.
* **Las tecnologías modernas no admiten IE10 ni IE11**: Para que las etiquetas sigan admitiendo las tecnologías más modernas, debe dejar de admitir IE10 y IE11, ya que estas tecnologías modernas no son compatibles con estos exploradores web.
* **La compatibilidad con IE10 y IE11 ralentiza el desarrollo general de las características**: Muchas de las nuevas características lanzadas para las etiquetas requieren una consideración cuidadosa de IE10 y IE11. Esta consideración resulta en horas de trabajo adicional para adquirir herramientas de prueba difíciles de encontrar que funcionen con IE10 e IE11, agregar código adicional para hacer que las características funcionen con IE10 e IE11 que no tienen soporte nativo e investigar para asegurarse de que la característica funcione según lo esperado. Al detener la compatibilidad con IE10 e IE11, el Adobe puede ofrecer nuevas funciones más rápido.

## Efectos de la obsolescencia de IE10 y IE11

Una vez que la compatibilidad esté obsoleta, se producirán los siguientes efectos:

* Es posible que las nuevas funciones no admitan IE10 ni IE11.
* Las pruebas para la compatibilidad con funciones actuales y nuevas mediante IE10 e IE11 dejarán de realizarse.
* Es posible que las funciones que antes admitían IE10 e IE11 ya no sean compatibles con estos exploradores.
