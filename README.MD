# 🚀 Taller Evaluativo: Flujo de Trabajo Git y Asincronismo en JS

¡Bienvenido/a a este taller!

El objetivo de esta actividad es doble: primero, aplicar un flujo de trabajo profesional utilizando Git, desde la clonación y configuración hasta la entrega de cambios mediante un Pull Request. Segundo, investigar y documentar los conceptos fundamentales del asincronismo en JavaScript.

**La correcta aplicación del flujo de Git es una parte fundamental de la evaluación.**

## 🎯 Objetivos de Aprendizaje

* Aplicar el flujo completo de Git: Fork, Clone, Branch, Commit, Push y Pull Request.
* Configurar credenciales de Git y mantener un historial de commits limpio y atómico.
* Explicar los conceptos clave del asincronismo en JavaScript: Call Stack, Callbacks, Promesas y Async/Await.

## 🛠️ Instrucciones y Flujo de Trabajo Obligatorio

Sigue cada paso en el orden exacto en que se presenta.

### Parte 1: Fork y Clonación del Repositorio

1.  **Acceder al Repositorio Original:** Ubícate en el repositorio principal entregado.
2.  **Hacer Fork:** En la esquina superior derecha, busca y haz clic en la opción **"Fork"**.
    * **Importante:** No cambies el nombre del repositorio.
    * Deja el campo de "Description" vacío.
    * Confirma la creación del Fork.
3.  **Clonar tu Repositorio:** Una vez GitHub te redirija a **tu copia del repositorio (tu fork)**, copia la URL HTTPS y clónalo en tu máquina local.
    ```bash
    git clone [URL_DE_TU_REPOSITORIO_FORKEADO]
    ```

### Parte 2: Limpieza y Configuración de Credenciales

Este paso es crucial para asegurar que tus commits queden asociados a tu usuario de GitHub.

1.  **Abrir Git Bash:** Abre una terminal de Git Bash.
2.  **Limpiar Credenciales Globales:** Ejecuta el siguiente comando para limpiar cualquier credencial guardada previamente en tu sistema. Esto evitará conflictos de autenticación.
    ```bash
    git config --global credential.helper ""
    ```
3.  **Configurar Usuario y Correo:** Asocia tus commits a tu identidad de GitHub. **Recuerda que este paso se detalla en las notas de clases anteriores.**
    ```bash
    git config --global user.name "Tu Nombre Completo o usuario de GitHub"
    git config --global user.email "tu_correo@asociadoagitub.com"
    ```

### Parte 3: Configuración del Repositorio Local

1.  **Abrir el Proyecto:** Abre la carpeta del proyecto que clonaste en tu editor de código (ej. Visual Studio Code).
2.  **Crear una Rama Personal:** Abre una nueva terminal integrada en tu editor y crea una nueva rama. El nombre de la rama debe ser tu nombre completo, utilizando la convención **PascalCase**.
    ```bash
    # Ejemplo: git checkout -b JaimeZapata
    git checkout -b TuNombreCompletoPascalCase
    ```
3.  **Crear Carpeta y Archivo:**
    * Dentro del proyecto, crea una **nueva carpeta**. El nombre de la carpeta debe ser tu nombre completo en **MAYÚSCULA SOSTENIDA**.
    * Dentro de esa nueva carpeta, crea un **nuevo archivo** llamado `CONSULTA.MD`.
4.  **Realizar el Primer Commit:** En este punto, agregarás los nuevos archivos a Git y harás tu primer commit para registrar la estructura inicial.
    ```bash
    git add .
    git commit -m "feat: crea estructura inicial del proyecto y archivo de consulta"
    ```

### Parte 4: Desarrollo de la Consulta

1.  **Responder en el Archivo:** Abre el archivo `CONSULTA.MD` y comienza a responder las preguntas que se encuentran allí.
2.  **Realizar Commits por Avance:** La consulta está dividida en partes. Se espera que realices **al menos un commit por cada pregunta principal respondida**. Esto resultará en aproximadamente 4-5 commits adicionales al inicial. Usa mensajes de commit descriptivos (ej: `docs: resuelve pregunta sobre el Call Stack`).
    ```bash
    # Ciclo de trabajo por cada pregunta
    # 1. Respondes la pregunta en CONSULTA.MD
    # 2. Guardas el archivo
    git add .
    git commit -m "docs: responde pregunta sobre Promesas"
    # 3. Repites para las demás preguntas
    ```

### Parte 5: Entrega Final (Pull Request)

1.  **Subir tu Rama:** Cuando hayas respondido toda la consulta y tengas todos tus commits, sube tu rama personal a tu repositorio forkeado en GitHub.
    ```bash
    # Ejemplo: git push origin JaimeZapata
    git push origin TuNombreCompletoPascalCase
    ```
2.  **Crear el Pull Request (PR):**
    * Ve a la página de tu repositorio forkeado en GitHub.
    * Verás una notificación para crear un "Pull Request" desde tu rama recién subida. Haz clic en "Compare & pull request".
    * Asegúrate de que la configuración sea:
        * **base repository:** El repositorio original del profesor.
        * **base:** `main`
        * **head repository:** Tu repositorio forkeado.
        * **compare:** `TuNombreCompletoPascalCase`
    * El título del PR debe ser: `Entrega Taller Asincronismo - Tu Nombre Completo`.
    * Haz clic en "Create pull request".

**¡Y listo! La entrega final es el Pull Request. No se requiere ningún otro tipo de envío.**