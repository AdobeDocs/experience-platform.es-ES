---
title: Información general sobre la seguridad de la capa de transporte mutuo (mTLS)
description: Descubra cómo puede utilizar mTLS para recuperar de forma segura certificados públicos emitidos por Adobe para el reenvío de eventos.
exl-id: e8ee8655-213d-4d2a-93d4-d62824b53b1d
source-git-commit: ab16cc3f70ec54460c7c4834e665c828d75d4d9e
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 2%

---

# Información general sobre la seguridad de la capa de transporte mutuo ([!DNL mTLS])

Vincule los certificados de seguridad de la capa de transporte mutuo ([!DNL mTLS]) en la [!UICONTROL interfaz de usuario de entornos] para tomar el control de la seguridad de su extensión. El certificado [!DNL mTLS] es una credencial digital que prueba la identidad de un servidor o cliente en comunicaciones seguras. Cuando usa la API del servicio [!DNL mTLS], estos certificados le ayudan a comprobar y cifrar las interacciones con el reenvío de eventos de Adobe Experience Platform. Este proceso no solo protege sus datos, sino que también garantiza que todas las conexiones procedan de un socio de confianza.

## Implementar [!DNL mTLS] en un entorno nuevo {#implement-mtls}

Configure el entorno de reenvío de eventos para garantizar que las compilaciones de biblioteca se implementen correctamente en la red perimetral. Durante la configuración, puede seleccionar la opción de alojamiento que mejor se adapte a sus necesidades de implementación. También se agrega automáticamente un certificado [!DNL mTLS] a su nuevo entorno para una comunicación segura.

Para crear un entorno nuevo, seleccione la ficha **[!UICONTROL Entornos]** en el panel izquierdo de las propiedades del Reenvío de eventos y, a continuación, seleccione **[!UICONTROL Agregar entorno]**.

![Propiedades de reenvío de eventos que muestran entornos existentes, destacando [!UICONTROL Agregar entorno].](../../../images/extensions/server/cloud-connector/add-environment.png)

En la página siguiente, seleccione el entorno que desee utilizar para esta configuración. Hay tres entornos disponibles:

>[!NOTE]
>
>Una propiedad se limita a un entorno de desarrollo, uno de ensayo y uno de producción.

| Entorno | Descripción |
| --- | --- |
| Desarrollo | El entorno de desarrollo es para que los integrantes del equipo prueben bibliotecas o cambios en el reenvío de eventos. |
| Ensayo | El entorno de ensayo es opcional y permite a los miembros del equipo aprobado probar y aprobar una biblioteca antes de publicarla. |
| Producción | El entorno de producción se utiliza para los datos de producción en directo. |

![La pantalla de selección de entorno, resaltando [!UICONTROL Select] for Development.](../../../images/extensions/server/cloud-connector/select-environment.png)

En la página **[!UICONTROL Crear entorno]**, escriba un **[!UICONTROL Nombre]** y seleccione ***Adobe Managed*** en el menú desplegable **[!UICONTROL Seleccionar host]**. El **[!UICONTROL certificado]** se ***agrega automáticamente***. Finalmente, seleccione **[!UICONTROL Guardar]**.

![La página Crear entorno de desarrollo, destacando [!UICONTROL Nombre], [!UICONTROL Seleccionar host] y [!UICONTROL Guardar].](../../../images/extensions/server/cloud-connector/create-environment.png)

El entorno se ha creado correctamente y volverá a la ficha **[!UICONTROL Entornos]**, que muestra el nuevo entorno.

![La ficha [!UICONTROL Entornos], que resalta el entorno de desarrollo.](../../../images/extensions/server/cloud-connector/new-environment-created.png)

## Ver detalles del certificado del entorno {#view-certificate}

Para ver los detalles del certificado de un entorno, seleccione la pestaña **[!UICONTROL Entornos]** en el panel izquierdo de las propiedades del Reenvío de eventos y, a continuación, seleccione el entorno para ver los detalles.

Se muestran los siguientes detalles del certificado:

| Nombre del campo | Descripción |
| --- | --- |
| Certificado | Detalles del certificado, que incluyen:<ul><li>**Nombre**: El nombre del certificado.</li><li>**Fecha de creación**: La fecha en la que se creó el certificado.</li><li>**Estado**: El estado actual del certificado:<ul><li>**Actual**: el certificado está en uso activamente.</li><li>**Obsoleto**: el certificado no está en uso, pero aún no ha caducado. Aún se puede seleccionar para su uso.</li><li>**Caducado**: el certificado ha caducado, está atenuado y ya no está disponible para su uso.</li></ul></ul> |
| Caduca | Fecha de caducidad del certificado. |
| Nombre de variable | Nombre de variable del certificado. |
| Estado | Estado actual del certificado:<ul><li>**Implementado**: El certificado se ha implementado correctamente y está activo.</li><li>**Implementación**: el certificado se está implementando.</li><li>**Necesita implementación**: Este estado aparece cuando se selecciona un certificado obsoleto.</li></ul> |

![La página Editar entorno de desarrollo, que resalta los detalles de [!UICONTROL Certificado].](../../../images/extensions/server/cloud-connector/certificate-details.png)

### Seleccionar e implementar un certificado obsoleto {#deploy-obsolete-certificate}

Para usar un certificado obsoleto, vaya a la pestaña **[!UICONTROL Entornos]** en el panel izquierdo de las propiedades del reenvío de eventos y, a continuación, seleccione el entorno para ver sus detalles.

![La ficha [!UICONTROL Entornos], que resalta el entorno de desarrollo.](../../../images/extensions/server/cloud-connector/new-environment-created.png)

En el menú desplegable **[!UICONTROL Certificado]**, seleccione un certificado obsoleto y luego seleccione **[!UICONTROL Guardar]**.

![La página Editar entorno de desarrollo, que resalta el menú desplegable [!UICONTROL Certificado] con certificado obsoleto y el cuadro de diálogo Guardar resaltado.](../../../images/extensions/server/cloud-connector/obsolete-certificate.png)

Para implementar el certificado, seleccione **[!UICONTROL Guardar e implementar]** en el cuadro de diálogo **[!UICONTROL Implementar certificado]**.

![Cuadro de diálogo Implementar certificado con las opciones Guardar e implementar resaltadas.](../../../images/extensions/server/cloud-connector/obsolete-certificate-deploy.png)


## Pasos siguientes {#next-steps}

Este documento muestra cómo crear un entorno para la propiedad de reenvío de eventos, agregar un certificado y utilizar un certificado obsoleto. Para obtener más información sobre los certificados de [!DNL mTLS], consulte [[!DNL mTLS] Información general de la API de servicio](../../../../data-governance/mtls-api/overview.md)

Para obtener información sobre cómo usar certificados de [!DNL mTLS] en las reglas de reenvío de eventos, consulte la [descripción general de la extensión del conector de nube](../cloud-connector/overview.md/#mtls-rules).
