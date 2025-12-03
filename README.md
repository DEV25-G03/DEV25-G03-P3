# DEV25-G03-P3
Repositorio creado por el gruopo G03 para el proyecto de pringa veletas

# Punto de partida
El punto de partida es la [plantilla](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-templates-reference?application_version=5.6) First Person que ofrece Unreal Engine con la variante Arena Shooter, que recrea un mundo 3D con vista en primera persona, la mecánica del disparo y cambio de arma, y dos personajes inteligentes enemigos. Además se podrá usar contenido del paquete Starter Content, la biblioteca de Quixel [Megascans](https://quixel.com/megascans) y otros recursos gratuitos de [Fab](https://www.fab.com/) como [Modular SciFi Season 1 Starter Bundle](https://www.fab.com/listings/86913335-3c75-42bf-8404-54fe9d9d7396) y [Modular Scifi Season 2 Starter Bundle](https://www.fab.com/listings/cb3c4494-4060-4a80-b079-e46936cb8dd0).

# Pringa Veletas
Este proyecto consiste en desarrollar el prototipo ejecutable de un videojuego de disparos 3D para un sólo jugador que consiste en «pringar» (disparar pintura pringosa) «veletas» (objetivos con cierto movimiento de rotación), manteniendo interacciones tanto competitivas como colaborativas con otros personajes del equipo propio o el equipo rival que también se mueven y disparan como nosotros. 

Las características principales del prototipo son:

<ol type="A">
  <li>
    Hay un mundo virtual consistente en un nivel principal que representa una «arena de combate» con distintos obstáculos y localizaciones. Cada vez que empieza el juego cuatro participantes, dos por cada equipo (equipo rojo y equipo azul), aparecen aleatoriamente en distintos puntos de la arena, así como una serie de 9 objetivos (veletas) que también pueden aparecer en distintas localizaciones y otros recursos como armas, recargas de munición y «duchas». Hay un menú al inicio y otro al final de la partida.
   <br><br>
  </li>
  <li>
    Nuestro protagonista interactúa con distintos objetos, como armas, recargas de munición, duchas y veletas. Hay tres tipos de arma: pistola, rifle y lanzagranadas… siendo cada una más poderosa que la anterior en cuanto a la capacidad de «pringar» (dañar) veletas y otros jugadores, pero también más lenta y de munición más escasa y valiosa. Sobre la pantalla se mostrará un resumen del inventario del protagonista y cuando se selecciona un arma también se mostrará la munición restante.
   <br><br>
  </li>
  <li>
   Las veletas, al igual que los demás personajes, muestran una barra encima de ellos que indica cómo de pringados están. Según la veleta se va pringando se mueve a menor velocidad y cuando está muy pringada se para totalmente, cambiando su color al del equipo del último jugador que la disparó y contando como 1 punto para dicho equipo. Cuando un equipo ha parado 5 veletas se declara vencedor de la roda y el nivel con todo su contenido vuelve a reiniciarse. En la pantalla también hay un cronómetro que nos indica cuanto queda de los 5 minutos que dura el partido completo, más las rondas ganadas y las veletas paradas en esta ronda por cada equipo. El jugador que controlamos, como decíamos, puede quedarse incapacitado para disparar si está muy pringado, aunque los jugadores tienen mucha más resistencia al pringue que las veletas.
   <br><br>
  </li>
  <li>
   Los enemigos buscan los objetivos más interesantes por el nivel, generalmente veletas que tienen cerca pero a veces también nos atacan a nosotros o al otro jugador de nuestro equipo. Con su comportamiento inteligente son capaces de detectar (mediante percepción visual o sonora, si hay algún otro jugador cerca), saben el nivel de pringue de cada objetivo y pueden perseguir, huir y hasta disparar desde cierta distancia a las veletas o los jugadores hasta pringarlos del todo.
   <br><br>
  </li>
  <li>
   El juego es fácil de superar (solemos ganar) si sabemos equilibrar el disparar veletas con lanzar alguna granada o algo así de contundente a enemigos que estén a punto de llevarse nuestra puntuación. Sin embargo, se vuelve difícil (solemos perder) si jugamos de manera imprudente, sin mucho criterio o si no me coordino bien con mi compañero.
  </li>
</ol>

# Instalación y uso

Los ficheros más importantes del proyecto están disponible en este repositorio, aunque puede que algunos binarios potencialmente grandes estén en el almacén GitHub LFS y se requiera tener activa la extensión Git LFS. El resto de los ficheros, generalmente de contenido más pesado o creado por terceros y sin intención de ser modificado en este proyecto, tendrá que descargarse de carpetas compartidas en [Google Drive](https://drive.google.com/drive/folders/1TfoB5S3yQw49-onoFfn0q79PTfk2RoSE) con ficheros ZIP, para después descomprirlos directamente en la carpeta Content.

Para este proyecto hace falta descargar los ficheros ZIP:

- Characters
- LevelPrototyping
- ThirdPerson
- Variant_Platforming

Y luego extraerlos dentro del archivo **Content**
 
# Preproducción

El diseño tiene estas secciones:

- [Estetica](#Estetica)
    - [Grafico](#Grafico)
    - [Sonido](#Sonido)
- [Dinamica](#Dinamica)
    - [Objetivo](#Objetivo)
    - [Castigo](#Castigo)
- [Mecanica](#Mecanica)
- [Contenido](#Contenido)
    - [Zona A](#Zona-A)
    - [Zona B](#Zona-B)
    - [Zona C](#Zona-C)

# Estetica

El entorno virtual se basa en la plantilla First Person que ofrece Unreal Engine con la variante Arena Shooter, que recrea un mundo 3D con vista en primera persona; además se incluye el contenido del paquete Starter Content. 

## Grafico

El juego usa solamente el contenido de la plantilla proporcinada por el profesor.

## Sonido

Debido a la falta de tiempo, hemos decidido a no implenmentar sonido en este poyecto.

# Dinamica

La dinamica del juego consiste en moverse por una arena 3D pringando veletas y enfrentandose a enemigos mientras se gestionan armas, municion y limpieza; el jugador y los personajes IA (enemigos) compiten y colaboran para detener veletas antes que el equipo rival, equilibrando ataque, defensa y uso estrategico del entorno para obtener ventaja en cada ronda. 

```mermaid
flowchart TD
    %% --- Inicio ---
    A0([<b>INICIO</b>])

    %% --- Menu Inicio ---
    M1[Menu Inicio]
    M2{¿jugador = rojo?}
    M3[Equipo jugador = rojo<br> Equipo enemigo = azul]
    M4[Equipo jugador = azul<br> Equipo enemigo = rojo]

    A0 --> M1
    M1 --> M2
    M2 --> |SI| M3
    M2 --> |NO| M4

    %% --- Arena ---
    AC0([Arena de combate])

    M3 --> AC0
    M4 --> AC0
 
    %% --- Generación ---
    A1[Equipo enemigo]
    A2[Objetivos<br> 9 veletas]
    A3[Recursos<br>armas, munición, duchas]
    A4[Equipo jugador]

    AC0 --> A1
    AC0 --> A2
    AC0 --> A3
    AC0 --> A4

    %% --- Jugador ---
    J1{¿Veleta o enemigo?}
    J2[Perseguir]
    J3[Disparo]
    J4[Incrementa pringue de enemigo o veleta]

    A4 --> J1 --> J2 --> J3 --> J4 --> V1

    %% --- Enemigo ---
    P1[Inventario de armas]
    P2[Elegir arma<br>rifle/lanzagranadas]
    P3{¿Tiene<br> Munición?}
    P4[Disparo]
    P5{¿Jugador pringado?}
    P6[Ir a ducha<br>recuperar limpieza]

    AC0 --> P1
    P1 --> P2 --> P3
    P3 -- Sí --> P4 --> P5
    P5 -- Sí --> P6 --> P1
    P3 -- No --> P1
    P5 -- No --> P1

    %% --- Veletas ---
    V1[Veleta<br>barra de pringue]
    V2[Recibe disparos]
    V3{¿Veleta parada?}
    V4[Se pinta del color del equipo]
    V5[+1 punto para equipo]
    V6{¿Equipo tiene 5?}
    V7([Victoria de ronda])

    A2 --> V1
    P4 --> V2
    V2 --> V1 --> V3
    V3 -- Sí --> V4 --> V5 --> V6
    V3 -- No --> V1
    V6 -- Sí --> V7

    %% --- IA enemiga ---
    E1[IA detecta objetivo<br>visión/sonido]
    E2{¿Veleta o jugador?}
    E3[Perseguir]
    E4[Disparo]
    E5[Incrementa pringue de jugador o veleta]

    A1 --> E1
    E1 --> E2 --> E3 --> E4 --> E5
    E5 --> V1
    E5 --> P5

    %% --- Menu Fin ---
    F1([Menu Fin])
    V7 --> F1

    %% --- Menu Fin ---
    R1([reinicio arena])

    F1 --> R1
```

## Objetivo

El objetivo principal es tener que parar las veletas hasta alcanzar un maximo de parado de 5 veletas para declararse vencedor de la ronda.

## Castigo

El castigo en el juego es quedar incapacitado para disparar cuando el jugador recibe demasiado pringue; en ese estado no puede defenderse ni puntuar hasta encontrar una ducha para limpiarse, lo que lo deja vulnerable y retrasa a su equipo. Tambien, inderectamente, perder una veleta frente al rival funciona como castigo estrategico.

# Contenido

A continuación se muestra los componentes del juego.

## Avatar jugador (caracter controlado por el jugador)

El clásico maniquí de Unreal Engine que se puede mover y saltar, es el avatar que controla el jugador, y empieza con el valor de limpieza de +20.

## Avatar enemigo (caracter controlado por la IA)

El clásico maniquí de Unreal Engine que se puede mover y saltar, es el avatar que se controla a travez de una Inteligencia artificial, la cual representa al enemigo que debe competir contra el jugador, y empieza con el valor de limpieza de +20.

## Armas 

Son los recursos con lo que cuenta el jugador para causar daño. las armas del tipo pistola, rifle y lanzagranada, cada una con un nivel de impacto distinto, el cual se menciona a continuacion:

* Pistola, la cual causa un daño de -1.
* Rifle, la cual causa un daño de -2.
* Lanzagranada, la cual causa un daño de -5.

## Veletas

Son los objetos identificados como los objetivo principales a parar en el juego, inicialmente inicia con el valor de limpieza de +20.

## Municion

Son los recursos con los que cuenta el jugador para recargar la cantidad de su armamento.

## Duchas

Es el area destinada a la limpieza del jugador, cuando este este totalmente pringado. 

# Contenido

A continuación se muestran las distintas instancias del juego.

## Instacia Menu Inicio

La primera zona del juego es un exterior con agua y consiste en cruzar el foso del castillo dando saltos sobre gruesos troncos que flotan sobre el agua, moviéndose lentamente bajo nuestros pies. Si el avatar cae al agua, muere pero reaparece al principio

```mermaid
flowchart LR
    %% --- Inicio ---
    A0([<b>INICIO</b>])

    %% --- Menu Inicio ---
    M1[Menu Inicio]
    M2{¿jugador = rojo?}
    M3[Equipo jugador = rojo<br> Equipo enemigo = azul]
    M4[Equipo jugador = azul<br> Equipo enemigo = rojo]

    A0 --> M1
    M1 --> M2
    M2 --> |SI| M3
    M2 --> |NO| M4

    %% --- Arena ---
    AC0([Arena de combate])

    M3 --> AC0
    M4 --> AC0
```

## Zona B

La segunda zona consiste en escalar la muralla del castillo aprovechando sus salientes, siendo necesario el uso de pastillas para saltar entre ciertas plataformas. Aunque prime la verticalidad, conviene dividir la escalada en partes, de modo que si el avatar cae, sólo tiene que repetir la escalada de la última parte. Algún saliente estará dañado y se romperá si el avatar lo pisa.

```mermaid
flowchart LR
    D["La muralla del castillo"] --> n1["Escalares o truncos que direge hacia la correzáon el castillo"]
    n1 --> n2["El corrazón del castillo"]
```

## Zona C

La tercera y última zona es un interior y consiste en atravesar las estancias interiores hasta el corazón del castillo, con varias puertas y algunas trampas. No hay “enemigos” como tales, sólo objetos con movimiento que resultan molestos e incluso mortales para el jugador, y las llaves de las puertas mencionadas anteriormente. Si el avatar muere, será necesario repetir la zona. Finalmente al coger el gran lingote dorado en el interior del castillo, la partida termina.

```mermaid
flowchart LR
    n2["El corrazón del castillo"] --> n3["Laberinto"]
    n3 --> n4["El gran lingote dorado, dentro de todo"]
```

# Referencia

[Fūun! Takeshi Jō]( https://narratech.com/es/desarrollo-de-videojuegos-25-26/)

[Castle - Base](https://github.com/narratech/castle-base)

# Video demo

Puede verse en el siguiente enlace de youtube:


Puede descargarse en el siguiente enlace:



