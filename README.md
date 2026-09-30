<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Generador de Lotería - La Miss GT</title>

<style>

/* =====================================================
   CONFIGURACIÓN GENERAL
===================================================== */

* {
    box-sizing: border-box;
}

body {
    margin: 0;
    font-family: Arial, Helvetica, sans-serif;
    background: #f8e9ff;
    color: #333;
}


/* =====================================================
   PANEL DE CONTROL
===================================================== */

.panel {
    width: 95%;
    max-width: 1100px;
    margin: 25px auto;
    padding: 28px;
    background: white;
    border-radius: 22px;
    box-shadow: 0 5px 20px rgba(0,0,0,0.15);
}

.titulo-principal {
    text-align: center;
    margin: 0 0 8px;
    color: #d6339a;
    font-size: 32px;
}

.descripcion {
    text-align: center;
    color: #777;
    margin-bottom: 25px;
}


/* =====================================================
   CAMPOS
===================================================== */

.grupo {
    margin-bottom: 20px;
}

.grupo label {
    display: block;
    margin-bottom: 7px;
    font-weight: bold;
    color: #555;
}

input[type="text"],
input[type="number"] {
    width: 100%;
    padding: 13px;
    border: 2px solid #ddd;
    border-radius: 10px;
    font-size: 16px;
    outline: none;
}

input[type="text"]:focus,
input[type="number"]:focus {
    border-color: #d6339a;
}

input[type="file"] {
    width: 100%;
    padding: 13px;
    border: 2px dashed #d6339a;
    border-radius: 10px;
    background: #fff5fc;
    cursor: pointer;
}


/* =====================================================
   LISTA DE IMÁGENES
===================================================== */

#listaImagenes {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(160px, 1fr));
    gap: 15px;
    margin-top: 20px;
}

.imagen-control {
    padding: 10px;
    background: white;
    border: 2px solid #eeeeee;
    border-radius: 15px;
}

.imagen-control img {
    width: 100%;
    height: 125px;
    object-fit: contain;
    display: block;
    background: white;
    border-radius: 10px;
}

.imagen-control input {
    width: 100%;
    margin-top: 8px;
    padding: 8px;
    border: 1px solid #ccc;
    border-radius: 8px;
    text-transform: uppercase;
}


/* =====================================================
   BOTONES
===================================================== */

.botones {
    display: flex;
    justify-content: center;
    gap: 15px;
    flex-wrap: wrap;
    margin-top: 25px;
}

button {
    border: none;
    padding: 15px 28px;
    border-radius: 14px;
    color: white;
    font-size: 17px;
    font-weight: bold;
    cursor: pointer;
    transition: 0.2s;
}

button:hover {
    transform: scale(1.04);
}

.btn-generar {
    background: #7b2cbf;
    box-shadow: 0 4px 10px rgba(123,44,191,0.3);
}

.btn-pdf {
    background: #198754;
    box-shadow: 0 4px 10px rgba(25,135,84,0.3);
}


/* =====================================================
   RESULTADO
===================================================== */

#resultado {
    display: none;
}

.titulo-resultado {
    width: 95%;
    max-width: 1100px;
    margin: 30px auto 15px;
    padding: 15px;
    background: white;
    border-radius: 15px;
    text-align: center;
    color: #7b2cbf;
    font-size: 24px;
    font-weight: bold;
}


/* =====================================================
   PÁGINA DEL CARTÓN
===================================================== */

.pagina-carton {
    width: 210mm;
    height: 297mm;

    margin: 30px auto;

    position: relative;

    background-image: url("fondo-loteria.png");
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;

    overflow: hidden;

    box-shadow: 0 5px 20px rgba(0,0,0,0.18);
}


/* =====================================================
   ENCABEZADO DEL CARTÓN
===================================================== */

.encabezado-carton {
    position: absolute;

    top: 9mm;
    left: 10mm;
    right: 10mm;

    text-align: center;
}

.encabezado-carton h2 {
    margin: 0;

    font-size: 38px;

    font-weight: 900;

    letter-spacing: 4px;

    color: #d6339a;

    text-shadow: 2px 2px white;
}

.titulo-carton {
    margin-top: 5px;

    font-size: 21px;

    font-weight: bold;

    color: #5a189a;
}


/* =====================================================
   TABLERO 4 X 3
===================================================== */

.tablero {
    position: absolute;

    top: 35mm;
    left: 10mm;
    right: 10mm;
    bottom: 18mm;

    display: grid;

    grid-template-columns: repeat(3, 1fr);

    grid-template-rows: repeat(4, 1fr);

    gap: 5px;
}


/* =====================================================
   CASILLAS DEL CARTÓN
===================================================== */

.casilla {
    background: rgba(255,255,255,0.97);

    border: 5px solid;

    border-radius: 10px;

    padding: 3px;

    display: flex;

    align-items: center;

    justify-content: center;

    overflow: hidden;
}

.casilla img {
    width: 100%;
    height: 100%;

    object-fit: contain;

    display: block;
}


/* =====================================================
   PÁGINA DE CARTONCITOS PARA CANTAR
===================================================== */

.pagina-cantitos {
    width: 210mm;
    height: 297mm;

    margin: 30px auto;

    position: relative;

    padding: 8mm;

    background-image: url("fondo-loteria.png");
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;

    overflow: hidden;

    box-shadow: 0 5px 20px rgba(0,0,0,0.18);
}


/* =====================================================
   ENCABEZADO DE CARTONCITOS
===================================================== */

.encabezado-cantitos {
    text-align: center;

    margin-bottom: 4mm;
}

.encabezado-cantitos h2 {
    margin: 0;

    font-size: 29px;

    color: #d6339a;

    font-weight: 900;

    letter-spacing: 2px;
}

.encabezado-cantitos p {
    margin: 3px 0 0;

    color: #5a189a;

    font-weight: bold;

    font-size: 15px;
}


/* =====================================================
   CARTONCITOS MÁS PEQUEÑOS
===================================================== */

.grid-cantitos {
    display: grid;

    grid-template-columns: repeat(4, 1fr);

    grid-template-rows: repeat(4, 1fr);

    gap: 4px;

    height: 250mm;
}


/* =====================================================
   CARTONCITO INDIVIDUAL
===================================================== */

.cartoncito {
    background: rgba(255,255,255,0.97);

    border: 3px dashed;

    border-radius: 8px;

    padding: 2px;

    display: flex;

    justify-content: center;

    align-items: center;

    overflow: hidden;
}

.cartoncito img {
    width: 100%;

    height: 100%;

    object-fit: contain;

    display: block;
}


/* =====================================================
   LA MISS GT
===================================================== */

.marca {
    position: absolute;

    right: 9mm;

    bottom: 5mm;

    font-family:
        "Brush Script MT",
        "Segoe Script",
        cursive;

    font-size: 19px;

    font-weight: bold;

    color: #e83eac;
}


/* =====================================================
   IMPRESIÓN
===================================================== */

@media print {

    body {
        background: white;
        margin: 0;
        padding: 0;
    }

    .panel {
        display: none !important;
    }

    .titulo-resultado {
        display: none !important;
    }

    .pagina-carton,
    .pagina-cantitos {
        margin: 0;

        box-shadow: none;

        page-break-after: always;

        break-after: page;
    }

    @page {
        size: A4 portrait;
        margin: 0;
    }
}


/* =====================================================
   VISTA EN CELULAR
===================================================== */

@media (max-width: 700px) {

    .panel {
        width: 94%;
        padding: 18px;
    }

    .titulo-principal {
        font-size: 25px;
    }

    .pagina-carton,
    .pagina-cantitos {
        transform: scale(0.45);

        transform-origin: top center;

        margin-bottom: -160mm;
    }

}

</style>
</head>


<body>


<!-- =====================================================
     PANEL
===================================================== -->

<div class="panel">

    <h1 class="titulo-principal">
        🎴 GENERADOR DE LOTERÍA 🎴
    </h1>

    <p class="descripcion">
        Crea tus cartones y cartoncitos para cantar.
    </p>


    <div class="grupo">

        <label for="titulo">
            Título de la lotería:
        </label>

        <input
            type="text"
            id="titulo"
            placeholder="Ejemplo: Lotería de los animales"
        >

    </div>


    <div class="grupo">

        <label for="cantidadCartones">
            ¿Cuántos cartones deseas generar?
        </label>

        <input
            type="number"
            id="cantidadCartones"
            min="1"
            value="4"
        >

    </div>


    <div class="grupo">

        <label for="imagenes">
            Sube todas las imágenes de tu lotería:
        </label>

        <input
            type="file"
            id="imagenes"
            accept="image/*"
            multiple
        >

    </div>


    <div id="listaImagenes"></div>


    <div class="botones">

        <button
            class="btn-generar"
            id="btnGenerar"
            onclick="generarLoteria()">

            🎴 GENERAR LOTERÍA

        </button>


        <button
            class="btn-pdf"
            id="btnPDF"
            onclick="guardarComoPDF()"
            style="display:none;">

            📄 GUARDAR COMO PDF

        </button>

    </div>

</div>


<!-- =====================================================
     RESULTADO
===================================================== -->

<div id="resultado">

    <div class="titulo-resultado">

        🎉 ¡TU LOTERÍA ESTÁ LISTA! 🎉

        <br>

        <span style="
            font-size:15px;
            color:#777;
            font-weight:normal;
        ">
            Revisa tus cartones y cartoncitos antes de guardarlos.
        </span>

    </div>


    <div id="documentoLoteria"></div>

</div>


<script>

/* =====================================================
   VARIABLES
===================================================== */

let imagenes = [];


/* =====================================================
   COLORES
===================================================== */

const coloresBordes = [

    "#ff4d6d",
    "#ff922b",
    "#ffd43b",
    "#69db7c",
    "#38d9a9",
    "#22b8cf",
    "#4dabf7",
    "#748ffc",
    "#9775fa",
    "#da77f2",
    "#f783ac",
    "#e64980"

];


/* =====================================================
   SUBIR IMÁGENES
===================================================== */

document
.getElementById("imagenes")
.addEventListener("change", function(event) {

    const archivos =
        Array.from(event.target.files);

    imagenes = [];


    archivos.forEach(
        (archivo, indice) => {

            const url =
                URL.createObjectURL(
                    archivo
                );


            let nombre =
                archivo.name
                .replace(
                    /\.[^/.]+$/,
                    ""
                )
                .replace(
                    /[_-]/g,
                    " "
                );


            imagenes.push({

                id: indice,

                url: url,

                nombre:
                    nombre.toUpperCase()

            });

        }
    );


    mostrarImagenes();

});


/* =====================================================
   MOSTRAR IMÁGENES
===================================================== */

function mostrarImagenes() {

    const contenedor =
        document.getElementById(
            "listaImagenes"
        );


    contenedor.innerHTML = "";


    imagenes.forEach(
        (item, indice) => {

            const div =
                document.createElement(
                    "div"
                );


            div.className =
                "imagen-control";


            div.innerHTML = `

                <img
                    src="${item.url}"
                    alt=""
                >

                <input
                    type="text"
                    value="${escaparHTML(item.nombre)}"
                    placeholder="Nombre de la imagen"
                >

            `;


            const input =
                div.querySelector(
                    "input"
                );


            input.addEventListener(
                "input",
                function() {

                    imagenes[indice].nombre =
                        this.value.toUpperCase();

                }
            );


            contenedor.appendChild(
                div
            );

        }
    );

}


/* =====================================================
   MEZCLAR
===================================================== */

function mezclar(array) {

    const nuevo =
        [...array];


    for (
        let i = nuevo.length - 1;
        i > 0;
        i--
    ) {

        const j =
            Math.floor(
                Math.random() *
                (i + 1)
            );


        [
            nuevo[i],
            nuevo[j]
        ] =
        [
            nuevo[j],
            nuevo[i]
        ];

    }


    return nuevo;

}


/* =====================================================
   IDENTIFICAR CARTÓN
===================================================== */

function firmaCarton(carton) {

    return carton
        .map(
            item => item.id
        )
        .join("-");

}


/* =====================================================
   GENERAR LOTERÍA
===================================================== */

function generarLoteria() {

    if (imagenes.length < 12) {

        alert(
            "Debes subir al menos 12 imágenes para crear los cartones."
        );

        return;

    }


    const cantidad =
        parseInt(
            document.getElementById(
                "cantidadCartones"
            ).value
        );


    if (
        !cantidad ||
        cantidad < 1
    ) {

        alert(
            "Indica cuántos cartones deseas generar."
        );

        return;

    }


    const titulo =
        document
        .getElementById("titulo")
        .value
        .trim()
        ||
        "Mi Lotería";


    const documento =
        document.getElementById(
            "documentoLoteria"
        );


    documento.innerHTML = "";


    /* -----------------------------------------
       CARTONES
    ----------------------------------------- */

    const cartonesUsados =
        new Set();


    for (
        let numero = 1;
        numero <= cantidad;
        numero++
    ) {

        let carton;

        let firma;

        let intentos = 0;


        do {

            carton =
                mezclar(imagenes)
                .slice(0, 12);


            firma =
                firmaCarton(carton);


            intentos++;

        } while (

            cartonesUsados.has(firma)

            &&

            intentos < 1000

        );


        cartonesUsados.add(firma);


        const pagina =
            crearPaginaCarton(
                carton,
                titulo,
                numero
            );


        documento.appendChild(
            pagina
        );

    }


    /* -----------------------------------------
       CARTONCITOS
    ----------------------------------------- */

    const grupos =
        dividirEnGrupos(
            imagenes,
            16
        );


    grupos.forEach(
        (grupo, indice) => {

            const pagina =
                crearPaginaCantitos(
                    grupo,
                    titulo,
                    indice + 1
                );


            documento.appendChild(
                pagina
            );

        }
    );


    /* -----------------------------------------
       MOSTRAR RESULTADO
    ----------------------------------------- */

    document.getElementById(
        "resultado"
    ).style.display =
        "block";


    /* -----------------------------------------
       MOSTRAR BOTÓN PDF
    ----------------------------------------- */

    document.getElementById(
        "btnPDF"
    ).style.display =
        "inline-block";


    /* -----------------------------------------
       DESPLAZAR AL RESULTADO
    ----------------------------------------- */

    setTimeout(
        function() {

            document
            .getElementById(
                "resultado"
            )
            .scrollIntoView({

                behavior: "smooth"

            });

        },
        100
    );

}


/* =====================================================
   CREAR CARTÓN
===================================================== */

function crearPaginaCarton(
    carton,
    titulo,
    numero
) {

    const pagina =
        document.createElement(
            "div"
        );


    pagina.className =
        "pagina-carton";


    const encabezado =
        document.createElement(
            "div"
        );


    encabezado.className =
        "encabezado-carton";


    encabezado.innerHTML = `

        <h2>
            LOTERÍA
        </h2>

        <div class="titulo-carton">
            ${escaparHTML(titulo)}
        </div>

    `;


    pagina.appendChild(
        encabezado
    );


    const tablero =
        document.createElement(
            "div"
        );


    tablero.className =
        "tablero";


    carton.forEach(
        (item, indice) => {

            const casilla =
                document.createElement(
                    "div"
                );


            casilla.className =
                "casilla";


            casilla.style.borderColor =
                coloresBordes[
                    indice %
                    coloresBordes.length
                ];


            casilla.innerHTML = `

                <img
                    src="${item.url}"
                    alt=""
                >

            `;


            tablero.appendChild(
                casilla
            );

        }
    );


    pagina.appendChild(
        tablero
    );


    const marca =
        document.createElement(
            "div"
        );


    marca.className =
        "marca";


    marca.textContent =
        "La Miss GT";


    pagina.appendChild(
        marca
    );


    return pagina;

}


/* =====================================================
   CREAR CARTONCITOS
===================================================== */

function crearPaginaCantitos(
    grupo,
    titulo,
    numero
) {

    const pagina =
        document.createElement(
            "div"
        );


    pagina.className =
        "pagina-cantitos";


    const encabezado =
        document.createElement(
            "div"
        );


    encabezado.className =
        "encabezado-cantitos";


    encabezado.innerHTML = `

        <h2>
            CARTONCITOS PARA CANTAR
        </h2>

        <p>
            ${escaparHTML(titulo)}
        </p>

    `;


    pagina.appendChild(
        encabezado
    );


    const grid =
        document.createElement(
            "div"
        );


    grid.className =
        "grid-cantitos";


    grupo.forEach(
        (item, indice) => {

            const tarjeta =
                document.createElement(
                    "div"
                );


            tarjeta.className =
                "cartoncito";


            tarjeta.style.borderColor =
                coloresBordes[
                    indice %
                    coloresBordes.length
                ];


            tarjeta.innerHTML = `

                <img
                    src="${item.url}"
                    alt=""
                >

            `;


            grid.appendChild(
                tarjeta
            );

        }
    );


    pagina.appendChild(
        grid
    );


    const marca =
        document.createElement(
            "div"
        );


    marca.className =
        "marca";


    marca.textContent =
        "La Miss GT";


    pagina.appendChild(
        marca
    );


    return pagina;

}


/* =====================================================
   DIVIDIR EN GRUPOS
===================================================== */

function dividirEnGrupos(
    array,
    tamaño
) {

    const grupos = [];


    for (
        let i = 0;
        i < array.length;
        i += tamaño
    ) {

        grupos.push(
            array.slice(
                i,
                i + tamaño
            )
        );

    }


    return grupos;

}


/* =====================================================
   GUARDAR COMO PDF
===================================================== */

function guardarComoPDF() {

    const documento =
        document.getElementById(
            "documentoLoteria"
        );


    if (
        !documento.innerHTML.trim()
    ) {

        alert(
            "Primero debes generar la lotería."
        );

        return;

    }


    window.print();

}


/* =====================================================
   ESCAPAR HTML
===================================================== */

function escaparHTML(texto) {

    return String(texto)

        .replace(
            /&/g,
            "&amp;"
        )

        .replace(
            /</g,
            "&lt;"
        )

        .replace(
            />/g,
            "&gt;"
        )

        .replace(
            /"/g,
            "&quot;"
        )

        .replace(
            /'/g,
            "&#039;"
        );

}

</script>

</body>
</html>
