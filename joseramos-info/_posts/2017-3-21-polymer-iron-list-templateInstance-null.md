---
layout: post
title: "Iron-list con Polymer: '_templateInstance' of null"
date:   2017-03-21
categories: polymer iron-list error
---

Tratando de mostrar una simple lista de datos con el elemento [iron-list](https://www.webcomponents.org/element/PolymerElements/iron-list)
de Polymer 1, me ha salido un error que no sabía descifrar.

> Uncaught TypeError: Cannot read property '_templateInstance' of null"

No comprendía nada puesto que el código referente a esta parte era demasiado sencillo. Mirad:

    <iron-list id="ironList" items="[[_filteredData]]">
      <template>
          Name: [[item.name]]
      </template>
    </iron-list>

Después de mucho investigar, dí en el clavo. ¡Vaya tontería! Resulta que dentro del template es necesario que haya un nodo que identificara a cada elemento de la lista. Lógico. Lo que yo estaba poniendo en el template era sólo texto (*Name: [[item.Name]]*). Por lo tanto, la solución pasaba por meter dicho texto dentro de un *div*, quedando:

    <iron-list id="ironList" items="[[_filteredData]]">
      <template>
        <div>
          Name: [[item.name]]
        </div>
      </template>
    </iron-list>

Como estaréis imaginando, también podía haberlo metido dentro de cualquier otro elemento (*span*, *a*, etc.).

¡Hasta la próxima!

## Referencias

* [github.com](https://github.com/PolymerElements/iron-list/issues/225)