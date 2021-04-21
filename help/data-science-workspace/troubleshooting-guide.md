---
keywords: Experience Platform;resolución de problemas;Data Science Workspace;temas populares
solution: Experience Platform
title: Guía de solución de problemas de Data Science Workspace
topic-legacy: Troubleshooting
description: Este documento proporciona respuestas a las preguntas más frecuentes sobre Adobe Experience Platform Data Science Workspace.
exl-id: fbc5efdc-f166-4000-bde2-4aa4b0318b38
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 1%

---

# [!DNL Data Science Workspace] guía de solución de problemas

Este documento proporciona respuestas a las preguntas frecuentes acerca de Adobe Experience Platform [!DNL Data Science Workspace]. Para preguntas y solución de problemas con las API [!DNL Platform] en general, consulte la [Guía de solución de problemas de la API de Adobe Experience Platform](../landing/troubleshooting.md).

## [!DNL JupyterLab] el entorno no se carga en  [!DNL Google Chrome]

>[!IMPORTANT]
>
>Este problema se ha resuelto, pero aún podría estar presente en el explorador Google Chrome 80.x. Asegúrese de que el explorador Chrome esté actualizado.

Con la versión 80.x del explorador [!DNL Google Chrome], todas las cookies de terceros se bloquean de forma predeterminada. Esta directiva puede evitar que [!DNL JupyterLab] se cargue dentro de Adobe Experience Platform.

Para solucionar este problema, siga estos pasos:

En el explorador [!DNL Chrome], vaya a la esquina superior derecha y seleccione **Configuración** (también puede copiar y pegar &quot;chrome://settings/&quot; en la barra de direcciones). A continuación, desplácese hasta la parte inferior de la página y haga clic en la lista desplegable **Avanzado**.

![avanzado de chrome](./images/faq/chrome-advanced.png)

Aparece la sección **Privacidad y seguridad**. A continuación, haga clic en **Configuración del sitio** seguida de **Cookies y datos del sitio**.

![avanzado de chrome](./images/faq/privacy-security.png)

![avanzado de chrome](./images/faq/cookies.png)

Por último, cambie &quot;Bloquear cookies de terceros&quot; a &quot;Desactivado&quot;.

![avanzado de chrome](./images/faq/toggle-off.png)

>[!NOTE]
>
>También puede deshabilitar las cookies de terceros y agregar [*.]ds.adobe.net a la lista de permitidos .

Vaya a &quot;chrome://flags/&quot; en la barra de direcciones. Busque y deshabilite el indicador titulado *&quot;SameSite by default cookies&quot;* mediante el menú desplegable de la derecha.

![deshabilitar indicador samesite](./images/faq/samesite-flag.png)

Después del paso 2, se le pedirá que vuelva a iniciar el explorador. Después de reiniciar, [!DNL Jupyterlab] debe ser accesible.

## ¿Por qué no puedo acceder a [!DNL JupyterLab] en Safari?

Safari deshabilita las cookies de terceros de forma predeterminada en Safari &lt; 12. Como la instancia de la máquina virtual [!DNL Jupyter] reside en un dominio diferente al de su fotograma principal, Adobe Experience Platform actualmente requiere que las cookies de terceros estén habilitadas. Habilite las cookies de terceros o cambie a un explorador diferente como [!DNL Google Chrome].

Para Safari 12, debe cambiar el agente de usuario a &#39;[!DNL Chrome]&#39; o &#39;[!DNL Firefox]&#39;. Para cambiar el agente de usuario, abra el menú *Safari* y seleccione **Preferencias**. Aparecerá la ventana de preferencias.

![Preferencias de Safari](./images/faq/preferences.png)

En la ventana de preferencias de Safari, seleccione **Avanzado**. A continuación, marque la casilla *Mostrar menú Desarrollo en la barra de menús*. Puede cerrar la ventana de preferencias una vez completado este paso.

![Safari avanzado](./images/faq/advanced.png)

A continuación, en la barra de navegación superior, seleccione el menú **Develop**. Desde la lista desplegable **Development**, pase el ratón sobre **User Agent**. Puede seleccionar la cadena del agente de usuario **[!DNL Chrome]** o **[!DNL Firefox]** que desee utilizar.

![Menú Desarrollo](./images/faq/user-agent.png)

## ¿Por qué veo un mensaje &quot;403 prohibido&quot; al intentar cargar o eliminar un archivo en [!DNL JupyterLab]?

Si el explorador está habilitado con software de bloqueo de anuncios como [!DNL Ghostery] o [!DNL AdBlock] Plus, se debe permitir el dominio &quot;\*.adobe.net&quot; en cada software de bloqueo de anuncios para que [!DNL JupyterLab] funcione normalmente. Esto se debe a que las [!DNL JupyterLab] máquinas virtuales se ejecutan en un dominio diferente al dominio [!DNL Experience Platform].

## ¿Por qué algunas partes de mi [!DNL Jupyter Notebook] parecen retorcidas o no se renderizan como código?

Esto puede suceder si la celda en cuestión se cambia accidentalmente de &quot;Código&quot; a &quot;Marcado&quot;. Mientras una celda de código está enfocada, al pulsar la combinación de teclas **ESC+M**, se cambia el tipo de celda a Markdown. El tipo de celda se puede cambiar mediante el indicador desplegable situado en la parte superior del bloc de notas para las celdas seleccionadas. Para cambiar un tipo de celda a código, comience por seleccionar la celda que desee cambiar. A continuación, haga clic en el menú desplegable que indica el tipo actual de la celda y seleccione &quot;Código&quot;.

![](./images/faq/code_type.png)

## ¿Cómo instalo bibliotecas [!DNL Python] personalizadas?

El núcleo [!DNL Python] viene preinstalado con muchas bibliotecas populares de aprendizaje automático. Sin embargo, puede instalar bibliotecas personalizadas adicionales ejecutando el siguiente comando en una celda de código:

```shell
!pip install {LIBRARY_NAME}
```

Para obtener una lista completa de las bibliotecas [!DNL Python] preinstaladas, consulte la sección [apéndice de la Guía del usuario de JupyterLab](./jupyterlab/overview.md#supported-libraries).

## ¿Puedo instalar bibliotecas PySpark personalizadas?

Desafortunadamente, no puede instalar bibliotecas adicionales para el núcleo PySpark. Sin embargo, puede ponerse en contacto con el representante de servicio al cliente de Adobe para que le instalen bibliotecas PySpark personalizadas.

Para obtener una lista de las bibliotecas PySpark preinstaladas, consulte la sección [apéndice de la Guía del usuario de JupyterLab](./jupyterlab/overview.md#supported-libraries).

## ¿Es posible configurar los [!DNL Spark] recursos de cluster para [!DNL JupyterLab] [!DNL Spark] o el núcleo PySpark?

Puede configurar los recursos añadiendo el siguiente bloque a la primera celda del bloc de notas:

```python
%%configure -f 
{
    "numExecutors": 10,
    "executorMemory": "8G",
    "executorCores":4,
    "driverMemory":"2G",
    "driverCores":2,
    "conf": {
        "spark.cores.max": "40"
    }
}
```

Para obtener más información sobre la configuración de [!DNL Spark] recursos de clúster, incluida la lista completa de propiedades configurables, consulte la [Guía del usuario de JupyterLab](./jupyterlab/overview.md#kernels).

## ¿Por qué recibo un error al intentar ejecutar ciertas tareas para conjuntos de datos más grandes?

Si está recibiendo un error por un motivo como `Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.`, esto generalmente significa que el controlador o un ejecutor se está quedando sin memoria. Consulte la documentación de JupyterLab Notebooks [data access](./jupyterlab/access-notebook-data.md) para obtener más información sobre los límites de datos y cómo ejecutar tareas en conjuntos de datos grandes. Normalmente, este error se puede resolver cambiando el `mode` de `interactive` a `batch`.

## [!DNL Docker Hub] restricciones de límite en Data Science Workspace

A partir del 20 de noviembre de 2020, entraron en vigor los límites de velocidad para el uso anónimo y autenticado gratuito de Docker Hub. Los usuarios anónimos y gratuitos de [!DNL Docker Hub] se limitan a 100 solicitudes de extracción de imágenes de contenedor cada seis horas. Si se ve afectado por estos cambios, recibirá este mensaje de error: `ERROR: toomanyrequests: Too Many Requests.` o `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`.

Actualmente, este límite solo afectará a su organización si está intentando crear 100 Notebook para fórmulas en un lapso de seis horas o si está utilizando portátiles basados en Spark en Data Science Workspace que a menudo están aumentando y reduciendo. Sin embargo, es poco probable, ya que el clúster en el que se ejecutan permanece activo durante dos horas antes de apagarse. Esto reduce el número de llamadas necesarias cuando el clúster está activo. Si recibe cualquiera de los errores anteriores, tendrá que esperar hasta que se restablezca su límite [!DNL Docker].

Para obtener más información sobre los límites de tasa [!DNL Docker Hub], visite la [documentación de DockerHub](https://www.docker.com/increase-rate-limits). Se está trabajando en una solución para esto, y se espera que así sea en una versión posterior.
