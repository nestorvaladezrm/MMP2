[![Open in MATLAB Online](https://www.mathworks.com/images/responsive/global/open-in-matlab-online.svg)](https://matlab.mathworks.com/open/github/v1?repo=nestorvaladezrm/MMP2)
# MMP2
# Práctica 2 — Caos en Sistemas Biológicos

Repositorio académico de la asignatura **Modelado Matemático**, correspondiente a la **Maestría en Ciencias de la Ingeniería** del Tecnológico Nacional de México / Instituto Tecnológico de Tijuana. Esta práctica estudia un sistema dinámico no lineal de tres poblaciones celulares, mediante el análisis de positividad, puntos de equilibrio, estabilidad local, conjuntos compactos invariantes y condiciones de eliminación de células patológicas utilizando el método directo de Lyapunov.

El modelo considera la interacción entre tres poblaciones celulares, representadas por las variables de estado \(x(t)\), \(y(t)\) y \(z(t)\), así como un parámetro de control \(\rho\) que influye en la dinámica de la tercera población.

**Docente:** Dr. Paul Antonio Valle Trujillo  
**Departamento:** Ingeniería Eléctrica y Electrónica  
**Institución:** Tecnológico Nacional de México / Instituto Tecnológico de Tijuana  
**Asignatura:** Modelado Matemático  
**Programa:** Maestría en Ciencias de la Ingeniería

**Alumno:** Valadez Madera Néstor Román. M26210087. m26210087@tectijuana.edu.mx

---

<a id="contenido"></a>
## Contenido

1. [Resumen](#resumen)
2. [Objetivos](#objetivos)
3. [Modelo matemático](#modelo)
4. [Positividad e invariancia](#positividad)
5. [Puntos de equilibrio libres de células patológicas](#equilibrios)
6. [Estabilidad asintótica local](#estabilidad-local)
7. [Conjuntos compactos invariantes](#conjuntos)
8. [Estabilidad asintótica global: condiciones de eliminación](#estabilidad-global)
9. [Actividades de la práctica](#actividades)
10. [Resultados y condiciones principales](#resultados)
11. [Alcance del material y reproducibilidad](#reproducibilidad)
12. [Referencias](#referencias)

---

<a id="resumen"></a>
## Resumen

Esta práctica estudia la dinámica de un sistema biológico compuesto por tres poblaciones celulares. El modelo se describe mediante un sistema de tres ecuaciones diferenciales ordinarias no lineales de primer orden. A partir de su formulación matemática, se analiza si las soluciones permanecen en el octante no negativo, se determinan los puntos de equilibrio en los que se elimina la población de células patológicas y se estudia la estabilidad local mediante la matriz Jacobiana y sus valores propios.

Posteriormente, se construyen conjuntos invariantes para establecer límites inferiores y superiores de las variables de estado. Finalmente, se propone la función candidata de Lyapunov \(V=x\), con el propósito de obtener una condición sobre el parámetro de control \(\rho\) que permita garantizar la eliminación de las células patológicas para condiciones iniciales positivas.

La condición principal de eliminación obtenida mediante el análisis global es

\[
\rho>\frac{r_1d_3}{a_{13}}.
\]

**Palabras clave:** biología matemática; células patológicas; ecuaciones diferenciales ordinarias; estabilidad asintótica; estabilidad de Lyapunov; sistemas dinámicos no lineales; puntos de equilibrio; conjuntos invariantes.

[Volver al contenido](#contenido)

---

<a id="objetivos"></a>
## Objetivos

### Objetivo general

Analizar la dinámica de un sistema biológico de tres poblaciones celulares mediante herramientas de sistemas dinámicos no lineales, con el propósito de establecer condiciones matemáticas para la eliminación de la población de células patológicas.

### Objetivos específicos

- Formular el modelo matemático mediante un sistema de tres ecuaciones diferenciales ordinarias no lineales.
- Analizar la positividad de las soluciones y demostrar la invariancia del octante no negativo.
- Determinar los puntos de equilibrio correspondientes a la ausencia de células patológicas.
- Construir la matriz Jacobiana y calcular los valores propios de los equilibrios de interés.
- Establecer condiciones para la estabilidad asintótica local del equilibrio libre de células patológicas.
- Construir conjuntos invariantes que permitan determinar límites para las variables de estado.
- Aplicar el método directo de Lyapunov para obtener condiciones de eliminación global de la población patológica.
- Interpretar el efecto del parámetro de control \(\rho\) sobre la dinámica del sistema.

[Volver al contenido](#contenido)

---

<a id="modelo"></a>
## Modelo matemático

La dinámica de las tres poblaciones celulares se describe mediante el siguiente sistema de ecuaciones diferenciales ordinarias no lineales de primer orden:

\[
\frac{dx}{dt}
=
r_1x(1-b_1x)-a_{12}xy-a_{13}xz,
\]

\[
\frac{dy}{dt}
=
r_2y(1-b_2y)-a_{21}xy,
\]

\[
\frac{dz}{dt}
=
(r_3-a_{31})xz-d_3z+\rho.
\]

Se considera que todos los parámetros son positivos, que las condiciones iniciales son no negativas y que el parámetro de control satisface \(\rho>0\).

En forma vectorial, el sistema se expresa como

\[
\dot{\boldsymbol{\phi}}
=
\mathbf{F}(\boldsymbol{\phi}),
\qquad
\boldsymbol{\phi}
=
\begin{bmatrix}
x&y&z
\end{bmatrix}^{T}.
\]

Las variables y parámetros se interpretan de la siguiente manera:

| Símbolo | Descripción |
|---|---|
| \(x(t)\) | Población de células patológicas, cuya eliminación es el objetivo del análisis |
| \(y(t)\) | Segunda población celular |
| \(z(t)\) | Tercera población celular |
| \(r_1,r_2\) | Parámetros de crecimiento de las poblaciones \(x\) y \(y\) |
| \(b_1,b_2\) | Parámetros asociados con la limitación del crecimiento de las poblaciones \(x\) y \(y\) |
| \(a_{12},a_{13}\) | Parámetros de interacción que reducen el crecimiento de la población \(x\) |
| \(a_{21}\) | Parámetro de interacción que reduce el crecimiento de la población \(y\) |
| \(r_3\) | Parámetro asociado con la dinámica de la población \(z\) |
| \(a_{31}\) | Parámetro de interacción asociado con la población \(x\) en la ecuación de \(z\) |
| \(d_3\) | Parámetro de eliminación o decaimiento de la población \(z\) |
| \(\rho\) | Parámetro de control positivo que interviene en la dinámica de \(z\) |

La variable \(x(t)\) representa la población que se desea controlar y llevar a cero. Por ello, una parte central del análisis consiste en determinar qué condiciones sobre \(\rho\) permiten que dicha población desaparezca.

[Volver al contenido](#contenido)

---

<a id="positividad"></a>
## Positividad e invariancia del sistema

El significado biológico de las variables requiere que las poblaciones celulares permanezcan no negativas. Para analizar esta propiedad, se evalúa el campo vectorial sobre las fronteras del octante no negativo.

Cuando \(x=0\),

\[
\left.\dot{x}\right|_{x=0}
=
r_1(0)(1-b_1(0))-a_{12}(0)y-a_{13}(0)z
=0.
\]

Cuando \(y=0\),

\[
\left.\dot{y}\right|_{y=0}
=
r_2(0)(1-b_2(0))-a_{21}x(0)
=0.
\]

Cuando \(z=0\),

\[
\left.\dot{z}\right|_{z=0}
=
(r_3-a_{31})x+\rho.
\]

Para que esta expresión sea no negativa para todo \(x\geq0\), se requiere, por ejemplo, que

\[
r_3-a_{31}\geq0,
\]

dado que \(\rho>0\). El documento fuente simplifica esta evaluación a \(\rho\), pero esa simplificación no se cumple para un valor general de \(x\) a menos que \(x=0\) o \(r_3=a_{31}\). Por ello, la demostración de positividad en todo el octante requiere explicitar una condición adicional sobre los parámetros o el dominio.

Bajo la condición \(r_3\geq a_{31}\), el campo vectorial no apunta hacia el exterior del dominio no negativo en sus fronteras.

Se define el octante no negativo como

\[
\mathbb{R}_{+,0}^{3}
=
\left\{
(x,y,z)\in\mathbb{R}^{3}
\mid x\geq0,\;y\geq0,\;z\geq0
\right\}.
\]

**Resultado: Positividad e invariancia en el octante no negativo.**

Sea

\[
\boldsymbol{\phi}(t)
=
(x(t),y(t),z(t))^{T}
\]

una solución del sistema con condiciones iniciales no negativas, es decir,

\[
\boldsymbol{\phi}(t_0)\in\mathbb{R}_{+,0}^{3}.
\]

Entonces, el octante no negativo es positivamente invariante y las soluciones satisfacen

\[
\boldsymbol{\phi}(t)\in\mathbb{R}_{+,0}^{3},
\qquad t\geq t_0.
\]

Esto significa que, si las poblaciones comienzan con valores no negativos, el modelo conserva esa propiedad durante su evolución temporal.

[Volver al contenido](#contenido)

---

<a id="equilibrios"></a>
## Puntos de equilibrio libres de células patológicas

Con el objetivo de determinar condiciones para eliminar las células patológicas, se buscan los puntos de equilibrio en los que

\[
x^*=0.
\]

Los puntos de equilibrio se obtienen igualando a cero las tres ecuaciones del sistema:

\[
r_1x(1-b_1x)-a_{12}xy-a_{13}xz=0,
\]

\[
r_2y(1-b_2y)-a_{21}xy=0,
\]

\[
(r_3-a_{31})xz-d_3z+\rho=0.
\]

Al establecer \(x=0\), el sistema se reduce a

\[
x^*=0,
\]

\[
r_2y(1-b_2y)=0,
\]

\[
-d_3z+\rho=0.
\]

Despejando las variables de estado se obtiene

\[
x^*=0,
\qquad
z^*=\frac{\rho}{d_3}.
\]

La ecuación correspondiente a \(y\) puede escribirse como

\[
y(1-b_2y)=0.
\]

Por lo tanto, existen dos soluciones:

\[
y_0^*=0,
\qquad
y_1^*=\frac{1}{b_2}.
\]

De esta manera, se obtienen dos puntos de equilibrio libres de células patológicas:

**Equilibrio 1:**

\[
E_0=
\left(
0,\;0,\;\frac{\rho}{d_3}
\right).
\]

**Equilibrio 2:**

\[
E_1=
\left(
0,\;\frac{1}{b_2},\;\frac{\rho}{d_3}
\right).
\]

El equilibrio \(E_1\) representa la ausencia de células patológicas y la presencia de las otras dos poblaciones en sus respectivos valores de equilibrio. Este punto es el principal objeto de interés para el análisis de estabilidad y eliminación.

[Volver al contenido](#contenido)

---

<a id="estabilidad-local"></a>
## Estabilidad asintótica local

Para analizar la estabilidad local de los puntos de equilibrio, se construye la matriz Jacobiana del sistema.

### 1. Matriz Jacobiana

La matriz Jacobiana se define como

\[
J(x,y,z)=
\begin{bmatrix}
\dfrac{\partial \dot{x}}{\partial x}
&
\dfrac{\partial \dot{x}}{\partial y}
&
\dfrac{\partial \dot{x}}{\partial z}
\\[6pt]
\dfrac{\partial \dot{y}}{\partial x}
&
\dfrac{\partial \dot{y}}{\partial y}
&
\dfrac{\partial \dot{y}}{\partial z}
\\[6pt]
\dfrac{\partial \dot{z}}{\partial x}
&
\dfrac{\partial \dot{z}}{\partial y}
&
\dfrac{\partial \dot{z}}{\partial z}
\end{bmatrix}.
\]

Al calcular las derivadas parciales se obtiene

\[
J(x,y,z)=
\begin{bmatrix}
r_1-a_{12}y-a_{13}z-2b_1r_1x
&
-a_{12}x
&
-a_{13}x
\\
-a_{21}y
&
r_2-a_{21}x-2b_2r_2y
&
0
\\
(r_3-a_{31})z
&
0
&
(r_3-a_{31})x-d_3
\end{bmatrix}.
\]

### 2. Estabilidad del equilibrio \(E_1\)

Se considera el equilibrio

\[
E_1=
\left(
0,\frac{1}{b_2},\frac{\rho}{d_3}
\right).
\]

Al evaluar la matriz Jacobiana en este punto se obtiene

\[
J(E_1)=
\begin{bmatrix}
r_1-\dfrac{a_{12}}{b_2}-\dfrac{a_{13}\rho}{d_3}
&
0
&
0
\\[8pt]
-\dfrac{a_{21}}{b_2}
&
-r_2
&
0
\\[8pt]
\dfrac{\rho}{d_3}(r_3-a_{31})
&
0
&
-d_3
\end{bmatrix}.
\]

La matriz resultante es triangular inferior. Por esta razón, sus valores propios corresponden a los elementos de su diagonal:

\[
\lambda_1
=
r_1-\frac{a_{12}}{b_2}-\frac{a_{13}\rho}{d_3},
\]

\[
\lambda_2=-r_2,
\qquad
\lambda_3=-d_3.
\]

Como los parámetros son positivos,

\[
\lambda_2<0,
\qquad
\lambda_3<0.
\]

Para que el equilibrio sea local asintóticamente estable, también se requiere que \(\lambda_1<0\). Por lo tanto,

\[
r_1-\frac{a_{12}}{b_2}
-\frac{a_{13}\rho}{d_3}<0.
\]

Despejando el parámetro de control:

\[
\boxed{
\rho>
\frac{d_3}{a_{13}}
\left(
r_1-\frac{a_{12}}{b_2}
\right)
}
\]

**Resultado: Condición de eliminación local de células patológicas.**

Si se satisface la condición

\[
\rho>
\frac{d_3}{a_{13}}
\left(
r_1-\frac{a_{12}}{b_2}
\right),
\]

entonces el equilibrio libre de células patológicas

\[
E_1=
\left(
0,\frac{1}{b_2},\frac{\rho}{d_3}
\right)
\]

es local asintóticamente estable. En consecuencia, una población inicial de células patológicas suficientemente cercana al equilibrio puede converger hacia cero.

### 3. Condición de persistencia

De manera complementaria, si

\[
\rho<
\frac{d_3}{a_{13}}
\left(
r_1-\frac{a_{12}}{b_2}
\right),
\]

el equilibrio \(E_1\) deja de satisfacer la condición de estabilidad asintótica local. El material de la práctica establece que, bajo esta condición, se observará persistencia de la población de células patológicas en las soluciones y trayectorias del sistema.

### 4. Estabilidad del equilibrio \(E_0\)

Como actividad complementaria, se analiza el equilibrio

\[
E_0=
\left(
0,0,\frac{\rho}{d_3}
\right).
\]

Al evaluar la matriz Jacobiana en este punto se obtiene

\[
J(E_0)=
\begin{bmatrix}
r_1-\dfrac{a_{13}\rho}{d_3}
&
0
&
0
\\[8pt]
0
&
r_2
&
0
\\[8pt]
\dfrac{\rho}{d_3}(r_3-a_{31})
&
0
&
-d_3
\end{bmatrix}.
\]

La matriz también es triangular, por lo que sus valores propios son

\[
\lambda_1=r_1-\frac{a_{13}\rho}{d_3},
\]

\[
\lambda_2=r_2,
\qquad
\lambda_3=-d_3.
\]

El primer valor propio es negativo si

\[
\rho>\frac{r_1d_3}{a_{13}}.
\]

Sin embargo, como \(r_2>0\), se tiene

\[
\lambda_2>0,
\qquad
\lambda_3<0.
\]

Por lo tanto, incluso cuando \(\lambda_1<0\), el equilibrio \(E_0\) conserva un valor propio positivo y uno negativo. En consecuencia, es un **punto silla** y no es local asintóticamente estable.

[Volver al contenido](#contenido)

---

<a id="conjuntos"></a>
## Conjuntos compactos invariantes

Para estudiar el dominio en el que se localizan las soluciones del sistema, se proponen funciones localizadoras que permiten establecer límites inferiores y superiores para las variables de estado \(x(t)\), \(y(t)\) y \(z(t)\).

Debido a la positividad del sistema, las soluciones con condiciones iniciales no negativas permanecen en

\[
\mathbb{R}_{+,0}^{3}
=
\left\{
(x,y,z)\in\mathbb{R}^{3}
\mid x,y,z\geq0
\right\}.
\]

### 1. Límites de la variable \(x(t)\)

Se propone la función localizadora

\[
h_1=x.
\]

Su derivada de Lie está dada por

\[
L_fh_1
=
\frac{dx}{dt}
=
r_1x(1-b_1x)-a_{12}xy-a_{13}xz.
\]

Se define el conjunto

\[
S(h_1)=\{L_fh_1=0\}.
\]

Al factorizar la variable \(x\):

\[
S(h_1)
=
\left\{
r_1-b_1r_1x-a_{12}y-a_{13}z=0
\right\}
\cup
\{x=0\}.
\]

De esta expresión se identifica el límite inferior

\[
x(t)\geq x_{\mathrm{inf}}=0.
\]

Además, el plano \(x=0\) es invariante: las trayectorias que se encuentran en dicho plano no lo atraviesan hacia valores negativos.

Para obtener una expresión del límite superior, se despeja \(x\):

\[
x=
\frac{1}{b_1}
-
\frac{a_{12}}{b_1r_1}y
-
\frac{a_{13}}{b_1r_1}z.
\]

Definiendo

\[
f(y,z)
=
\frac{a_{12}}{b_1r_1}y
+
\frac{a_{13}}{b_1r_1}z,
\]

se obtiene

\[
S(h_1)
=
\left\{
x=\frac{1}{b_1}-f(y,z)
\right\}
\cup
\{x=0\}.
\]

Por lo tanto, el material establece el siguiente conjunto de límites para \(x(t)\):

\[
\boxed{
K_x=
\left\{
0\leq x(t)\leq\frac{1}{b_1}
\right\}.
}
\]

### 2. Límites de la variable \(y(t)\)

Para la segunda variable se propone

\[
h_2=y.
\]

Su derivada de Lie es

\[
L_fh_2
=
\frac{dy}{dt}
=
r_2y(1-b_2y)-a_{21}xy.
\]

Se define

\[
S(h_2)=\{L_fh_2=0\}.
\]

Factorizando \(y\):

\[
S(h_2)
=
\{r_2-b_2r_2y-a_{21}x=0\}
\cup
\{y=0\}.
\]

Despejando \(y\):

\[
y=
\frac{1}{b_2}
-
\frac{a_{21}}{b_2r_2}x.
\]

Si se define

\[
f(x)=\frac{a_{21}}{b_2r_2}x,
\]

entonces

\[
S(h_2)
=
\left\{
y=\frac{1}{b_2}-f(x)
\right\}
\cup
\{y=0\}.
\]

De esta manera, se establece el conjunto

\[
\boxed{
K_y=
\left\{
0\leq y(t)\leq\frac{1}{b_2}
\right\}.
}
\]

### 3. Límite inferior de la variable \(z(t)\)

Para la tercera variable se propone

\[
h_3=z.
\]

Su derivada de Lie es

\[
L_fh_3
=
\frac{dz}{dt}
=
(r_3-a_{31})xz-d_3z+\rho.
\]

Se define el conjunto

\[
S(h_3)=\{L_fh_3=0\}.
\]

Al despejar \(z\), se obtiene

\[
z=
\frac{\rho}{d_3}
+
\frac{r_3-a_{31}}{d_3}xz.
\]

Si se cumple la condición

\[
r_3-a_{31}>0,
\]

se puede establecer el límite inferior

\[
\boxed{
K_z=
\left\{
z(t)\geq\frac{\rho}{d_3}
\right\}.
}
\]

### 4. Dominio conjunto

Los conjuntos obtenidos para las tres variables permiten definir el dominio de análisis mediante la intersección

\[
K=K_x\cap K_y\cap K_z.
\]

De acuerdo con los límites establecidos en el material de la práctica:

\[
0\leq x(t)\leq\frac{1}{b_1},
\]

\[
0\leq y(t)\leq\frac{1}{b_2},
\]

\[
z(t)\geq\frac{\rho}{d_3}.
\]

Estos límites se utilizan posteriormente para evaluar la función candidata de Lyapunov y establecer condiciones de eliminación de células patológicas.

[Volver al contenido](#contenido)

---

<a id="estabilidad-global"></a>
## Estabilidad asintótica global: condiciones de eliminación

Para establecer condiciones de eliminación de la población de células patológicas se aplica el método directo de Lyapunov.

La variable que se desea controlar es \(x(t)\), por lo que se propone la siguiente función candidata:

\[
\boxed{V(x)=x.}
\]

La elección de esta función responde a que el objetivo del análisis es llevar la población patológica al origen, es decir,

\[
x(t)\longrightarrow0.
\]

### 1. Condiciones de una función candidata de Lyapunov

Para aplicar el método directo de Lyapunov se consideran las siguientes propiedades:

**1. Definida positiva.**

Una función es definida positiva respecto al origen si

\[
V(0)=0,
\qquad
V(x)>0\quad\text{para }x>0.
\]

En este caso, \(V(x)=x\) satisface esta propiedad en el dominio no negativo.

**2. Radialmente desacotada.**

Una función es radialmente desacotada si

\[
V(x)\longrightarrow\infty
\quad\text{cuando}\quad
\|x\|\longrightarrow\infty.
\]

Esta propiedad permite relacionar el crecimiento de la función con la distancia respecto al origen.

**3. Derivada temporal semidefinida negativa o definida negativa.**

La derivada temporal de la función candidata debe ser, preferentemente, definida negativa. Es semidefinida negativa cuando

\[
\dot V(x)\leq0,
\]

y definida negativa cuando

\[
\dot V(x)<0
\quad\text{para }x>0,
\qquad
\dot V(0)=0.
\]

**4. Principio de invariancia de LaSalle.**

Cuando la derivada temporal es semidefinida negativa, se garantiza que la función candidata no aumenta a lo largo de las trayectorias. Para establecer condiciones de estabilidad asintótica se puede aplicar el principio de invariancia de LaSalle, que permite analizar el comportamiento de las trayectorias dentro del conjunto donde

\[
\dot V=0.
\]

### 2. Derivada temporal de la función candidata

Dado que

\[
V(x)=x,
\]

su derivada temporal es

\[
\dot V
=
\frac{dV}{dt}
=
\frac{dx}{dt}.
\]

Sustituyendo la primera ecuación del sistema:

\[
\dot V
=
r_1x(1-b_1x)-a_{12}xy-a_{13}xz.
\]

Factorizando:

\[
\dot V
=
(r_1-b_1r_1x-a_{12}y-a_{13}z)x.
\]

### 3. Evaluación mediante los límites invariantes

Se evalúa la expresión anterior utilizando los límites establecidos para las variables:

\[
x_{\mathrm{inf}}=0,
\qquad
y_{\mathrm{inf}}=0,
\qquad
z_{\mathrm{inf}}=\frac{\rho}{d_3}.
\]

Por lo tanto,

\[
\dot V
\leq
\left(
r_1-b_1r_1x_{\mathrm{inf}}
-a_{12}y_{\mathrm{inf}}
-a_{13}z_{\mathrm{inf}}
\right)x.
\]

Sustituyendo los límites inferiores:

\[
\dot V
\leq
\left(
r_1-\frac{a_{13}\rho}{d_3}
\right)x.
\]

Para que la derivada sea negativa cuando \(x>0\), se requiere

\[
r_1-\frac{a_{13}\rho}{d_3}<0.
\]

Despejando el parámetro de control:

\[
\boxed{
\rho>\frac{r_1d_3}{a_{13}}.
}
\]

### 4. Condición global de eliminación

**Resultado: Condición de eliminación.**

Si se satisface la condición

\[
\boxed{
\rho>\frac{r_1d_3}{a_{13}},
}
\]

entonces, de acuerdo con el análisis de Lyapunov presentado en la práctica, la población de células patológicas se eliminará para cualquier condición inicial positiva. Además, las trayectorias convergerán al equilibrio

\[
\boxed{
E_1=
\left(
0,\frac{1}{b_2},\frac{\rho}{d_3}
\right).
}
\]

Esta condición establece un umbral para el parámetro de control \(\rho\). Cuando dicho parámetro supera el umbral, se obtiene una condición suficiente para la eliminación de la población patológica.

[Volver al contenido](#contenido)

---

<a id="actividades"></a>
## Actividades de la práctica

Las actividades se organizan de acuerdo con los apartados del desarrollo matemático proporcionado.

### 1. Modelo matemático

- Identificar las tres variables de estado y los parámetros del sistema.
- Interpretar el significado de cada término de las ecuaciones diferenciales.
- Identificar la población que se desea controlar y el parámetro de control.

### 2. Positividad del sistema

- Evaluar el campo vectorial en las fronteras \(x=0\), \(y=0\) y \(z=0\).
- Establecer las condiciones que garantizan que las soluciones permanezcan en el octante no negativo.
- Explicar el significado de la invariancia positiva en el contexto biológico.

### 3. Puntos de equilibrio libres de células patológicas

- Igualar a cero las tres ecuaciones del sistema.
- Establecer \(x=0\).
- Resolver las ecuaciones restantes para obtener los valores de equilibrio de \(y\) y \(z\).
- Identificar y describir los dos puntos de equilibrio obtenidos.

### 4. Estabilidad asintótica local

- Calcular la matriz Jacobiana del sistema.
- Evaluar la matriz Jacobiana en el equilibrio \(E_1\).
- Obtener los valores propios de la matriz resultante.
- Determinar la condición sobre \(\rho\) para garantizar estabilidad asintótica local.
- Analizar la condición complementaria asociada con la persistencia de células patológicas.

### 5. Estabilidad del equilibrio en el origen de la población patológica

- Evaluar la matriz Jacobiana en

\[
E_0=\left(0,0,\frac{\rho}{d_3}\right).
\]

- Calcular los valores propios.
- Determinar las condiciones de signo de cada valor propio.
- Clasificar el equilibrio y explicar por qué no es local asintóticamente estable.

### 6. Conjuntos compactos invariantes

- Proponer la función localizadora \(h_1=x\).
- Calcular su derivada de Lie y determinar los límites de \(x(t)\).
- Proponer la función localizadora \(h_2=y\).
- Calcular su derivada de Lie y determinar los límites de \(y(t)\).
- Proponer la función localizadora \(h_3=z\).
- Determinar la condición requerida para establecer el límite inferior de \(z(t)\).
- Construir el dominio conjunto a partir de la intersección de los conjuntos obtenidos.

### 7. Estabilidad asintótica global y condiciones de eliminación

- Proponer la función candidata de Lyapunov \(V=x\).
- Explicar qué significa que una función sea definida positiva.
- Explicar qué significa que una función sea radialmente desacotada.
- Distinguir entre una derivada semidefinida negativa y una definida negativa.
- Explicar cuándo es necesario utilizar el principio de invariancia de LaSalle.
- Calcular la derivada temporal de la función candidata.
- Evaluar la derivada utilizando los límites inferiores de las variables.
- Despejar la condición sobre \(\rho\) que garantiza la eliminación de células patológicas.
- Interpretar el equilibrio al que convergen las trayectorias.

[Volver al contenido](#contenido)

---

<a id="resultados"></a>
## Resultados y condiciones principales

Las condiciones matemáticas obtenidas en el desarrollo se resumen en la siguiente tabla.

| Análisis | Resultado |
|---|---|
| Positividad | El octante no negativo es positivamente invariante |
| Equilibrio libre de células patológicas \(E_0\) | \(\left(0,0,\frac{\rho}{d_3}\right)\) |
| Equilibrio libre de células patológicas \(E_1\) | \(\left(0,\frac{1}{b_2},\frac{\rho}{d_3}\right)\) |
| Valores propios en \(E_1\) | \(\lambda_1=r_1-\frac{a_{12}}{b_2}-\frac{a_{13}\rho}{d_3}\), \(\lambda_2=-r_2\), \(\lambda_3=-d_3\) |
| Condición de estabilidad local de \(E_1\) | \(\rho>\frac{d_3}{a_{13}}\left(r_1-\frac{a_{12}}{b_2}\right)\) |
| Condición de eliminación mediante Lyapunov | \(\rho>\frac{r_1d_3}{a_{13}}\) |
| Equilibrio de convergencia indicado para la eliminación | \(\left(0,\frac{1}{b_2},\frac{\rho}{d_3}\right)\) |

### Comparación de las condiciones de eliminación

El análisis local y el análisis global producen dos condiciones diferentes:

**Condición local:**

\[
\rho>
\frac{d_3}{a_{13}}
\left(
r_1-\frac{a_{12}}{b_2}
\right).
\]

**Condición global mediante Lyapunov:**

\[
\rho>\frac{r_1d_3}{a_{13}}.
\]

La primera se obtiene a partir de los valores propios de la matriz Jacobiana evaluada en el equilibrio \(E_1\). La segunda se obtiene mediante la función candidata de Lyapunov y los límites inferiores de las variables de estado.

Por lo tanto, ambas condiciones corresponden a enfoques distintos del análisis de estabilidad y no deben interpretarse como si fueran el mismo criterio.

[Volver al contenido](#contenido)

---

<a id="reproducibilidad"></a>
## Alcance del material y reproducibilidad

El material proporcionado para esta práctica contiene el desarrollo analítico del modelo, el análisis de positividad, el cálculo de los puntos de equilibrio, la matriz Jacobiana, los valores propios, los conjuntos invariantes y el análisis de Lyapunov.

Aunque el título de la actividad es **Caos en Sistemas Biológicos**, el material matemático recibido desarrolla principalmente propiedades de positividad, estabilidad y eliminación de poblaciones. No incluye un análisis específico de caos, como exponentes de Lyapunov, secciones de Poincaré, bifurcaciones o identificación de atractores caóticos. Por ello, el documento conserva el nombre de la práctica, pero no atribuye al modelo resultados de caos que no aparecen en el material.

Tampoco se especifican valores numéricos de los parámetros, condiciones iniciales particulares, un conjunto de datos experimentales ni un archivo de implementación computacional. Por esta razón, este documento presenta los resultados analíticos y las condiciones simbólicas disponibles, sin atribuir al sistema simulaciones o resultados numéricos que no fueron proporcionados.

Para complementar el análisis con una implementación computacional sería necesario definir los valores de los parámetros y las condiciones iniciales, y resolver numéricamente el sistema de ecuaciones diferenciales.

### Resultados mínimos que deben identificarse en el desarrollo

- Sistema de tres ecuaciones diferenciales no lineales.
- Demostración de positividad e invariancia del octante no negativo.
- Dos puntos de equilibrio con \(x=0\).
- Matriz Jacobiana del sistema.
- Valores propios de los equilibrios \(E_0\) y \(E_1\).
- Condición de estabilidad asintótica local de \(E_1\).
- Clasificación de \(E_0\) como punto silla.
- Límites de las variables de estado mediante funciones localizadoras.
- Función candidata de Lyapunov \(V=x\).
- Condición global de eliminación \(\rho>\frac{r_1d_3}{a_{13}}\).
- Equilibrio al que convergen las trayectorias bajo la condición de eliminación indicada.

[Volver al contenido](#contenido)

---

<a id="referencias"></a>
## Referencias

[1] P. A. Valle, *Syllabus para Biología de Sistemas y Gemelos Digitales*, Tecnológico Nacional de México / Instituto Tecnológico de Tijuana, Tijuana, B.C., México, 2026. Disponible en: https://biomath.xyz/course/

[2] De Leenheer y Aeyels, trabajo citado en el material de la práctica para el criterio de positividad de sistemas dinámicos. Los datos bibliográficos completos no se especifican en el documento fuente.

---

## Uso académico

Este repositorio se utiliza con fines docentes en la asignatura **Modelado Matemático** de la **Maestría en Ciencias de la Ingeniería**. El desarrollo debe complementarse con la interpretación matemática y biológica de los resultados. La obtención de condiciones de estabilidad y eliminación requiere comprender tanto el comportamiento local alrededor de los puntos de equilibrio como las propiedades globales de las trayectorias del sistema.
