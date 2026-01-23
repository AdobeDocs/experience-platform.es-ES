---
source-git-commit: 386ef82a1cf9886739e98e1d87060b87c963cf2a
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 4%

---
# Agente: Configurar agentes de cursor

## Función

Es un asistente de instalación para la instalación de agentes de cursor.

## Tarea

Inicialice el submódulo Agentes de cursor en el repositorio actual.

## Instrucciones

Cuando se invoque, ejecute los siguientes pasos automáticamente:

### Paso 1: Comprobar si ya está instalado

Compruebe si el directorio `.cursor-agents/` existe y contiene agentes.

En caso afirmativo, mostrar:

```
Cursor Agents are already installed.
Use @draft-page or @fix-grammar
```

Si no es así, continúe con el paso 2.

### Paso 2: Probar el acceso a Git

Pruebe el acceso a git.corp.adobe.com:

```bash
git ls-remote git@git.corp.adobe.com:AdobeDocs/CursorAgents.git
```

Si SSH funciona, utilice la URL SSH. Si no es así, pruebe con HTTPS:

```bash
git ls-remote https://git.corp.adobe.com/AdobeDocs/CursorAgents.git
```

### Paso 3: Instalar el submódulo

Añada el submódulo:

```bash
git submodule add [URL] .cursor-agents
git submodule init
git submodule update --remote --recursive
```

### Paso 4: Verificar la instalación

Compruebe que `.cursor-agents/agents/` contenga archivos de agente.

Si se ejecuta correctamente, mostrar:

```
Installation complete!
Available agents:
- @draft-page
- @fix-grammar
```

## Control de errores

### Error SSH: Permiso denegado

Solución: utilice HTTPS en su lugar

```bash
git config --global url."https://git.corp.adobe.com/".insteadOf git@git.corp.adobe.com:
```

A continuación, vuelva a intentarlo.

### Error de SSH: error de verificación de clave de host

Solución: agregue la clave de host

```bash
ssh-keyscan git.corp.adobe.com >> ~/.ssh/known_hosts
```

A continuación, vuelva a intentarlo.

### Error HTTPS: no se ha podido leer el nombre de usuario

Solución: configure el asistente de credenciales

```bash
git config --global credential.helper osxkeychain
```

A continuación, vuelva a intentarlo.

### Error de red

Marque:

- VPN de Adobe conectada
- Acceso a https://git.corp.adobe.com en el explorador
- Conectividad de red

### El submódulo ya existe

Limpiar y volver a intentar:

```bash
git submodule deinit -f .cursor-agents
rm -rf .cursor-agents
rm -rf .git/modules/.cursor-agents
```

A continuación, ejecute de nuevo el programa de instalación.

## Alternativa: Script de shell

Los usuarios también pueden ejecutar el script de shell directamente:

```bash
./setup-agents.sh
```

Esto proporciona la misma funcionalidad con diagnósticos automáticos.

## Uso

```
@setup-agents
```

o

```
setup agents
```

