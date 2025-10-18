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

### Pregunta 2: Los Callbacks

* **2.1.** ¿Qué es un **"callback"** en JavaScript? Explica con tus propias palabras para qué se utilizaban principalmente en el contexto asíncrono.
* **2.2.** Investiga en internet sobre el término **"Callback Hell"** o **"Pyramid of Doom"**. Pega un ejemplo de código que lo ilustre y explica por qué esa estructura es problemática para la legibilidad y el mantenimiento del código a largo plazo.

**[ESPACIO PARA TU RESPUESTA 2]**

**[2.1] Un callback es una función que se pasa como argumento a otra función, se espera que esta segunda función la ejecute en un momento posterior.

**[2.2] En el contexto asíncrono, los callbacks eran la forma original y fundamental de manejar operaciones que no son inmediatas. Se utilizaban principalmente para decirle al motor de JavaScript:

"Oye, haz esta tarea que va a tomar tiempo (como leer un archivo, hacer una petición a un servidor o esperar 5 segundos), y cuando termines, ejecuta esta función callback que te estoy pasando."

De esta manera, el programa no se "bloquea" esperando a que la tarea lenta termine, sino que puede seguir ejecutando otro código. Cuando la tarea asíncrona finaliza, el callback se coloca en una cola (la "Callback Queue") y eventualmente es llevado al "Call Stack" para ser ejecutado. Esto es el corazón del Event Loop.

El "Callback Hell" (Infierno de los Callbacks) o "Pyramid of Doom" (Pirámide de la Perdición) es un anti-patrón que surge cuando anidamos muchos callbacks asíncronos de forma consecutiva, uno dentro del otro, leading a un código con una sangría excesiva y muy difícil de leer, que se asemeja a una pirámide o a las paredes de un pozo.

Ejemplo de Código (Un vistazo al averno):

// Simulando una secuencia de pasos para hacer un café
// Cada paso depende del anterior y es asíncrono.

function hacerCafe(callback) {
    calentarAgua(function(aguaCaliente) {
        molerGranos(function(granosMolidos) {
            mezclarIngredientes(aguaCaliente, granosMolidos, function(cafeMezclado) {
                servirEnTaza(cafeMezclado, function(cafeServido) {
                    añadirAzucar(cafeServido, function(cafeFinal) {
                        callback(cafeFinal);
                    });
                });
            });
        });
    });
}

// Funciones auxiliares (simuladas con setTimeout)
function calentarAgua(callback) {
    setTimeout(() => callback("Agua caliente lista"), 1000);
}
function molerGranos(callback) {
    setTimeout(() => callback("Granos molidos listos"), 500);
}
function mezclarIngredientes(agua, granos, callback) {
    setTimeout(() => callback(`Café mezclado con ${agua} y ${granos}`), 300);
}
function servirEnTaza(cafe, callback) {
    setTimeout(() => callback(`¡${cafe} en la taza!`), 200);
}
function añadirAzucar(cafe, callback) {
    setTimeout(() => callback(`☕ ${cafe} con azúcar`), 150);
}

// Uso
hacerCafe(function(cafe) {
    console.log(cafe); // ☕ ¡Café mezclado con Agua caliente lista y Granos molidos listos en la taza! con azúcar
});

¿Por qué esta estructura es problemática?

Pésima Legibilidad: El código se va "comiendo" hacia la derecha, formando una pirámide que es muy difícil de seguir visualmente. No se lee de forma natural (de arriba a abajo).

Dificultad de Mantenimiento: Si quieres agregar, quitar o cambiar el orden de un paso, tienes que modificar varios niveles de anidación, lo que es propenso a errores.

Manejo de Errores Complicado: En este modelo, manejar errores en cada paso se vuelve un suplicio. Tendrías que pasar y verificar un objeto de error en cada uno de los callbacks, duplicando aún más el código y la complejidad.

Acoplamiento Excesivo: Cada paso está fuertemente acoplado al siguiente, haciendo el código rígido y poco reutilizable.

Pérdida de Control: Se vuelve complicado realizar tareas como ejecutar algunas operaciones en paralelo o cancelar toda la secuencia si algo falla.


