# Tarea: Mi componente interactivo

## Componente elegido

Gestor interactivo de lista de tareas pendientes con asignación de prioridades, marcado de estado completado y eliminación dinámica de elementos.

---

## Version 1: solo DOM

En esta primera versión se construyó la estructura visual base HTML y se manipularon los elementos directamente con el DOM para verificar la inserción de contenido estático desde JavaScript.

### Código principal (Version 1)

```javascript
const listaTareas = document.querySelector("#listaTareas");

// Creación directa de elementos en el DOM sin eventos
const li = document.createElement("li");
li.textContent = "Estudiar selectores del DOM [Prioridad: Alta]";
listaTareas.appendChild(li);
```

---

## Version 2: con eventos

Se incorporó el manejo de eventos para recibir datos desde un formulario, validar que los campos no estén vacíos y permitir interacción directa con botones.

### Código principal (Version 2)

```javascript
const formTarea = document.querySelector("#formTarea");
const tituloInput = document.querySelector("#tituloTarea");
const prioridadInput = document.querySelector("#prioridadTarea");
const msgError = document.querySelector("#msgError");
const listaTareas = document.querySelector("#listaTareas");

formTarea.addEventListener("submit", (e) => {
  e.preventDefault();

  // Validación de campos
  if (tituloInput.value.trim() === "" || prioridadInput.value.trim() === "") {
    msgError.textContent = "Por favor, completa todos los campos.";
    return;
  }

  msgError.textContent = "";

  const li = document.createElement("li");
  li.textContent = `${tituloInput.value} [Prioridad: ${prioridadInput.value}]`;

  const btnEliminar = document.createElement("button");
  btnEliminar.textContent = "Eliminar";

  btnEliminar.addEventListener("click", () => {
    li.remove();
  });

  li.appendChild(btnEliminar);
  listaTareas.appendChild(li);

  formTarea.reset();
});

tituloInput.addEventListener("input", () => {
  if (tituloInput.value.trim() !== "") {
    msgError.textContent = "";
  }
});
```

## Version 3: con clases y objetos

Se refactorizó el código introduciendo Programación Orientada a Objetos mediante la clase `Tarea` para encapsular la estructura de datos y la lógica del estado de cada elemento.

### Código principal (Version 3)

```javascript
class Tarea {
  constructor(titulo, prioridad) {
    this.id = Date.now();
    this.titulo = titulo;
    this.prioridad = prioridad;
    this.completada = false;
  }

  alternarEstado() {
    this.completada = !this.completada;
  }

  obtenerDetalle() {
    return `${this.titulo} [Prioridad: ${this.prioridad}]`;
  }
}

const formTarea = document.querySelector("#formTarea");
const tituloInput = document.querySelector("#tituloTarea");
const prioridadInput = document.querySelector("#prioridadTarea");
const msgError = document.querySelector("#msgError");
const listaTareas = document.querySelector("#listaTareas");

const tareasBD = [];

formTarea.addEventListener("submit", (e) => {
  e.preventDefault();

  if (tituloInput.value.trim() === "" || prioridadInput.value.trim() === "") {
    msgError.textContent = "Por favor, completa todos los campos.";
    return;
  }

  msgError.textContent = "";
  const nuevaTarea = new Tarea(tituloInput.value, prioridadInput.value);
  tareasBD.push(nuevaTarea);

  renderizarTarea(nuevaTarea);
  formTarea.reset();
});

tituloInput.addEventListener("input", () => {
  if (tituloInput.value.trim() !== "") {
    msgError.textContent = "";
  }
});

function renderizarTarea(tareaObj) {
  const li = document.createElement("li");
  li.dataset.id = tareaObj.id;

  const span = document.createElement("span");
  span.textContent = tareaObj.obtenerDetalle();

  const btnCompletar = document.createElement("button");
  btnCompletar.textContent = "Completar";

  const btnEliminar = document.createElement("button");
  btnEliminar.textContent = "Eliminar";

  btnCompletar.addEventListener("click", () => {
    tareaObj.alternarEstado();
    span.classList.toggle("completada");
  });

  btnEliminar.addEventListener("click", () => {
    li.remove();
  });

  li.appendChild(span);
  li.appendChild(btnCompletar);
  li.appendChild(btnEliminar);
  listaTareas.appendChild(li);
}
```

## Donde uso DOM, eventos y objetos

| Pieza       | Linea / Fragmento de codigo                                                                 | Para que sirve                                                                                            |
| :---------- | :------------------------------------------------------------------------------------------ | :-------------------------------------------------------------------------------------------------------- |
| **DOM**     | `document.createElement("li")` / `li.remove()`                                              | Para crear e insertar dinámicamente elementos en la lista y eliminarlos de la pantalla.                   |
| **Eventos** | `formTarea.addEventListener("submit", ...)` / `btnCompletar.addEventListener("click", ...)` | Para capturar el envío del formulario, reaccionar al presionar botones y validar entradas en tiempo real. |
| **Objetos** | `new Tarea(...)` / `tareaObj.alternarEstado()`                                              | Para instanciar los elementos con sus propios datos y alternar su estado interno.                         |

---

## Pruebas realizadas

| Accion de prueba                            | Resultado esperado                                                 | Resultado obtenido                                    | Cumple (Si/No) |
| :------------------------------------------ | :----------------------------------------------------------------- | :---------------------------------------------------- | :------------- |
| Enviar formulario vacío                     | Muestra mensaje de error en texto rojo.                            | "Por favor, completa todos los campos."               | Si             |
| Escribir en un campo teniendo error         | Limpiar el mensaje de error automáticamente.                       | El mensaje de error desaparece al escribir.           | Si             |
| Agregar "Estudiar DOM" con prioridad "Alta" | Muestra la tarea en la lista con su botón de completar y eliminar. | Se crea el nodo `<li>` con los botones asociados.     | Si             |
| Hacer clic en el botón "Completar"          | Tachar el texto de la tarea cambiando su estilo visual.            | Se agrega la clase `.completada` y el texto se tacha. | Si             |
| Hacer clic en el botón "Eliminar"           | Remover la tarea de la lista en la pantalla.                       | El nodo `<li>` correspondiente se elimina del DOM.    | Si             |

---

## Por que disene asi mi clase

Diseñé la clase `Tarea` con los atributos `id`, `titulo`, `prioridad` y `completada` porque representan de manera precisa la información requerida de una tarea en un entorno de trabajo o estudio.

Los métodos `alternarEstado()` y `obtenerDetalle()` permiten encapsular la lógica de manipulación de datos dentro del propio objeto. De esta forma, el código responsable de renderizar el DOM no necesita preocuparse por la estructura del objeto ni por cómo cambia su estado, manteniendo un código limpio, modular y mantenible.
