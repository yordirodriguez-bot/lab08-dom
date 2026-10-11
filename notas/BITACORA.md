# Bitacora de JavaScript interactivo

Laboratorio 08: JavaScript Interactivo - DOM, Eventos y Objetos.
Navegador usado: Google Chrome

## Ejercicio 2: Seleccionar y modificar el DOM

| Instruccion | Que cambio en la pantalla | Se mantiene al recargar (Si/No) |
| ---------------------------- | V-------------------------------------------------------------- | ------------------------------- |
| textContent desde la consola | El título cambia temporalmente a "Hola desde la consola" | No |
| textContent desde app.js | El título cambia permanentemente a "Hola TECSUP" | Si |
| style.color | El texto del título cambia a color azul | Si |
| classList.add | El párrafo adquiere un fondo amarillo destacado | Si |
| createElement + appendChild | Se agrega un tercer elemento "JavaScript" al final de la lista | Si |

## Ejercicio 3: Evento click

| Tipo de evento | Que accion lo dispara                       | Cuanto suma por accion              |
| -------------- | ------------------------------------------- | ----------------------------------- |
| click          | Hacer un solo clic izquierdo sobre el botón | Suma 1 cada vez                     |
| dblclick       | Hacer doble clic rápido sobre el botón      | Suma 1 por cada doble clic          |
| mouseover      | Pasar el puntero del mouse sobre el botón   | Suma 1 cada vez que entra el cursor |

evento.type muestra el nombre del evento que ocurrió (por ejemplo, "click").
evento.target muestra el elemento HTML que recibió la acción (por ejemplo, el botón <button id="btnSumar">).

## Ejercicio 4: Eventos input y submit

| Prueba                                  | Que paso en la pantalla                                     | Se recargo la pagina (Si/No) |
| --------------------------------------- | ----------------------------------------------------------- | ---------------------------- |
| Escribir en el campo nombre             | El saludo se actualiza en tiempo real letra por letra       | No                           |
| Enviar sin preventDefault               | Muestra el texto un milisegundo y se recarga limpiando todo | Si                           |
| Enviar con preventDefault, correo sin @ | Muestra "Correo no valido: falta @" en texto rojo           | No                           |
| Enviar con preventDefault, correo con @ | Muestra "Enviado: correo@ejemplo.com" en texto normal       | No                           |

## Ejercicio 5: Clases y objetos

| Objeto  | nombre  | precio | descripcion()       | conDescuento(0.25) |
| ------- | ------- | ------ | ------------------- | ------------------ |
| laptop  | Laptop  | 2500   | Laptop - S/ 2500.00 | 1875               |
| mouse   | Mouse   | 45     | Mouse - S/ 45.00    | 33.75              |
| teclado | Teclado | 120    | Teclado - S/ 120.00 | 90                 |
| monitor | Monitor | 680    | Monitor - S/ 680.00 | 510                |

Usar la clase permite reutilizar la estructura de datos y la lógica de cálculo sin repetir código. Si se agregan nuevos objetos en JavaScript, la página los renderiza automáticamente sin necesidad de modificar la plantilla HTML a mano.

## Ejercicio 6: DOM, eventos y objetos juntos

| Prueba          | Total que muestra la pagina  | Correcto (Si/No) |
| --------------- | ---------------------------- | ---------------- |
| Cuaderno 12.50  | 12.50                        | Si               |
| + Lapicero 3.20 | 15.70                        | Si               |
| + Mochila 89.90 | 105.60                       | Si               |
| Sin Number()    | Error en consola (TypeError) | No               |

| Pieza  | Linea de tu codigo donde aparece                     | Para que sirve                                                                    |
| ------ | ---------------------------------------------------- | --------------------------------------------------------------------------------- |
| DOM    | document.querySelector("#formProducto"), appendChild | Para capturar datos del formulario e insertar elementos li en la interfaz         |
| Evento | formProducto.addEventListener("submit", ...)         | Escucha el envío del formulario y evita la recarga de página con preventDefault() |
| Objeto | new Producto(...), carrito.agregar(...)              | Instancia los productos y gestiona el cálculo del monto total acumulado           |
