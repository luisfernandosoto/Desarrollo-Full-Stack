# Resumen de HTTP GET y Solicitudes en Aplicaciones Web

## Protocolo HTTP GET

El protocolo **HTTP** es el mecanismo de comunicación entre un servidor y un navegador web. En la pestaña **Network** de las herramientas de desarrollo, podemos ver cómo se comunica el navegador con el servidor. Al recargar una página, se pueden observar dos eventos:

1. El navegador solicita el contenido de la página **studies.cs.helsinki.fi/exampleapp**.
2. Se descarga la imagen **kuva.png**.

### Eventos de Red

Al hacer clic en el primer evento, se muestra más información:

- **Método GET**: El navegador realiza una solicitud a la URL **https://studies.cs.helsinki.fi/exampleapp** con un código de estado **200**, indicando que la solicitud fue exitosa.
- **Cabeceras de Respuesta**: Las cabeceras indican el tamaño de la respuesta, el tipo de contenido (HTML) y otros detalles como la hora exacta de la respuesta.

El navegador también solicita la imagen **kuva.png**:

- Solicitud a **https://studies.cs.helsinki.fi/exampleapp/kuva.png** con un tipo de contenido **image/png**.
- **Código de estado 200**: Indica que la imagen fue descargada correctamente.

### Diagrama de Secuencia

El diagrama de secuencia visualiza la interacción entre el navegador y el servidor:

1. El navegador realiza una solicitud HTTP GET para obtener el código HTML.
2. El HTML contiene una etiqueta `<img>` que hace que el navegador realice una segunda solicitud para la imagen.
3. La página HTML se muestra antes de que la imagen se haya obtenido del servidor.

## Aplicaciones Web Tradicionales

En aplicaciones web tradicionales, el navegador obtiene un documento HTML que detalla la estructura de la página. Este HTML puede ser generado de forma estática o dinámica por el servidor.

### Ejemplo de Generación Dinámica de HTML

El siguiente código genera dinámicamente la página de inicio de una aplicación web:

```javascript
const getFrontPageHtml = noteCount => {
  return`
    <! DOCTYPE html>
    <html>
      <head>
      </head>
      <body>
        <div class='container'>
          <h1>
          <p>number of notes created ${noteCount}</p>
          <a href='/notes'>notes</a>
          <img src='kuva.png' width='200' />
        </div>
      </body>
    </html>
`
}

app.get('/', (req, res) => {
  const page = getFrontPageHtml(notes.length)
  res.send(page);
});
