---
title: Ejemplo De Escenarios Para Configurar La Identidad
description: Obtenga información sobre escenarios de ejemplo para configurar Ajustes de identidad.
hide: true
hidefromtoc: true
badge: Alfa
source-git-commit: 03e4cd440f8627ad837a31e1c017d0b824cafb04
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 1%

---

# Casos de ejemplo para configurar reglas de vinculación de gráficos de identidad

>[!IMPORTANT]
>
>Las reglas de vinculación de gráficos de identidad están actualmente en Alpha. La funcionalidad y la documentación están sujetas a cambios.

Este documento describe ejemplos de escenarios que puede tener en cuenta al configurar reglas de vinculación de gráficos de identidad.

## Dispositivo compartido

Hay casos en los que se pueden producir varios inicios de sesión en un solo dispositivo:

| Dispositivo compartido | Descripción |
| --- | --- |
| Ordenadores familiares y tabletas | El marido y la mujer inician sesión en sus respectivas cuentas bancarias. |
| Quiosco público | Viajeros en un aeropuerto que inician sesión con su ID de fidelidad para facturar maletas e imprimir tarjetas de embarque. |
| Centro de llamadas | El personal del centro de llamadas inicia sesión en un solo dispositivo en nombre de los clientes que llaman al servicio de atención al cliente para resolver problemas. |

![shared-devices](../images/identity-settings/shared-devices.png)

En estos casos, desde un punto de vista gráfico y sin límites habilitados, un solo ECID se vinculará a varios ID de CRM.

Con las reglas de vinculación de gráficos de identidad, puede:

* Configure el ID utilizado para iniciar sesión como identificador único. Por ejemplo, puede limitar un gráfico para almacenar solo una identidad con un área de nombres de ID de CRM y, por lo tanto, definir ese ID de CRM como el identificador único de un dispositivo compartido.
   * Al hacer esto, puede asegurarse de que los ID de CRM no se fusionen con el ECID.

## Escenarios de correo electrónico/teléfono no válidos

También hay casos de usuarios que proporcionan valores falsos como números de teléfono o direcciones de correo electrónico al registrarse. En estos casos, si los límites no están activados, las identidades relacionadas con el teléfono/correo electrónico terminarán vinculándose a varios ID de CRM diferentes.

![invalid-email-phone](../images/identity-settings/invalid-email-phone.png)

Con las reglas de vinculación de gráficos de identidad, puede:

* Configure el ID de CRM, el número de teléfono o la dirección de correo electrónico como identificador único y, por lo tanto, limite a una persona a un ID de CRM, número de teléfono o dirección de correo electrónico asociados a su cuenta.

## Valores de identidad erróneos o incorrectos

Hay casos en los que se incorporan valores de identidad erróneos y no únicos en el sistema, independientemente del área de nombres. Algunos ejemplos son:

* Área de nombres IDFA con el valor de identidad &quot;user_null&quot;.
   * Los valores de identidad IDFA deben tener 36 caracteres: 32 caracteres alfanuméricos y cuatro guiones.
* Área de nombres del número de teléfono con el valor de identidad &quot;no especificado&quot;.
   * Los números de teléfono no deben contener caracteres alfabéticos.

Estas identidades podrían resultar en los siguientes gráficos, donde varios ID de CRM se combinan con la identidad &quot;incorrecta&quot;:

![datos erróneos](../images/identity-settings/bad-data.png)

Con las reglas de vinculación de gráficos de identidad puede configurar el CRM ID como identificador único para evitar que el perfil no deseado se contraiga debido a este tipo de datos.

## Pasos siguientes

Para obtener más información sobre las reglas de vinculación de gráficos de identidad, lea la siguiente documentación:

* [Resumen de reglas de vinculación de gráficos de identidad](./overview.md)
* [Servicio de identidad y perfil del cliente en tiempo real](identity-and-profile.md)
* [Lógica de vinculación de identidad](./identity-linking-logic.md)