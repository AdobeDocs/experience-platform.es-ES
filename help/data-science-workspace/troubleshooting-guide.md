---
keywords: Experience Platform;troubleshooting;Data Science Workspace;popular topics
solution: Experience Platform
title: Guía de solución de problemas de Área de trabajo de Data Science
topic: Troubleshooting
translation-type: tm+mt
source-git-commit: e77b76bdcfa5137d9bd77400b15f2fe8db3b7c0b
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 0%

---


# Guía de solución de problemas de Área de trabajo de Data Science

Este documento proporciona respuestas a las preguntas más frecuentes sobre el espacio de trabajo de ciencia de datos de la plataforma Adobe Experience Workspace. Para obtener preguntas y solución de problemas con las API de plataforma en general, consulte la guía [de solución de problemas de las API de la plataforma de](../landing/troubleshooting.md)Adobe Experience Platform.

## El entorno de JupyterLab no se está cargando en Google Chrome

>[!IMPORTANT] Este problema se ha resuelto, pero aún podría estar presente en el navegador Google Chrome 80.x. Asegúrese de que el navegador Chrome esté actualizado.

Con la versión 80.x del explorador Google Chrome, todas las cookies de terceros están bloqueadas de forma predeterminada. Esta política puede evitar que JupyterLab se cargue en Adobe Experience Platform.

Para solucionar este problema, siga estos pasos:

En el navegador Chrome, desplácese hasta la parte superior derecha y seleccione **Configuración** (también puede copiar y pegar &quot;chrome://settings/&quot; en la barra de direcciones). A continuación, desplácese hasta la parte inferior de la página y haga clic en el menú desplegable **Avanzado** .

![Chrome avanzado](./images/faq/chrome-advanced.png)

Aparece la sección *Privacidad y seguridad* . A continuación, haga clic en Configuración **del** sitio seguido de **Cookies y datos** del sitio.

![Chrome avanzado](./images/faq/privacy-security.png)

![Chrome avanzado](./images/faq/cookies.png)

Por último, cambie &quot;Bloquear cookies de terceros&quot; por &quot;Desactivado&quot;.

![Chrome avanzado](./images/faq/toggle-off.png)

>[!NOTE] También puede deshabilitar las cookies de terceros y agregar [*.]ds.adobe.net a la lista allow.

Vaya a &quot;chrome://flags/&quot; en la barra de direcciones. Busque y deshabilite el indicador titulado *&quot;SameSite de forma predeterminada&quot;* mediante el menú desplegable de la derecha.

![deshabilitar indicador samesite](./images/faq/samesite-flag.png)

Después del paso 2, se le pedirá que vuelva a iniciar el explorador. Después de reiniciar, Jupyterlab debe ser accesible.

## ¿Por qué no puedo acceder a JupyterLab en Safari?

Safari desactiva las cookies de terceros de forma predeterminada en Safari &lt; 12. Dado que la instancia de la máquina virtual de Jupyter reside en un dominio diferente al marco principal, Adobe Experience Platform requiere actualmente que se habiliten las cookies de terceros. Habilite las cookies de terceros o cambie a otro explorador, como Google Chrome.

Para Safari 12, debe cambiar el agente de usuario a &#39;Chrome&#39; o &#39;Firefox&#39;. Para cambiar el agente de usuario, abra el menú *Safari* y seleccione **Preferencias**. Aparecerá la ventana de preferencias.

![Preferencias de Safari](./images/faq/preferences.png)

En la ventana de preferencias de Safari, seleccione **Avanzado**. A continuación, marque el menú *Mostrar desarrollo en la casilla de la barra* de menús. Puede cerrar la ventana de preferencias una vez completado este paso.

![Safari avanzado](./images/faq/advanced.png)

A continuación, en la barra de navegación superior, seleccione el menú **Desarrollar** . En la lista desplegable *Desarrollar* , pase el ratón por encima del agente *de usuario*. Puede seleccionar la cadena de agente de usuario de **Chrome** o **Firefox** que desee utilizar.

![Menú Desarrollar](./images/faq/user-agent.png)

## ¿Por qué veo un mensaje &#39;403 prohibido&#39; al intentar cargar o eliminar un archivo en JupyterLab?

Si el explorador está habilitado con software de bloqueo de anuncios como Ghostery o AdBlock Plus, se debe permitir el dominio &quot;\*.adobe.net&quot; en cada software de bloqueo de anuncios para que JupyterLab funcione normalmente. Esto se debe a que las máquinas virtuales de JupyterLab se ejecutan en un dominio diferente al dominio de la plataforma de experiencia.

## ¿Por qué algunas partes de mi bloc de notas Jupyter parecen revueltas o no se representan como código?

Esto puede suceder si la celda en cuestión se cambia accidentalmente de &quot;Código&quot; a &quot;Código de barras&quot;. Mientras una celda de código está enfocada, al pulsar la combinación de teclas **ESC+M** se cambia el tipo de celda a Markdown. El tipo de celda se puede cambiar mediante el indicador desplegable en la parte superior del bloc de notas de las celdas seleccionadas. Para cambiar un tipo de celda a código, seleccione el inicio de la celda que desee cambiar. A continuación, haga clic en el menú desplegable que indica el tipo actual de celda y, a continuación, seleccione &quot;Código&quot;.

![](./images/faq/code_type.png)

## ¿Cómo instalo bibliotecas Python personalizadas?

El núcleo Python viene preinstalado con muchas bibliotecas populares de aprendizaje automático. Sin embargo, puede instalar bibliotecas personalizadas adicionales ejecutando el siguiente comando en una celda de código:

```shell
!pip install {LIBRARY_NAME}
```

Para obtener una lista completa de las bibliotecas de Python preinstaladas, consulte la sección de [apéndice de la Guía](./jupyterlab/overview.md#supported-libraries)del usuario de JupyterLab.

## ¿Puedo instalar bibliotecas PySpark personalizadas?

Desafortunadamente, no puede instalar bibliotecas adicionales para el núcleo PySpark. Sin embargo, puede ponerse en contacto con el representante de servicio al cliente de Adobe para que le instalen bibliotecas PySpark personalizadas.

Para obtener una lista de las bibliotecas PySpark preinstaladas, consulte la sección de [apéndice de la Guía](./jupyterlab/overview.md#supported-libraries)del usuario de JupyterLab.

## ¿Es posible configurar los recursos del clúster de Spark para el núcleo de JupyterLab Spark o PySpark?

Puede configurar los recursos agregando el siguiente bloque a la primera celda del bloc de notas:

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

Para obtener más información sobre la configuración de recursos del clúster de Spark, incluida la lista completa de propiedades configurables, consulte la Guía del usuario de [JupyterLab](./jupyterlab/overview.md#kernels).