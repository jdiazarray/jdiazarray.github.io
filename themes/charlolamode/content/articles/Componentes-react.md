---
title: Componentes controlados y no controlados
type: page
description: Apuntes de diferentes tipos de controladores con ejemplos basico
topic: react
---

En React, los componentes de formulario pueden ser de dos tipos: Controlados y No controlados.

# Componentes controlados

En los componentes controlados, React controla el estado de los elementos del formulario. En lugar de dejar que los elementos del formulario manejen su propio estado interno (como el valor actual de un input), en los componentes controlados, React maneja el estado y las actualizaciones de ese estado.

Por ejemplo:

``` JSX
import React, { useState } from "react";

function ControlledComponent() {
  const [name, setName] = useState("");

  function handleChange(event) {
    setName(event.target.value);
  }

  return (
    <div>
      <label>Name:</label>
      <input type="text" value={name} onChange={handleChange} />
    </div>
  );
}

export default ControlledComponent;
```

En este caso, useState se utiliza para crear un estado para el valor del input. Cada vez que el usuario escribe algo en el input, el controlador del evento onChange se activa y actualiza el estado de name en el componente.

# Componentes no controlados

En los componentes no controlados, React no controla el estado de los elementos del formulario. En lugar de eso, los elementos del formulario controlan su propio estado internamente.

Para recuperar el valor de los elementos del formulario en los componentes no controlados, puedes usar una referencia (ref) al elemento del formulario.

Por ejemplo:

``` JSX
import React, { useRef } from "react";

function UncontrolledComponent() {
  const inputRef = useRef();

  function handleSubmit(event) {
    event.preventDefault();
    console.log(inputRef.current.value);
  }

  return (
    <form onSubmit={handleSubmit}>
      <label>Name:</label>
      <input type="text" ref={inputRef} />
      <button type="submit">Submit</button>
    </form>
  );
}

export default UncontrolledComponent;
```

En este caso, utilizamos useRef para crear una referencia al input. Cuando el formulario se envía, accedemos al valor del input a través de la referencia.

## Diferencias

Las principales diferencias entre los componentes controlados y no controlados son:

 * En los componentes controlados, React controla el estado de los elementos del formulario. En los componentes no controlados, los elementos del formulario controlan su propio estado.

 * En los componentes controlados, los valores de los elementos del formulario se controlan mediante el estado de React y los controladores de eventos. En los componentes no controlados, los valores de los elementos del formulario se acceden utilizando referencias.

* Los componentes controlados son más comunes y suelen ser más fáciles de manejar y depurar. Sin embargo, los componentes no controlados pueden ser útiles cuando necesitas interactuar directamente con los elementos del formulario, como en el caso de las cargas de archivos.

Mas ejemplos de codigos:

[Componente no controlado](https://github.com/jdiazarray/codigos-curso-react/blob/main/1.-Uncontrolled-components.js)

[Componente no controlado con Hook](https://github.com/jdiazarray/codigos-curso-react/blob/main/3.-Uncontrolled-react-way.js)

[Componente no controlado con archivo](https://github.com/jdiazarray/codigos-curso-react/blob/main/2.-Uncontrolled-with-files.js)

[Componente controlado](https://github.com/jdiazarray/codigos-curso-react/blob/main/4.-Controlled-component.js)