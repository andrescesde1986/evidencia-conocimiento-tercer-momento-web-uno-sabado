* **1.1.** ¿Qué es el **Call Stack** en JavaScript? Explícalo con una analogía del mundo real que facilite su comprensión.
* **1.2.** ¿Qué significa el famoso error `Maximum call stack size exceeded` y cómo podrías provocarlo intencionalmente con un pequeño y simple fragmento de código? (Incluye el código de ejemplo).

**[ESPACIO PARA TU RESPUESTA 1]**
**[1.1] Imagina que el Call Stack (o "Pila de Llamadas") es como una pila de platos sucios en la cocina de un restaurante muy concurrido.

Cada Plato es una Función: Cada vez que llamas a una función en tu código, es como si tomaras un plato nuevo y lo colocaras en lo alto de la pila. Este plato representa la tarea que se está ejecutando en ese momento exacto.

LIFO: La pila funciona con el principio LIFO (Last-In, First-Out), es decir, el último plato que entra es el primero en salir. No puedes lavar un plato que está en medio de la pila sin antes lavar todos los que están encima.

El Proceso:

Llamar a una función: Pones un nuevo plato (función) encima de la pila.

Ejecutar la función: Te enfocas en lavar ese plato de arriba de todo.

Retornar de la función: Cuando la función termina (con un return o al llegar al final), el plato se lava y se retira de la pila. Ahora, el plato que está debajo se convierte en el "actual" y continúa su ejecución desde donde la había dejado.** 

**[1.2] Este error es el equivalente a apilar tantos platos que se te caen todos y haces un desastre monumental en la cocina. El motor de JavaScript tiene un límite para evitar que esta pila sea infinita y se bloquee todo. Cuando superas ese límite, te lanza este error.

¿Cómo provocarlo? Es muy fácil: creando una función recursiva sin caso base (o con un caso base que nunca se cumple). Es como una función que se llama a sí misma sin parar, apilándose una y otra vez hasta desbordar.

Código de ejemplo (el desastre garantizado):

function provocarDesbordamiento() {
    provocarDesbordamiento(); // ¡Se llama a sí misma infinitamente!
}

provocarDesbordamiento(); // Ejecuta esto y prepárate para el error.

---