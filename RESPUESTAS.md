# Parcial 2 · Respuestas de razonamiento

Nombre:

Son cuatro preguntas de 5 puntos sobre código que ya conoces. Para cada una:

1. Lee el código y escribe primero lo que **crees** que pasa.
2. Compruébalo: pégalo en la consola de DevTools (F12 → Console) con tu página del parcial abierta en Live Server. En esa consola sí se puede usar `await` fuera de una función.
3. Escribe tu respuesta debajo de cada letra: (a), (b), (c)…

Se califica la explicación, no solo el resultado: con dos o tres frases por letra es suficiente. Escríbela con tus palabras, porque te la pueden preguntar.

## P1 · ¿En qué orden se imprime? (5 puntos)

**Lo viste en:** la función `cargar` del Explorador (semana 8): «await pausa ESTA función, no el navegador».

```js
console.log('1');
setTimeout(() => console.log('2'), 0);
const cargar = async () => {
  console.log('3');
  const respuesta = await fetch('https://rickandmortyapi.com/api/episode/1');
  console.log('4');
};
cargar();
console.log('5');
```

**(a)** Los cinco números en el orden en que salen en la consola. (2 pts)

Respuesta:

**(b)** Por qué el `3` sale **antes** que el `5`, si `cargar` es una función `async`. (2 pts)

Respuesta:

**(c)** Por qué el `5` no espera a que termine el `fetch`, y por qué el `2` y el `4` salen al final. (1 pt)

Respuesta:

## P2 · Un 404 que no llega al catch (5 puntos)

**Lo viste en:** el `pedirJSON` del Explorador (semana 8): «fetch solo falla si NO pudo hablar con el servidor».

El episodio 9999 no existe: la API responde con código **404** y el cuerpo `{"error":"Episode not found"}`.

```js
try {
  const respuesta = await fetch('https://rickandmortyapi.com/api/episode/9999');
  const datos = await respuesta.json();
  console.log('Episodio:', datos.name);
} catch (error) {
  console.log('Falló:', error.message);
}
```

**(a)** Qué imprime la consola, exactamente. (1 pt)

Respuesta:

**(b)** Por qué **no** entra al `catch`, aunque el episodio no existe. Pista: piensa en la diferencia entre «el servidor respondió con un 404» y «no hubo respuesta» (por ejemplo, sin internet). (2 pts)

Respuesta:

**(c)** La línea que falta para que sí entre al `catch`: escríbela e indica en qué parte del código va. Luego escribe qué imprimiría la consola con esa línea. (2 pts)

Respuesta:

## P3 · LocalStorage sin JSON (5 puntos)

**Lo viste en:** `js/favoritos.js` del Explorador (semana 8): «localStorage solo guarda TEXTO».

```js
const vistos = [1, 5, 8];
localStorage.setItem('vistos', vistos);
const leido = localStorage.getItem('vistos');
console.log(leido, typeof leido);      // (a)
console.log(leido.length);             // (b)
const recuperado = JSON.parse(leido);  // (c)
```

**(a)** Qué imprime la línea marcada (a): el valor y su tipo. (1 pt)

Respuesta:

**(b)** Qué imprime la línea marcada (b), y por qué da ese número. (1 pt)

Respuesta:

**(c)** Qué pasa en la línea marcada (c): ¿funciona o sale un error? Si sale un error, cuál y por qué. (1 pt)

Respuesta:

**(d)** La segunda línea corregida, para que `recuperado` vuelva a ser el array `[1, 5, 8]`. (1 pt)

Respuesta:

**(e)** Por qué en tu `leerVistos` el `JSON.parse` va dentro de un `try/catch`: qué podría pasarle a la app si no estuviera. (1 pt)

Respuesta:

## P4 · Botones que dejan de funcionar (5 puntos)

**Lo viste en:** la delegación en la grilla del Explorador (semana 7, paso 04). Está explicada en el README, en R6: «¿Qué es la delegación?».

Un compañero escribió este código. Al cargar la página, el primer clic en «Marcar como visto» funciona; pero después de ese clic, o después de escribir una letra en el buscador, **ningún botón responde**.

```js
render();
document.querySelectorAll('[data-id]').forEach((boton) => {
  boton.addEventListener('click', () => {
    vistos = alternarId(vistos, Number(boton.dataset.id));
    guardarVistos(vistos);
    render();
  });
});
```

**(a)** Qué les pasó a los botones. Pista: fíjate en qué hace `render()` con el contenido de `#lista` cada vez que se llama, y en cuántas veces se ejecuta el `forEach`. (2 pts)

Respuesta:

**(b)** El código reescrito con **delegación**: un solo listener en `#lista` que funcione con cualquier botón, aunque `render()` lo haya creado después. Se revisan tres cosas, 1 punto cada una: que el listener esté en `#lista` y no en los botones; que use `closest('[data-id]')` (o algo equivalente) para saber qué botón se presionó; y que no haga nada si el clic no fue en un botón. (3 pts)

Respuesta:

```js

```
Luna Villa Santafe 

Examen 2- Programación Web 

 

P1 · ¿En qué orden se imprime? (5 puntos) 

console.log('1'); 

setTimeout(() => console.log('2'), 0); 

const cargar = async () => { 

console.log('3'); 

const respuesta = await fetch('https://rickandmortyapi.com/api/episode/1'); 

console.log('4'); 

}; 

cargar(); 

console.log('5'); 

 

(a) ¿Los cinco números en el orden en que salen en la consola? 

El orden que muestran son: 1, 3, 5, 2, 4. 

(b) ¿Por qué el 3 sale antes que el 5, si cargar es una función async? 

Porque una función async empieza  hasta llegar a un await, entonces, el número 3 se imprime antes de que la función se detenga a esperar la respuesta de fetch. 

(c) ¿Por qué el 5 no espera a que termine el fetch, y por qué el 2 y el 4 salen al final? 

Porque await solamente pausa la ejecución dentro de la función cargar, pero no para lo siguiente. El número 5 se imprime inmediatamente. El número 2 se ejecuta después porque está dentro de un setTimeout, y el número 4 aparece cuando termina el fetch. 

 

P2 . 

(a) ¿Qué imprime la consola, exactamente? 

La consola nos mostrara: 

text Episodio: undefined 

(b) ¿Por qué no entra al catch, aunque el episodio no existe? 

Porque la petición recibió una respuesta del servidor, aunque el recurso solicitado no esta, Por eso, el programa continúa. 

(c) ¿Qué línea falta para que sí entre al catch? Escríbela e indica en qué parte del código va. 

Falta : 

javascript if (!respuesta.ok) { throw new Error(HTTP ${respuesta.status}); } 

 

P3. 

(a) ¿Qué imprimen las líneas marcadas (a), (b) y (c)? 

La consola imprime: 

text 1,3,8 5 string 

(b) ¿Por qué el dato es un string y no un array? 

Porque localStorage solamente almacena información como texto. Cuando guardamos un arreglo , JavaScript lo convierte en una cadena de caracteres. 

(c) ¿Qué pasa si intentamos hacer leido.push(4)? 

Se produce un error porque esta leido es un string, y el método push solamente funciona con arreglos. 

(d) ¿Qué dos líneas debemos corregir para guardar y recuperar el array correctamente? 

Para guardar: 

javascript localStorage.setItem('vistos', JSON.stringify(vistos)); 

Para recuperar: 

javascript const leido = JSON.parse(localStorage.getItem('vistos')); 

 

 

JSON.stringify() convierte el arreglo en texto JSON y JSON.parse() permite recuperarlo como un arreglo de JavaScript. 

P4. 

(a) ¿Qué les pasa a los botones después de hacer clic en el primero? 

Después de hacer clic los botones dejan de responder porque render vuelve a generar el contenido HTML de las tarjetas. Los botones nuevos no tienen los eventos que se habían agregado a los anteriores. 

(b) ¿Por qué ocurre esto? 

Porque cuando utilizamos innerHTML para reemplazar las tarjetas, los elementos anteriores desaparecen del DOM junto con sus eventos. Los nuevos botones son elementos diferentes y no conservan los addEventListener pasados. 

(c) ¿Cómo se puede solucionar utilizando delegación de eventos? 

Podemos agregar un solo evento al contenedor  lista, en lugar de agregar un evento a cada botón. De esta forma, el evento permanece funcionando porque está asociado al contenedor lista, que no se reemplaza cuando se ejecuta render. 

 
