---
title: Referencia de resolución de alertas CMK
description: Identifique, solucione problemas y resuelva alertas comunes activadas por errores de configuración de clave gestionada por el cliente (CMK) en Adobe Experience Platform. Utilice esta guía para seguir instrucciones claras y paso a paso y restaurar el acceso seguro a las claves.
exl-id: ffe2eadc-dfb5-418b-a201-2c20dcc9cfe4
source-git-commit: e8cfed9ebd50cf50f03e232755eddef1cb8c0d3b
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 0%

---

# Referencia de resolución de alertas CMK

Utilice esta guía para solucionar problemas y resolver alertas activadas por configuraciones incorrectas de la clave gestionada por el cliente (CMK) en Adobe Experience Platform. Ayuda a los administradores de sistemas y a los especialistas en implementación a identificar causas y aplicar resoluciones para restaurar el acceso seguro.

## Categorías de alerta {#categories}

En las siguientes secciones se describen los tipos de alertas que pueden activarse por problemas de claves gestionadas por el cliente (CMK) en Adobe Experience Platform:

- [Acceso a clave desactivado](#key-access-disabled)
- [Error de acceso a clave](#key-access-failure)
- [Notificación de alerta](#alert-notification)

## Acceso a clave desactivado {#key-access-disabled}

Esta alerta indica que Adobe Experience Platform no puede acceder al CMK configurado porque la clave está deshabilitada o no se puede acceder a ella debido a su configuración. En estos casos, el sistema trata la condición como una eliminación intencionada del acceso con clave.

### Cuando se produce

Esta alerta se activa cuando la clave de cifrado de Azure Key Vault está deshabilitada, eliminada o mal configurada de una manera que impide el acceso durante las operaciones de la plataforma.

### Posibles causas

Las siguientes son razones comunes por las que puede producirse esta alerta:

- La clave se ha deshabilitado manualmente.
- Se han eliminado las operaciones clave (wrapKey/unwrapKey).
- La fecha de activación de la clave se establece en el futuro.
- La fecha de caducidad de la clave es anterior.
- La clave se ha eliminado.
- Los permisos de la aplicación MultiTenant se han eliminado o alterado.
- Se ha eliminado la aplicación MultiTenant.
- Se han cambiado las propiedades de la aplicación MultiTenant.
- El almacén de claves se ha eliminado o ya no es accesible.

### Resolución

+++Si la clave está deshabilitada

1. Vaya a [Azure Key Vault](https://portal.azure.com/) que contiene el CMK.
2. Seleccione la clave asociada a Adobe Experience Platform.
3. Compruebe que el estado de la clave esté establecido en **Habilitado**.
4. Si la clave está deshabilitada, actívela mediante el portal de Azure o el comando CLI `az keyvault key enable`.

>[!NOTE]
>
>Personalice este comando para su entorno de Azure.

+++

+++Si se han alterado las operaciones clave

1. Vuelva a agregar los permisos de `wrapKey` y `unwrapKey` a la clave.

>[!NOTE]
>
>Todos los ajustes de la clave, incluidas las fechas de activación y caducidad, deben ser válidos para que la clave funcione.

+++

+++Si la fecha de activación o caducidad está mal configurada

1. Establezca la fecha de activación en el pasado o en el presente.
2. Establezca la fecha de caducidad en una fecha futura.

+++

+++Si la clave se ha eliminado

1. Asegúrese de que la eliminación suave esté habilitada en Azure Key Vault.
2. Vaya a &quot;Administrar claves eliminadas&quot; en el portal de Azure o CLI.
3. Seleccione la clave eliminada de la lista de elementos eliminados temporalmente.
4. Haga clic en **Recuperar** para restaurar la clave.

+++

+++Si los permisos de la aplicación MultiTenant se eliminaron o modificaron

1. Restaure los permisos correctos para la aplicación MultiTenant.
2. Asegúrese de que se concede el siguiente permiso: `Key Vault Crypto Service Encryption User`

+++

+++Si se eliminó la aplicación MultiTenant

Este es un cambio radical. Debe ponerse en contacto con Adobe para restaurar o regenerar la aplicación de varios inquilinos.

+++

+++Si se cambió la configuración de la aplicación MultiTenant

1. Revertir los cambios a las propiedades asociadas con la aplicación MultiTenant.

+++

+++Si se ha eliminado Key Vault

1. Confirme que la eliminación suave está habilitada en Azure.
2. Vaya a &quot;Administrar depósitos eliminados&quot; en el portal o CLI.
3. Recupere el almacén eliminado dentro de su período de retención (7-90 días).
4. Si la protección contra purgas está desactivada, es posible que aún pueda recuperar el almacén.

>[!NOTE]
>
>Si la protección de eliminación suave o purga no está configurada correctamente, es posible que la clave o el almacén no se puedan recuperar.

+++

## Error de acceso a clave {#key-access-failure}

Esta alerta indica que Adobe Experience Platform no pudo acceder al CMK debido a una denegación de acceso a nivel de red o basada en la configuración.

>[!IMPORTANT]
>
>Esto se trata como un error recuperable. En este caso, los datos **no** se purgaron en SLA.

### Cuando se produce

Esta alerta se suele activar cuando el cortafuegos de Key Vault no está configurado para permitir el acceso CMK de Adobe o cuando falla el acceso basado en identidad.

### Posibles causas

- El firewall de Key Vault está bloqueando la IP estática de Adobe (`20.88.123.53`)
- La clave ya no existe en la ubicación esperada
- Faltan permisos para la aplicación de Adobe MultiTenant
- Se ha eliminado o configurado incorrectamente el almacén de claves
- El ID de objeto de la aplicación MultiTenant ha cambiado

### Resolución

+++Si la clave o el depósito de claves ya no existe

1. Compruebe que el almacén de claves y la clave de cifrado siguen existiendo.
2. Si la clave se ha eliminado, siga los pasos de recuperación de eliminación suave en &quot;Acceso a clave deshabilitado&quot;.

+++

+++Si faltan o se han cambiado los permisos de la aplicación MultiTenant

1. Confirme que la aplicación de Adobe MultiTenant tiene los siguientes permisos:
   - `get`, `wrapKey` y `unwrapKey` en la clave.
2. Compruebe que el ID de objeto de la aplicación MultiTenant sea correcto. Si ha cambiado, vuelva a aplicar los permisos.

+++

+++Si el cortafuegos está bloqueando Adobe

1. Revise las reglas del firewall en Azure Key Vault.
2. Asegúrese de que permiten el acceso desde la IP estática de Adobe: `20.88.123.53`.

>[!NOTE]
>
>Incluso con los permisos correctos, una IP bloqueada impedirá el acceso a las claves.

+++

## Notificación de alerta {#alert-notification}

Esta alerta sirve como notificación general para la configuración de CMK o las anomalías de acceso que no coinciden con un tipo de error conocido.

>[!NOTE]
>
>Esta alerta puede reflejar un error interno, una nueva configuración incorrecta o una condición inesperada.

### Cuando se produce

Esta alerta aparece cuando Adobe CMK detecta un problema desconocido, no admitido o nuevo durante el acceso o la monitorización de claves.

### Posibles causas

- Condiciones de red/cortafuegos no previstas
- Cambios clave o de Vault no cubiertos por tipos de alerta predefinidos
- Interrupciones internas de la red de Adobe
- Configuración incorrecta que Adobe no ha visto antes

### Resolución

+++Si la causa es desconocida o ambigua

1. Revise el mensaje de alerta para cualquier detalle contextual.
2. Compruebe la configuración del cortafuegos, el almacén y las claves para ver si hay cambios recientes.
3. Si no se encuentra una causa clara, póngase en contacto con el soporte técnico de Adobe para obtener ayuda.
4. Monitorice los registros y el comportamiento del sistema para identificar patrones.

+++

## Pasos siguientes

Para comprender cómo se activan las alertas y cómo se configura la inclusión en la lista de permitidos IP para [!DNL Azure] CMK, consulte la guía [Configuración de alertas y lista de permitidos IP para Azure CMK](./azure/alerts-and-ip-access.md).
