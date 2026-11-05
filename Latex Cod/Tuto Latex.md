Para un trabajo práctico de programación, la estructura clave de LaTeX se basa en utilizar **paquetes** específicos para incrustar código fuente con colores, insertar diagramas lógicos y escribir fórmulas matemáticas o análisis de complejidad.

  

Aquí tienes los comandos fundamentales y la configuración exacta que necesitas.

  

### 1. Comandos de Estructura y Texto

- **Secciones:** Organizan el documento automáticamente y arman el índice.
    
      
    - `\section{Nombre de la sección}` (ej: Introducción, Desarrollo)
        
    - `\subsection{Subtítulo}`

- **Formato de texto:**
    
      
    - `\textbf{texto}` para **negrita**.
        
    - `\textit{texto}` para _cursiva_.
        
    - `\texttt{texto}` para tipografía de código en línea (ideal para nombrar variables como `int contador`).
        
- **Listas:**
    
      
    
    Fragmento de código
    
    ``` tex
    \begin{itemize}
        \item Primer punto de la lista.
        \item Segundo punto.
    \end{itemize}
    ```
    

### 2. Insertar Código Fuente (El paquete `listings`)

Para que tu código en Java, C, Python o SQL se formatee correctamente con colores y números de línea, debes cargar el paquete `\usepackage{listings}` en la parte superior del documento (preámbulo) y usar este entorno dentro del texto:

  

Fragmento de código

```latex
\begin{lstlisting}[language=Java]
public class Jugador {
    private int vida;
    
    public Jugador() {
        this.vida = 100;
    }
}
\end{lstlisting}
```

### 3. Fórmulas Matemáticas y Lógica

Si necesitas justificar la complejidad de un algoritmo, plantear ecuaciones de probabilidad o expresiones de álgebra booleana, usas el modo matemático.

  

- **En la misma línea de texto:** Lo encierras entre signos de dólar `$ O(n \log n) $`.
    
      
    
- **Ecuación centrada en una nueva línea:** Lo encierras entre dos signos de dólar:
    
      
    
    Fragmento de código
    
    ```
    $$ f(x, y) = x \cdot \overline{y} + z $$
    ```
    

### Plantilla Completa para tu TP

Copia y pega este código en tu archivo `TP.tex`. Ya tiene configurado el idioma, los márgenes, y un estilo visual profesional para bloques de código que te servirá de base para cualquier entrega.

Fragmento de código

```latex
\documentclass[11pt,a4paper]{article}

% --- PAQUETES BÁSICOS ---
\usepackage[utf8]{inputenc}
\usepackage[spanish]{babel}
\usepackage{amsmath} % Para matemáticas avanzadas
\usepackage{graphicx} % Para insertar imágenes (diagramas de memoria, circuitos)
\usepackage{xcolor} % Para colores personalizados
\usepackage{geometry} % Para ajustar los márgenes
\geometry{top=2.5cm, bottom=2.5cm, left=2.5cm, right=2.5cm}

% --- CONFIGURACIÓN DE CÓDIGO (Listings) ---
\usepackage{listings}
\lstset{
    backgroundcolor=\color{black!5}, % Fondo gris claro
    basicstyle=\ttfamily\small,      % Tipografía de código
    keywordstyle=\color{blue}\bfseries, % Palabras reservadas en azul
    commentstyle=\color{green!50!black}, % Comentarios en verde
    stringstyle=\color{red},         % Strings en rojo
    showstringspaces=false,
    frame=single,                    % Borde alrededor del código
    numbers=left,                    % Números de línea a la izquierda
    numberstyle=\tiny\color{gray},
    breaklines=true                  % Cortar líneas muy largas automáticamente
}

% --- PORTADA ---
\title{Trabajo Práctico: [Nombre del TP]}
\author{Tu Nombre - Padrón: [Tu Número]}
\date{\today}

\begin{document}

\maketitle
\tableofcontents % Genera un índice automático
\newpage

\section{Introducción}
En este trabajo práctico se implementa el diseño lógico y las estructuras de datos necesarias para resolver el problema planteado. La variable \texttt{estadoActual} controla el flujo principal.

\section{Implementación}
A continuación se presenta el fragmento principal desarrollado en Java:

\begin{lstlisting}[language=Java]
// Método principal de inicialización
public void iniciarJuego() {
    System.out.println("Cargando base de datos...");
    conexionBD();
}
\end{lstlisting}

\section{Análisis de Rendimiento}
La probabilidad de colisión en la tabla hash o el cálculo de la varianza se define como:
$$ P(A \cup B) = P(A) + P(B) - P(A \cap B) $$

\end{document}
```