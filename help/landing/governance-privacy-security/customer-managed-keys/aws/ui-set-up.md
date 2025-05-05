---
title: Instalación y configuración de claves administradas por el cliente con AWS mediante el Experience Platform IU
description: Aprenda a configurar la aplicación CMK con su nombre de recurso de Amazon (ARN) y a enviar su ID de clave de cifrado a Adobe Experience Platform.
exl-id: f0e38a60-d448-4975-977e-1367fca10515
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1263'
ht-degree: 0%

---

# Instalación y configuración de claves administradas por el cliente con AWS mediante el Experience Platform IU

Utilice este guía para habilitar las claves administradas por el cliente (CMK) para Experience Platform instancias alojadas en AWS a través del IU Experience Platform.

>[!IMPORTANT]
>
>Antes de continuar con este guía, asegúrese de haber completado la configuración detallada en el [documento &quot;Configuración de AWS KMS para CMK&quot;.](./configure-kms.md)

## Actualice la clave AWS directiva para integrarla con Experience Platform

Para integrar la clave de AWS con Experience Platform, debe editar el JSON en la **[!DNL Key Policy]** sección del espacio de trabajo de KMS. Un directiva de clave predeterminada es similar al JSON que se muestra a continuación.

<!-- The AWS ID below is fake. Q) Can I refer to it simply as AWS_ACCOUNT_ID ? Is that suitable? -->

```JSON
{
  "Id": "key-consolepolicy-3",
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Enable IAM User Permissions",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::123464903283:root" // this is a mock AWS Principal ID, your ID will differ
      },
      "Action": "kms:*",
      "Resource": "*"
    }
  ]
}
```

En el ejemplo anterior, todos los recursos (`"Resource": "*"`) dentro de la misma cuenta (`Principal.AWS`) pueden acceder a la clave. Este directiva permite a los servicios del cuenta realizar operaciones de cifrado y descifrado, restringidas al cuenta especificado. Para conceder a su Experience Platform inquilino único acceso cuenta a esta clave, añada nuevas instrucciones al directiva predeterminado de AWS. Puede obtener el directiva JSON necesario del Experience Platform IU y aplicarlo a su clave de AWS KMS para establecer una conexión segura con Adobe Experience Platform.

En el Experience Platform IU, vaya a la **[!UICONTROL sección Administración]** en el navegación izquierdo carril y seleccione **[!UICONTROL Cifrado]**. En el espacio de trabajo Configuración de  cifrado, seleccione **[!UICONTROL Configurar]** en el tarjeta de claves administradas por el cliente.

![La configuración de cifrado de Experience Platform espacio de trabajo con Configurar resaltada en el tarjeta de claves administradas por el cliente.](../../../images/governance-privacy-security/key-management-service/encryption-configuration.png)

Aparece la configuración de claves administradas por el [!UICONTROL cliente. Copie el objeto del directiva KMS de CMK que se muestra en la Configuración] de cifrado de claves  administradas por el `statement` cliente.

<!-- Select the copy icon (![A copy icon.](../../../../images/icons/copy.png)) to copy the CMK KMS policy to your clipboard. A green pop-up notification confirms that the policy was copied.  -->

<!-- I cannot add the 'and the copy icon highlighted.' to the alt text below as i do not have access to this UI. -->

![directiva muestra la configuración de claves administradas por el cliente con el KMS de CMK.](../../../images/governance-privacy-security/key-management-service/copy-cmk-policy.png)

<!-- This part of the workflow was in contention at the time of the demo.  -->

Siguiente, vuelva a la espacio de trabajo de AWS KMS y actualice los directiva clave que se muestran a continuación.

![La fase de revisión del flujo de trabajo con el directiva y el acabado actualizados resaltados.](../../../images/governance-privacy-security/key-management-service/updated-cmk-policy.png)

añadir al valor predeterminado directiva las cuatro instrucciones del [!UICONTROL espacio de trabajo Configuración] de cifrado de Platform, como se ve a continuación: `Enable IAM User Permissions`, `CJA Flow IAM User Permissions`, `CJA Integrity IAM User Permissions`, `CJA Oberon IAM User Permissions`.

```json
{
    "Version": "2012-10-17",
    "Id": "key-consolepolicy",
    "Statement": [
        {
            "Sid": "Enable IAM User Permissions",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::975049898882:root" // this is a mock AWS Principal ID, your ID will differ
            },
            "Action": [
                "kms:Decrypt",
                "kms:Encrypt",
                "kms:ReEncrypt*",
                "kms:GenerateDataKey*",
                "kms:DescribeKey",
                "kms:CreateGrant"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:PrincipalAccount": "975049898882" // this is a mock AWS Principal ID, your ID will differ
                }
            }
        },
        {
            "Sid": "CJA Flow IAM User Permissions",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::767397686373:root"
            },
            "Action": [
                "kms:Decrypt",
                "kms:Encrypt",
                "kms:ReEncrypt*",
                "kms:GenerateDataKey*",
                "kms:DescribeKey",
                "kms:CreateGrant"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:PrincipalAccount": "767397686373"
                }
            }
        },
        {
            "Sid": "CJA Integrity IAM User Permissions",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::730335345392:root"
            },
            "Action": [
                "kms:Decrypt",
                "kms:Encrypt",
                "kms:ReEncrypt*",
                "kms:GenerateDataKey*",
                "kms:DescribeKey",
                "kms:CreateGrant"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:PrincipalAccount": "730335345392"
                }
            }
        },
        {
            "Sid": "CJA Oberon IAM User Permissions",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::891377157113:root"
            },
            "Action": [
                "kms:Decrypt",
                "kms:Encrypt",
                "kms:ReEncrypt*",
                "kms:GenerateDataKey*",
                "kms:DescribeKey",
                "kms:CreateGrant"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:PrincipalAccount": "891377157113"
                }
            }
        }
    ]
}
```

Seleccione **[!DNL Finish]** esta opción para confirmar el directiva actualizado y crear la clave. La configuración ahora incluye cinco instrucciones, lo que permite a su cuenta de AWS comunicarse con Adobe Experience Platform. Los cambios se aplicarán inmediatamente.

Aparece el espacio de trabajo actualizado [!DNL Customer Managed Keys] de AWS [!DNL Key Management Service] .

### añadir los detalles de la clave de cifrado de AWS para Experience Platform

Siguiente, para habilitar el cifrado, agregue el nombre de recurso de Amazon (ARN) de la clave a la configuración de claves administradas por el cliente de Experience Platform. En la [!DNL Customer Managed Keys] sección de AWS, seleccione el alias de la nueva clave en el lista del [!DNL Key Management Service]archivo .

![Las claves administradas por el cliente de AWS KMS espacio de trabajo con el nuevo alias de clave resaltado.](../../../images/governance-privacy-security/key-management-service/customer-managed-keys-on-aws.png)

Se muestran los detalles de la clave. Todo en AWS tiene un nombre de recurso (ARN) Amazon que
es un identificador único utilizado para especificar recursos en todos los servicios de AWS. Sigue un formato estandarizado: `arn:partition:service:region:account-id:resource`.

Seleccione el icono Copiar para copiar el ARN. Aparecerá un cuadro de diálogo de confirmación.

![Los detalles clave de su clave administrada por el cliente de AWS KMS con el ARN resaltado.](../../../images/governance-privacy-security/key-management-service/keys-details-arn.png)

Ahora, vuelva al IU de configuración de claves administradas por el cliente de Experience Platform. En la sección añadir detalles de la **[!UICONTROL clave de cifrado de AWS, agregue un**&#x200B;[!UICONTROL &#x200B; nombre &#x200B;]&#x200B;**de configuración y el**&#x200B;[!UICONTROL &#x200B; ARN &#x200B;]&#x200B;**de clave de KMS que copió de la IU de]** AWS.

![La espacio de trabajo de configuración de cifrado de Experience Platform con el nombre de configuración y el ARN de clave de KMS resaltados en la sección añadir detalles de la clave de cifrado de AWS.](../../../images/governance-privacy-security/key-management-service/add-encryption-key-details.png)

Siguiente, seleccione **[!UICONTROL GUARDAR]** para enviar el nombre de configuración, el ARN de clave KMS y comenzar validación de la clave.

![La configuración de cifrado de Experience Platform espacio de trabajo con Guardar resaltados.](../../../images/governance-privacy-security/key-management-service/save.png)

Volverá a la [!UICONTROL espacio de trabajo de configuraciones de] cifrado. El estado de la configuración de cifrado se muestra en la parte inferior del tarjeta Claves **administradas por el** cliente.

![Las Configuraciones de cifrado espacio de trabajo en el IU Experience Platform con Procesamiento resaltado en el tarjeta Claves administradas por el cliente.](../../../images/governance-privacy-security/key-management-service/configuration-status.png)

Una vez validada la clave, los identificadores del almacén de claves se agregan al lago de datos y se perfil almacenes de datos para todos los entornos aislados.

>[!NOTE]
>
>La duración del proceso depende del tamaño de los datos. Normalmente, el proceso se completa en menos de 24 horas. Cada sandbox generalmente se actualiza en dos o tres minutos.

## Revocación de claves {#key-revocation}

>[!IMPORTANT]
>
>Comprenda las implicaciones de la revocación de claves en las aplicaciones descendentes antes de revocar cualquier acceso.

Las siguientes son consideraciones clave para la revocación de claves:

- Revocar o deshabilitar la clave hará que sus datos de Experience Platform sean inaccesibles. Esta acción es irreversible y debe realizarse con precaución.
- Tenga en cuenta los plazos de propagación cuando se revoca el acceso a las claves de cifrado. Los almacenes de datos primarios se vuelven inaccesibles en cuestión de unos minutos a 24 horas. Los almacenes de datos en caché o transitorios dejan de ser accesibles en un plazo de siete días.

Para revocar una clave, vaya al espacio de trabajo de AWS KMS. La **[!DNL Customer managed keys]** sección muestra todas las claves disponibles para su cuenta AWS. Seleccione el alias de su clave en el lista.

![Las claves administradas por el cliente de AWS KMS espacio de trabajo con el nuevo alias de clave resaltado.](../../../images/governance-privacy-security/key-management-service/customer-managed-keys-on-aws.png)

Se muestran los detalles de la clave. Para desactivar la clave, seleccione **[!DNL Key actions]** y, a continuación **[!DNL Disable]** , en el menú desplegable.

![Los detalles de su clave de AWS en la IU de AWS KMS con las acciones clave y la desactivación resaltadas.](../../../images/governance-privacy-security/key-management-service/disable-key.png)

Aparecerá un cuadro de diálogo de confirmación. Seleccione **[!DNL Disable key]** para confirmar su elección. El impacto de deshabilitar la clave debe reflejarse en Experience Platform aplicaciones y el IU en un plazo aproximado de cinco minutos.

>[!NOTE]
>
>Una vez que haya deshabilitado la clave, puede habilitarla nuevamente utilizando el mismo método descrito anteriormente si es necesario. Esta opción está disponible en la **[!DNL Key actions]** lista desplegable.

![El cuadro de diálogo Deshabilitar clave con la clave de desactivación resaltada.](../../../images/governance-privacy-security/key-management-service/disable-key-dialog.png)

Alternativamente, si su clave se usa en otros servicios, puede eliminar el acceso para Experience Platform directamente desde el directiva de claves. Seleccione **[!UICONTROL Editar]** en la **[!DNL Key Policy]** sección.

![La sección de detalles de la clave AWS con Editar resaltada en la sección Key directiva.](../../../images/governance-privacy-security/key-management-service/edit-key-policy.png)

Aparecerá la **[!DNL Edit key policy]** Página. Resalte y elimine la instrucción directiva, copiada de la IU de Experience Platform, para quitar los permisos de la aplicación Customer Managed Keys. A continuación, seleccione **[!DNL Save changes]** para completar el proceso.

![La clave Editar directiva espacio de trabajo en AWS con la instrucción JSON object y Guardar cambios resaltados.](../../../images/governance-privacy-security/key-management-service/delete-statement-and-save-changes.png)

## Rotación de claves {#key-rotation}

AWS ofrece rotación de claves automática y bajo demanda. Para reducir el riesgo de comprometer las claves o cumplir los requisitos de cumplimiento normativo de seguridad, puede generar automáticamente nuevas claves de cifrado bajo demanda o a intervalos regulares. Programe la rotación automática de claves para limitar la vida útil de una clave y asegurarse de que si una clave se ve comprometida, se vuelva inutilizable después de la rotación. Si bien los algoritmos de cifrado modernos son altamente seguros, la rotación de claves es un importante medir de cumplimiento de seguridad y demuestra el cumplimiento de las mejores prácticas de seguridad.

### Rotación automática de teclas {#automatic-key-rotation}

La rotación automática de claves está deshabilitada de forma predeterminada. Para programar la rotación automática de teclas desde el espacio de trabajo KMS, seleccione el **[!DNL Key rotation]** pestaña, seguido **[!DNL Edit]** de en el **[!DNL Automatic key rotation section]** archivo .

![La sección de detalles de la clave AWS con la rotación de claves y Editar resaltados.](../../../images/governance-privacy-security/key-management-service/key-rotation.png)

Aparecerá la **[!DNL Edit automatic key rotation]** espacio de trabajo. Desde aquí, seleccione el botón de opción para activar o desactivar la rotación automática de teclas. Luego use el campo de entrada de texto, o el menú desplegable, para elegir un período de tiempo para la rotación de claves. Seleccione **[!DNL Save]** esta opción para confirmar la configuración y volver a los detalles clave espacio de trabajo.

>[!NOTE]
>
>El período mínimo de rotación de claves es de 90 días y el máximo es de 2560 días.

![La Editar rotación automática de teclas espacio de trabajo con el período de rotación y la Guardar resaltados.](../../../images/governance-privacy-security/key-management-service/automatic-key-rotation.png)

### Rotación de claves a petición {#on-demand-key-rotation}

Seleccione **[!DNL Rotate Now]** esta opción para realizar una rotación de clave inmediata si la clave actual se ve comprometida. AWS limita esta característica a 10 rotaciones. Para el mantenimiento regular, programe rotaciones automáticas de teclas en su lugar.

![La sección de detalles de la clave AWS con Rotar ahora resaltada.](../../../images/governance-privacy-security/key-management-service/on-demand-key-rotation.png)

## Pasos siguientes

Después de leer este documento, ha aprendido a crear, configurar y administrar claves de cifrado en AWS KMS para Adobe Experience Platform. Siguiente, revise las políticas de seguridad y cumplimiento de su organización para implementar prácticas recomendadas, como programar rotaciones de claves y garantizar la seguridad de almacenamiento clave.
