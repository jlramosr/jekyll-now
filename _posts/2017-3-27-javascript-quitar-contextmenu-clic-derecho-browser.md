---
layout: post
title: "Cómo quitar el menú por defecto al hacer clic derecho"
date:   2017-03-27
categories: polymer iron-list error
---

Hoy os dejo una sencilla solución para quitar el menú que aparece por defecto al hacer clic derecho sobre una web en el navegador o sobre un elemento de la misma. Esto es útil por si quisiéramos crear nuestro propio menú o evitar, por ejemplo, que el usuario tenga disponible la opción de guardar una imagen al hacer clic derecho sobre ella.

    document.addEventListener('contextmenu', function(event) {
      event.preventDefault();
      {...}
    });

El evento *contextmenu* se activa al hacer clic derecho con el mouse o pulsando mucho y rápido el botón izquierdo. En el ejemplo, utilizamos una función anónima para el listener y se usa la función *preventDefault*, útil para detener el resto del funcionamiento por defecto del evento. Tened en cuenta también que en el ejemplo se escucha el evento *contextmenu* en todo el documento. Si quisiéramos desactivar el clic derecho sólamente en un elemento habría que hacer lo mismo pero con 

    elemento.addEventListener('contextmenu', listener);

Recuerda entonces: **usa *event.preventDefault()* para cancelar el comportamiento por defecto de un evento.**

¡Saludos!

## Referencias

* [developer.mozilla.org](https://developer.mozilla.org/es/docs/Web/API/Event/preventDefault)
* [htmlpoint.com](http://www.htmlpoint.com/javascript/corso/js_11.htm)