# FILTRO HTML-CSS

En este proyecto se inicializa con un proyecto base previamente diseñado el cual contenía una ejemplificación funcional del dashboard (Javascript); dicho dashboard fue modificado a conveniencia; también se elimina código que no será utilizado para optimizar el espacio de desarrollo.

Para este proyecto se requirió la creación de los siguientes archivos de estilos:

* **style.css ->** Archivo de estilos principal, en ella se realizan la edición de los estilos generales de todo el proyecto
* **styProd1.css ->** Hoja de estilos encargada de generalizar los estilos y disposición para cada uno de los productos que corresponden a su categoría; en la misma pagina se modifican las imágenes que se requieren cambiar.

## style.css

Inicialmente se importa la fuente que será utilizada.

En * se inicializan los estilos eliminando **margin** y **padding** predeterminados por el navegador, además se inicializa el tamaño total del elemento con **box-sizing**

Se definen algunas variables con los colores que se usaran durante el desarrollo y facilitar su acceso, esto se hace usando **:root**

Se oculta todo lo que no se desborde en el body en el eje X; además se le aplica un color de fondo usando los previamente guardados

Se le eliminan las decoraciones a los textos de los hipervínculos; tambien se quitan estilos predeterminados a elementos de lista **li**

```css
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;500;600;700&display=swap');
* {
	font-family: 'Open Sans', sans-serif;
	margin: 0;
	padding: 0;
	box-sizing: border-box;
}
:root {
	--grey: #F1F0F6;
	--dark-grey: #dad9d9;
	--light: #fff;
	--dark: #000;
	--green: #81D43A;
	--light-green: #E3FFCB;
	--blue: #1775F1;
	--light-blue: #D0E4FF;
	--dark-blue: #0C5FCD;
	--red: #FC3B56;
}

body {
	background: var(--grey);
	overflow-x: hidden;
}

a {
	text-decoration: none;
}

li {
	list-style: none;
}

```

a **main** se le asigna un ancho relativo y paddings especificos para cada lado; al **title** se le asigna un tamaño de fuente y un espesor especifico ; adicional al contenedor **info-data** se le genera la distribución del grid para que las tarjetas de los productos se distribuyan correctamente en el espacio de trabajo, de tal manera que usando **auto-fit** distribuya tantas tarjetas como el **min** le permita así se cambie el tamaño de la ventana del navegador.

```css
main {
	width: 100%;
	padding: 24px 20px 20px 20px;
}
main .title {
	font-size: 28px;
	font-weight: 600;
	margin-bottom: 10px;
}
main .info-data {
	margin-top: 36px;
	display: grid;
	grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
	grid-gap: 20px;
}
```

Para darle estilos a cada div presente en el dashboard principal  agregándole una imagen de background se cambia según el identificador propio asignado; el código se repite tantas veces como imagenes se requieran.

```css
main .info-data .abrigo1{
	background: url('../images/prod1/abrigo1.webp') no-repeat center center;
	background-size: contain;
}
```

a los botones que llevaran a la pagina de cada producto se le asigna un tiempo de transicion y se activa utilizando un :hover

```css
.botonNav {
    display: block;
    text-decoration: none;
    color: #fff;
    transition: 0.4s;  
	border-radius: 10px;  
}
.botonNav:hover{
    transform: scale(1.05);
	opacity: 0.80;
}
```

para que el menu principal muestre unicamente las camisas, abrigos o pantalones se utiliza la pseudoclase **:has** que permite modificar las propiedades de elemntos que no son hermanos o hijos pero que poseen un mismo padre; esto permite que usando un checkbox en cada nombre de la categoria se pueda ocultar las tarjetas (**card**) que no se quieran ver

```css
.mega:has(#abrigo:checked) .card2, .card3{
	display: none;
}
.mega:has(#abrigo:checked) .card3{
	display: none;
}
```

en up i se le asigna el estilo al boton que se encarga de regresar a la parte superior de todas las paginas; se fija con **position:fixed;** de tal manera que siempre se mantenga en una ubicacion predeterminada, se le asigna color forma y prioridad con **z-index** para que siempre se encuentre en el nivel superior

```css
.up i {
    color: #d3d3d3;
    padding: 10px;
    position: fixed;
    bottom: 3%;
    right: 3%;
    background-color: #193d549a;
    padding: 0;
    width: fit-content;
    border-radius: 50%;
    font-size: 2rem;
    z-index: 100;
}
```

## styProd1.css

Nota: En esta hoja de estilos se reutilizaron algunos estilos, por lo tanto se omitirán

Container será el contenedor de todos los productos de la categoría, se usa gap para generar separación entre cada producto de la categoría; además se genera un background transparent junto con backdrop-filter: blur(8px); para generar un efecto de blur en el fondo de cada producto.

```css
.container{
    display: flex;
    align-items: center;
    padding: 0px 50px;
    gap: 50px;
    border-radius: 10px;
    border: 2px solid gray;
    background: transparent;
    backdrop-filter: blur(8px);
}
```

Se genera el grid que se usara para la disposición de las imagenes; **grid-template-columns: 20% 80%;** dos columnas con un ancho relativo **grid-template-rows: repeat(4,1fr);** 4 filas que usaran 1 fracción del espacio disponible cada una

```
.vistas{
    margin: 20px;
    display: grid;
    grid-template-columns: 20% 80%;
    grid-template-rows: repeat(4,1fr);
    gap: 15px;
    width: 100%;
    height: 100%;
}
```

En esta seccion se utiliza la imagen del producto como un fondo, de tal manera que cuando se realice :hover a otras imágenes se pueda modificar mas fácilmente la imagen que se presenta como principal; además se hace la distribución de las imagenes con un grid de tal manera que todas las imágenes posean el mismo nivel y poder usar un selector especifico **~** para poder cambiar las propiedades del otro elemento.

**.vistas > .vista1:hover** muestra la ruta y cuando se realiza :hover sobre cada imagen se modifica el background de la imagen principal; esta función se utilizo para las cuatro vistas por producto

```css
div.imgPpal{
    width: 100%;
    padding: 0;
    margin: 20px;
    grid-column: 2;
    grid-row: 1/span 4;
    transition: all 0.6s ease-in-out 0.2s;
}
.imgPpal1{    
    background: url('../images/prod1/abrigo1.webp') no-repeat center center;
    background-size: cover;
}
div.vistas > .vista1:hover ~ .imgPpal1{
    background: url('../images/prod1/vista1.avif') no-repeat center center;
    background-size: cover;
    width: 100%;
    box-shadow: 10px 10px 10px gray;
}
```

Los cambios para que la pagina sean responsives se realiza mediante **MediaQuery** para cambiar la disposición del grid de tal manera que las imágenes se acoplen al espacio y no se desborden

Adicional a esto se ubica imagen por imagen en las coordenadas del grid correspondiente.

```css
@media (max-width: 768px) {
    main{
        padding: 0;
    }
    div.container{
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(180px, 500px));
        justify-content: center;
        flex-direction: column;
        align-items: center;
        padding: 0;
        gap: 0px;    
    }
    .imgPpal {
        width: 100%;
        margin-left: 0;
        height: auto;
        grid-row: 1/span4;
        grid-column: 2;
    }
    .vistas img{
        width: 100%;
        height: auto;
    }
    .vista1{
        grid-row: 1;
        grid-column: 1;
    }
    .vista2{
        grid-row: 2;
        grid-column: 1;
    }
    .vista3{
        grid-row: 3;
        grid-column: 1;
    }
    .vista4{
        grid-row: 4;
        grid-column: 1;
    }
```

