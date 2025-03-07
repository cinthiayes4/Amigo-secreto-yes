
File: README.md

Juego del amigo secetro

Descripción
Este es un sencillo juego web del Amigo Secreto, desarrollado con JavaScript, HTML y CSS. Permite a un grupo de personas ingresar sus nombres y realizar un sorteo aleatorio para asignar a cada uno un amigo secreto.
📝 Características
✅ Agregar nombres a la lista de participantes.
✅ Evita nombres duplicados.
✅ Sorteo del amigo secreto
✅ Posibilidad de reiniciar el juego para hacer un nuevo sorteo.

Instrucciones
- Agrega los nombres de los participantes en el campo de texto y haz clic en "Añadir" para ir construyendo la lista.
Una vez que hayas ingresado todos los nombres, haz clic en "Sortear Amigo" para que el sistema asigne un amigo secreto a cada participante.
- El resultado del sorteo se mostrará en pantalla.
Para volver a jugar, haz clic en "Volver a jugar".

Capturas de Pantalla
Pantalla de inicio del amigo secreto
![{D8C59CD0-2B14-40A2-9456-0770FB69CEE0}](https://github.com/user-attachments/assets/8ac346c8-3281-42ee-93ae-effc9e5aa704)
2. Escribir el nombre del participante y click en añadir:
![{B96CC6A8-3C6C-4C8D-901E-7E62B7D09283}](https://github.com/user-attachments/assets/f72d343b-9d58-4162-b992-9f3f8cc0d5f3)
3. El programa añadira el nombre a una lista en la parte inferior. Repetir el este paso cuantas veces sea necesario.
![{159D4356-FFA9-4F22-81E0-EE2178D288D5}](https://github.com/user-attachments/assets/d31341ac-cfb6-4551-a98b-232d2d43c4a5)
4. Una vez terminada la lista click en sortear amigo secreto.
![{5D075189-0F3D-4289-A34E-061B8D6942A9}](https://github.com/user-attachments/assets/e026b96d-1e28-463f-84b4-b92901d7bd79)
5. El programa devolvera el nombre del amigo secreto sorteado. 
![{C9FE028E-0875-4213-ACEB-BA2CB92F292A}](https://github.com/user-attachments/assets/07a134d0-c049-4569-a3a0-6443b5dc7f0a)
6. Si desea volver a jugar click en "Volver a jugar" y el programa reiniciara el juego. 
![{45820E1E-B8F8-41EA-8513-42DFC54550D1}](https://github.com/user-attachments/assets/918d3c5c-f6e5-42bf-b905-a6499d512510)


Tecnologías Utilizadas
- JavaScrip- HTML
- CSS
  



File: app.js

// El principal objetivo de este desafío es fortalecer tus habilidades en lógica de programación. Aquí deberás desarrollar la lógica para resolver el problema.
let numSorteado = 0;
let listaDeAmigos = [];
let listaNumSorteados = [];

// function de asisgnar texto al elemento 
function asignarTextoElementoLista(elemento,lista){
    let elementoHTML = document.querySelector(elemento);
    let listaHTML = "";
    for (let item of lista) {
        listaHTML += `<li>${item}</li>`;
    }
    elementoHTML.innerHTML = listaHTML;
    return;
}

function asignarTextoElemento(elemento, texto) {
    let elementoHTML = document.querySelector(elemento);
    elementoHTML.innerHTML = texto;
    return;
  }

// usar despues de añadir para limpiar la caja 
function limpiarCaja(cajaElemento,texto){
    // document.querySelector('#amigo').value = '';
    let elementoCaja = document.querySelector(cajaElemento);
   // document.querySelector(cajaElemento).value = "";
   elementoCaja.innerHTML = texto;
    return;
}

// Creando la lista de amigo que se sortearan 
function agregarAmigo(){

    if(document.getElementById('amigo').value != ''){
        let verificar = document.getElementById('amigo').value;
        if(listaDeAmigos.includes(verificar)){
            alert('Este nombre ya existe');
        }else{
            listaDeAmigos.push(document.getElementById('amigo').value); 
        
            //cambia el valor del input Lo limpia
            let miInput = document.querySelector("#amigo");
            miInput.value = "";
            asignarTextoElementoLista('ul',listaDeAmigos);
        }      

        }
        else{
        alert("Debe colocar el nombre de un amigo para el sorteo");
        }
}

// MOSTRAR AMIGOS SECRETOS EN EL UL 
function sortearAmigo(){
    
    // ENCONTRAR EL N TOTAL DE LA LISTA 
    let numLista = listaDeAmigos.length;
    if(numLista!=0){
    // GENERAR UN NUMERO ALEATORIO ENTRE 0 A N  
    numSorteado = Math.floor(Math.random()*numLista);
        if(listaNumSorteados.length == numLista){
            alert('Ya se sortearon todas los amigos secretos posibles');

        }else{
            if(listaNumSorteados.includes(numSorteado)){
                return sortearAmigo();
            }else{
                console.log(numSorteado);
                // ESE NUMERO SERA EL INDICE DE LA LISTA 
                
                listaNumSorteados.push(numSorteado);
                limpiarCaja("#listaAmigos","");
                asignarTextoElemento('#resultado', `El amigo secreto sorteado es: ${listaDeAmigos[numSorteado]}`);
            document.getElementById('reiniciar').removeAttribute('disabled');
               
             }
        
         }
    
    }else{
        alert('No se puede sortear porquue no ha ingresado nombres');
    }
    return;
   
}


function condicionesIniciales(){
    numSorteado = 0;
    listaDeAmigos = [];
    listaNumSorteados = [];
    limpiarCaja("#listaAmigos","");
    asignarTextoElemento('#resultado','');

}

function reiniciarJuego(){
    condicionesIniciales();
    document.querySelector('#reiniciar').setAttribute('disabled','true');
}









File: index.html

<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="style.css">
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@100;400;700;900&family=Merriweather:ital,wght@0,300;0,400;0,700;0,900;1,300;1,400;1,700;1,900&display=swap" rel="stylesheet">
    <title>Amigo Secreto</title>
</head>

<body>
    <main class="main-content">
        <header class="header-banner">
            <h1 class="main-title">Amigo Secreto</h1>
            <img src="assets/amigo-secreto.png" alt="Imagen representativa de amigo secreto">
        </header>
        
        <section class="input-section">
            <h2 class="section-title">Digite el nombre de sus amigos</h2>
            <div class="input-wrapper">
                <input type="text" id="amigo" class="input-name" placeholder="Escribe un nombre">
                <button class="button-add" onclick="agregarAmigo();">Añadir</button>
            </div>
           
            <ul id="listaAmigos" class="name-list" aria-labelledby="listaAmigos" role="list"></ul>
            <ul id="resultado" class="result-list" aria-live="polite"></ul>

            <div class="button-container">
                <button class="button-draw" onclick="sortearAmigo();" aria-label="Sortear amigo secreto">
                    <img class="imagen__boton" src="assets/play_circle_outline.png" alt="Ícono para sortear">
                    Sortear amigo
                </button>
                <button class="button_reset" id="reiniciar" onclick="reiniciarJuego();" aria-label="Reiniciar juego" disabled>
                    <img class="imagen__boton" src="assets/icon_reiniciar.png"  alt="Ícono para sortear">
                    Volver a jugar
                </button>
            </div>
        </section>
    </main>

    <script src="app.js" defer></script>
</body>
</html>


================================================
File: style.css
================================================
:root {
    --color-primary: #257180;
    --color-secondary: #F2E5BF;
    --color-tertiary: #FD8B51;
    --color-button: #C5705D;
    --color-button-hover: #e55720;
    --color-text: #444444;
    --color-white: #FFFFFF;
}

/* Estilos generales */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    height: 100vh;
    background-color: var(--color-primary);
    display: flex;
    justify-content: center;
    align-items: center;
}

.main-content {
    display: flex;
    flex-direction: column;
    height: 100%;
    width: 100%;
}

/* Banner */
.header-banner {
    flex: 40%;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 40px 0 0;
}

/* Sección de entrada */
.input-section {
    flex: 60%;
    background-color: var(--color-secondary);
    border: 1px solid #000;
    border-radius: 64px 64px 0 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 20px;
    width: 100%;
}

/* Títulos */
.main-title {
    font-size: 48px;
    font-family: "Merriweather", serif;
    font-weight: 900;
    font-style: italic;
    color: var(--color-white);
}

.section-title {
    font-family: "Inter", serif;
    font-size: 36px;
    font-weight: 700;
    color: var(--color-primary);
    margin: 10px 0;
    text-align: center;
}

/* Contenedores de entrada y botón */
.input-wrapper {
    display: flex;
    justify-content: center;
    width: 100%;
    max-width: 600px;
    margin-top: 20px;
}

.input-name {
    width: 100%;
    padding: 10px;
    border: 2px solid #000;
    border-radius: 25px 0 0 25px;
    font-size: 16px;
}

.button-container {
    display: flex;
    flex-direction: column;
    width: 300px;
    justify-content: center;
    gap:20px;
}

/* Estilos de entrada de texto */
.input-title {
    flex: 1;
    padding: 10px 15px;
    font-size: 16px;
    border: 2px solid #333;
    border-right: none;
    border-radius: 25px 0 0 25px;
    font-family: "Merriweather", serif;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
}

/* Estilos de botón */
button {
    padding: 15px 30px;
    font-family: "Inter", sans-serif;
    font-size: 16px;
    border: 2px solid #000;
    border-radius: 25px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
    cursor: pointer;
}

.button-add {
    background-color: var(--color-tertiary);
    color: var(--color-text);
    border-radius: 0 25px 25px 0;
}

.button-add:hover {
    background-color: #a1a1a1;
}

.button-add:active{
    background-color: var(--color-tertiary);
    color: var(--color-text);
}

.imagen__boton{
    width: 15%;
    color: #FFFFFF;
}


/* Listas */
ul {
    list-style-type: none;
    color: var(--color-text);
    font-family: "Inter", sans-serif;
    font-size: 18px;
    margin: 20px 0;
}

.result-list {
    margin-top: 15px;
    color: rgb(202, 54, 202);
    font-size: 22px;
    font-weight: bold;
    text-align: center;
}

/* Botón de sortear título */
.button-draw {
    display: flex;
    align-items: center;
    width: 100%;
    padding: 10px 40px;
    color: var(--color-white);
    background-color: var(--color-button);
    font-size: 16px;
}

.button-draw img {
    margin-right: 40px;
}

.button_reset{
    display: flex;
    align-items: center;
    width: 100%;
    padding: 10px 40px;
    color: var(--color-white);
    background-color: var(--color-button);
    font-size: 16px;
}
.button_reset:disabled{
    background-color: #898989;
}

.button_reset:active{
    background-color: var(--color-button-hover);
}

.button_reset img{
    margin-right: 40px;
}

.button-draw:hover {
    background-color: var(--color-button-hover);
}



