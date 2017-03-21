---
layout: post
title: "El tercer parámetro de addEventListener"
date:   2017-03-21
categories: javascript browser
---

En mi proceso de aprendizaje sobre los [pointer events](), decidí de una vez por todas comprender bien qué significaba el tercer parámetro del evento *addEventListener* utilizado, como bien sabéis, para registrar un evento ocurrido en cualquier elemento del DOM:

    addEventListener('evento', listener [, useCapture])

Siempre que escribía este método, obviaba el tercer parámetro o directamente lo ponía a *true* porque de esta forma nunca me daba problemas para cumplir mi objetivo. *"Ese parámetro será cosa de pros"*, me decía. Pero nada de eso.

Vamos a tomar como ejemplo este código:

    <body>
      <div>
        <button id="button">Hola</button>
      </div>
    </body>

Según el flujo de eventos del DOM, cuando se produce un evento sobre un elemento del mismo, éste salta también en todos los elementos padre del original. Por lo que, si hacemos clic con el ratón sobre el elemento *button* también lo estamos haciendo sobre el elemento *div* y el elemento *body*.

Aquí es donde entra el paramétro al que hacíamos referencia. Si su valor es *true* (valor por defecto), el orden en el que se lanzan los listeners del evento que escucha el elemento hijo es de arriba a abajo. En el ejemplo, sería *body*-*div*-*button*:

    document.getElementById('button')
      .addEventListener('clic', function() {..}, true);

O también:

    document.getElementById('button')
      .addEventListener('clic', function() {..});

Esto es llamado **fase de captura**. Vamos, lo que hacía yo siempre sin darme cuenta.

En cambio, si queremos que el primer listener que salte sea el del elemento hijo, en este caso, el del elemento *button*, tendríamos que poner el tercer parámetro a *false*. Fácil, ¿no?

    document.getElementById('button')
        .addEventListener('clic', function() {..}, false);

En este caso, la propagación sería *button*-*div*-*body*. Es lo que se llama **fase de burbuja**.

Cuando descrubrí este diagrama, lo comprendí todo en cuestión de segundos:

![true => Fase de caputura, false => Fase de burbuha](../images/2017-3-21-javascript-document-addeventlistener-tercer-parametro.png)

Con todo esto, ¿qué ocurriría si tuviéramos el siguiente código?

    document.getElementById('button')
        .addEventListener('click', function(event) {
          console.log(event.target);
          event.stopPropagation();
        }, false);

La respuesta es sencilla: al hacer clic sobre el elemento *button* sólo se imprimiría por consola el elemento *button*. La función *stopPropagation* corta el flujo de eventos del DOM, por lo que la fase de burbuja terminaría. Si, en cambio, el tercer parámetro fuese *true* (o directamente lo dejáramos en blanco), el elemento a mostrar por consola sería el elemento padre *body*.

## Referencias

* [developer.mozilla.org](https://developer.mozilla.org/es/docs/Web/API/EventTarget/addEventListener)
* [arkaitzgarro.com](https://www.arkaitzgarro.com/javascript/capitulo-15.html)
* [odexexempla.org](http://www.codexexempla.org/curso/curso_4_3_e.php)