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

### Pregunta 3: El Mundo de las APIs 

* **3.1.** ¿Qué es una **API** ? Explícalo de forma sencilla, como si se lo estuvieras explicando a alguien que no es programador.
* **3.2.** ¿Qué es una **API REST**? Describe brevemente sus características principales o principios.
* **3.3.** ¿Qué es un **Endpoint**? En el contexto de la API de Rick and Morty (`https://rickandmortyapi.com/api/character/2`), ¿qué parte de la URL representa el endpoint y qué información específica esperarías obtener de él?
* **3.4.** ¿Para qué sirve una herramienta como **Postman** o **Thunder Client** (la extensión de VS Code)? Describe su función principal en el desarrollo de software.
* **3.5. Códigos de Estado HTTP:** Investiga y explica qué representa cada una de las siguientes familias de códigos de estado. Para cada familia, menciona al menos un ejemplo de código específico y lo que significa. 🆕
    * **Codigos (100-199):** ¿Cuál es su propósito general?, ¿Qué indican este tipo de respuestas?
    * **Codigos (200-299):** ¿Cuál es su propósito general?, ¿Qué indican este tipo de respuestas?
    * **Codigos (300-399):** ¿Cuál es su propósito general?, ¿Qué indican este tipo de respuestas?
    * **Codigos (400-499):** ¿Cuál es su propósito general?, ¿Qué indican este tipo de respuestas?
    * **Codigos (500-599):** ¿Cuál es su propósito general?, ¿Qué indican este tipo de respuestas?

**[ESPACIO PARA TU RESPUESTA 3]**

**[3.1] Imagina que una API es como el menú de un restaurante.

Tú, como cliente (tu aplicación), quieres comer algo (obtener datos o realizar una acción).

El restaurante (el servidor) tiene una cocina con todos sus ingredientes y recetas (sus bases de datos y lógica), pero tú no puedes entrar a cocinar.

El menú (la API) te presenta una lista estandarizada de platos que puedes pedir (las operaciones disponibles), describe lo que obtendrás (la respuesta) y te indica cómo hacer el pedido (la estructura de la solicitud).

Tú pides el "Pizza Margarita" (haces una petición a un endpoint), el mesero lleva tu pedido a la cocina, y luego te trae la pizza exactamente como se describe en el menú (recibes una respuesta estandarizada).

En conclusión, una API es un intermediario que permite que dos aplicaciones se comuniquen entre sí, definiendo las reglas y formatos para hacerlo, sin que una necesite conocer los detalles internos de la otra.

**[3.2] Una API REST es un tipo específico de API que sigue un conjunto de principios o reglas de arquitectura. Es como si el restaurante decidiera estandarizar todo su servicio usando solo verbos básicos (GET, POST, PUT, DELETE) y un menú donde cada plato tiene una dirección única.

Sus características principales son:

Arquitectura Cliente-Servidor: Separación clara de responsabilidades.

Sin Estado (Stateless): Cada petición del cliente al servidor debe contener toda la información necesaria para entenderla. El servidor no "recuerda" nada entre una petición y otra.

Interfaz Uniforme:

Recursos: Todo se trata como un recurso (ej: /users, /products).

URI (Identificador Uniforme de Recurso): Cada recurso tiene una dirección única (la URL).

Verbos HTTP: Usa los métodos HTTP para definir la acción: GET (obtener), POST (crear), PUT/PATCH (actualizar), DELETE (eliminar).

Representaciones: Los datos se intercambian en formatos como JSON o XML.

Sistema en Capas: El cliente no necesita saber si se está conectando directamente al servidor final o a un intermediario (como un cache).

**[3.3] Un endpoint es una URL específica proporcionada por una API para interactuar con un recurso en particular. Es la dirección exacta a la que envías una solicitud para realizar una operación concreta.

En la URL de la API de Rick and Morty: https://rickandmortyapi.com/api/character/2

La parte que representa el endpoint es: /api/character/2

Desglose:

/api/: Suele ser la raíz o prefijo para todas las operaciones de la API.

/character/: Indica el recurso con el que quiero interactuar (los personajes).

/2: Es el identificador único de un recurso específico (el personaje con ID = 2).

De este endpoint, esperaría obtener un objeto JSON con toda la información específica del personaje con ID 2, que en este caso es Morty Smith. La respuesta incluiría detalles como su nombre, estado, especie, género, origen, ubicación e imagen.

**[3.4] Son herramientas conocidas como clientes de API o probadores de API. Su función principal es actuar como un "laboratorio de pruebas" para desarrolladores, permitiéndonos interactuar con las APIs sin necesidad de escribir código frontend.

¿Qué podemos hacer con ellas?

Enviar Peticiones HTTP: Probarlas manualmente con diferentes métodos (GET, POST, etc.).

Configurar Headers y Body: Añadir fácilmente encabezados de autorización (como API Keys o tokens Bearer) y cuerpos de solicitud en JSON.

Inspeccionar Respuestas: Ver el código de estado, los headers de respuesta y el cuerpo de la respuesta de forma estructurada y legible.

Automatizar y Organizar: Guardar colecciones de peticiones, crear entornos con variables (ej: URL de desarrollo vs producción) y escribir tests automatizados para las respuestas.

Es una herramienta fundamental para el desarrollo, debugging y documentación de APIs.

**[3.5] Son códigos numéricos de 3 dígitos que el servidor envía para indicar el resultado de una petición HTTP. Se agrupan en familias por su primer dígito.

Códigos 100-199 (Respuestas Informativas):

Propósito General: Indicar que la petición fue recibida y el proceso continúa.

Qué indican: "Te he escuchado, sigue así". Son provisionales.

Ejemplo: 100 Continue. Le dice al cliente que la primera parte de la solicitud fue recibida y que puede proceder a enviar el resto (útil en envíos de datos grandes).

Códigos 200-299 (Peticiones Exitosas):

Propósito General: Confirmar que la petición fue recibida, entendida y procesada con éxito.

Qué indican: "¡Todo salió bien!".

Ejemplo: 200 OK. El estándar para una petición exitosa. 201 Created es otro común, indicando que un nuevo recurso fue creado como resultado.

Códigos 300-399 (Redirecciones):

Propósito General: Indicar que se necesita una acción adicional, generalmente una redirección, para completar la petición.

Qué indican: "El recurso que buscas no está aquí, pero te digo dónde está".

Ejemplo: 301 Moved Permanently. La URL solicitada ha sido movida permanentemente a una nueva dirección, y el cliente debe usar esta última en el futuro.

Códigos 400-499 (Errores del Cliente):

Propósito General: Indicar que hubo un error por parte del cliente al hacer la petición.

Qué indican: "Has hecho algo mal".

Ejemplo: 404 Not Found. El recurso solicitado no pudo ser encontrado en el servidor. Otro muy común es 400 Bad Request, que indica que la solicitud está malformada (ej: JSON inválido).

Códigos 500-599 (Errores del Servidor):

Propósito General: Indicar que el servidor falló al intentar procesar una solicitud que parecía válida.

Qué indican: "Yo (el servidor) he cometido un error".

Ejemplo: 500 Internal Server Error. Un error genérico y muy común que indica que algo salió mal en el servidor, pero no se especifica qué. Otro es 503 Service Unavailable, que significa que el servidor no está disponible (por sobrecarga o mantenimiento).
