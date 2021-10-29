

# Moovi-video-supervisor

Esta extension permite manejar las actividades h5p incrustadas de moovi.uvigo.gal a través de comandos de JavaScript y de DOM traversal.
Esta acompañada de una interfaz bastante sencillita que incluye botones para saltar a los puntos de la actividad que requieren interacción del usuario, un input para cambiar la velocidad de reproducción de las actividades y una lista organizada de las respuestas a las actividades extraidas de un script incrustado en la página.

## Instalación

Hay **2** opciones para instalar la extensión:
1. La primera y mas recomendable porque ahorra problemas de compatibilidad con chrome. Para esta descargamos el archivo que termina en **[source_code.zip](https://github.com/valonsogit/moovi-video-supervisor/releases/latest)** y extraemos los archivos del interior en una carpeta que elijamos.
Vamos a la url [chrome://extensions]() (hay que copiarla en la barra de búsqueda) y activamos la checkbox que dice *Developer mode*.
Después de esto cerramos y volvemos a abrir Chrome y volveremos a ir a la página [chrome://extensions](). Aqui pulsaremos la opción de *Load unpacked* y se nos abrirá una ventana para elegir una carpeta, seleccionamos la carpeta que extrajimos previamente y la extensión ya estaría lista para su uso. 
2. La segunda requiere de los mismos pasos al principio pero en vez de pulsar *Load unpacked* simplemente arrastramos el archivo que termina en **[packed_extension.crx](https://github.com/valonsogit/moovi-video-supervisor/releases/latest)** y lo arrastramos a la ventana del navegador, siempre estando en [chrome://extensions]().
Es posible que este método no funcione por un problema de compatibilidad a la hora de comprimirse el archivo, si no funciona te recomiendo probar el modo 1.

![Una foto sacada de Google enseñando los pasos](https://wd.imgix.net/image/BrQidfK9jaQyIHwdw91aVpkPiib2/iYdLKFsJ1KSVGLhbLRvS.png)

>Una foto sacada de Google enseñando los pasos
## El diablo:
```javascript

$.map($("iframe").contents().find("script"), function (script) {
    if (script.innerText && script.innerText.includes("var H5PIntegration")) {
        script_text = script.innerText.slice(script.innerText.indexOf("{", 0))


        return $.map(JSON.parse(Object.values(JSON.parse(script_text.slice(0, script_text.lastIndexOf(";"))).contents)[0].jsonContent).interactiveVideo.assets.interactions.sort(GetSortOrder("duration", "from")), function (interaction, index) {});
    }
})
```
### Créditos
A mi mismo porque la verdad es que no ayuda nadie.

![gatoooo](https://i.pinimg.com/originals/2c/ec/71/2cec71161268a2ef69288b5a4a210587.jpg)