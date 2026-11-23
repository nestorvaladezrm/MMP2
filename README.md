# Práctica 2 — Caos en Sistemas Biológicos

Repositorio académico de la asignatura **Modelado Matemático**, correspondiente a la **Maestría en Ciencias de la Ingeniería** del Tecnológico Nacional de México / Instituto Tecnológico de Tijuana. Esta práctica estudia un modelo de tres poblaciones celulares mediante ecuaciones diferenciales ordinarias no lineales, con énfasis en la positividad del sistema, los puntos de equilibrio, la estabilidad local, los conjuntos compactos invariantes y las condiciones de eliminación de células patológicas.

El modelo considera la interacción entre una población de células patológicas y otras dos poblaciones celulares, además de un parámetro de control $\rho$ que influye en la dinámica de la tercera variable.

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
4. [Análisis matemático](#analisis)
   - [Positividad e invariancia](#positividad)
   - [Equilibrios libres de células patológicas](#equilibrios)
   - [Estabilidad asintótica local](#estabilidad)
   - [Conjuntos compactos invariantes](#compactos)
   - [Estabilidad asintótica global y condiciones de eliminación](#lyapunov)
5. [Actividades y desarrollo de la práctica](#actividades)
6. [Resultados analíticos principales](#resultados)
7. [Alcance y consideraciones](#alcance)
8. [Referencias](#referencias)

---

<a id="resumen"></a>
## Resumen

Esta práctica estudia un modelo matemático de tres ecuaciones diferenciales ordinarias no lineales que describe la interacción entre tres poblaciones celulares. El análisis se enfoca en la población de células patológicas, representada por $x(t)$, cuya eliminación se busca mediante el parámetro de control $\rho$.

Primero se formula el sistema y se examina la positividad de sus soluciones en el octante no negativo. Después se determinan los puntos de equilibrio libres de células patológicas, se construye la matriz Jacobiana y se obtienen condiciones para la estabilidad asintótica local. Posteriormente se proponen conjuntos invariantes para acotar las variables de estado y se utiliza una función candidata de Lyapunov para establecer una condición suficiente de eliminación global.

El resultado central del análisis presentado es que, bajo las condiciones indicadas para el modelo y sus parámetros, el control debe satisfacer una cota inferior relacionada con $r_1$, $d_3$ y $a_{13}$ para favorecer la eliminación de la población patológica.

**Palabras clave:** sistemas biológicos; ecuaciones diferenciales ordinarias; poblaciones celulares; positividad; puntos de equilibrio; matriz Jacobiana; estabilidad local; conjuntos invariantes; función de Lyapunov; eliminación de células patológicas.

[Volver al contenido](#contenido)

---

<a id="objetivos"></a>
## Objetivos

### Objetivo general

Analizar la dinámica de un sistema biológico de tres poblaciones celulares mediante herramientas de sistemas dinámicos no lineales, con el propósito de establecer condiciones de estabilidad y eliminación de la población de células patológicas.

### Objetivos específicos

- Formular el modelo matemático mediante un sistema de tres ecuaciones diferenciales ordinarias no lineales.
- Examinar las condiciones de positividad de las soluciones y la invariancia del octante no negativo.
- Determinar los puntos de equilibrio en los que la población de células patológicas es nula.
- Construir la matriz Jacobiana y calcular los valores propios en los puntos de equilibrio.
- Establecer condiciones de estabilidad asintótica local en función del parámetro de control $\rho$.
- Proponer límites inferiores y superiores para las variables de estado mediante conjuntos invariantes.
- Aplicar el método directo de Lyapunov para obtener una condición suficiente de eliminación global.
- Interpretar el significado biológico de las condiciones matemáticas obtenidas.

[Volver al contenido](#contenido)

---

<a id="modelo"></a>
## Modelo matemático

El modelo matemático que describe la dinámica entre tres poblaciones celulares está dado por el siguiente sistema de ecuaciones diferenciales ordinarias no lineales de primer orden:

$$
\frac{dx}{dt}=r_1x(1-b_1x)-a_{12}xy-a_{13}xz,
$$

$$
\frac{dy}{dt}=r_2y(1-b_2y)-a_{21}xy,
$$

$$
\frac{dz}{dt}=(r_3-a_{31})xz-d_3z+\rho.
$$

Se considera que los parámetros son positivos, que las condiciones iniciales son no negativas y que el parámetro de control cumple $\rho>0$.

El sistema puede expresarse en forma vectorial como

$$
\dot{\mathbf{X}}=\mathbf{F}(\mathbf{X}),
\qquad
\mathbf{X}=
\begin{bmatrix}
x\\y\\z
\end{bmatrix}.
$$

Las variables de estado son:

| Variable | Descripción en el modelo |
|---|---|
| $x(t)$ | Población de células patológicas cuya eliminación se busca |
| $y(t)$ | Segunda población celular |
| $z(t)$ | Tercera población celular, asociada al término de control $\rho$ |

Los parámetros del modelo son:

| Parámetro | Función en el sistema |
|---|---|
| $r_1$ | Tasa de crecimiento de la población $x$ |
| $r_2$ | Tasa de crecimiento de la población $y$ |
| $r_3$ | Coeficiente de interacción de $x$ y $z$ en la ecuación de $z$ |
| $b_1$ | Coeficiente de saturación o limitación de la población $x$ |
| $b_2$ | Coeficiente de saturación o limitación de la población $y$ |
| $a_{12}$ | Coeficiente de interacción entre $x$ y $y$ en la ecuación de $x$ |
| $a_{13}$ | Coeficiente de interacción entre $x$ y $z$ en la ecuación de $x$ |
| $a_{21}$ | Coeficiente de interacción entre $x$ y $y$ en la ecuación de $y$ |
| $a_{31}$ | Coeficiente que modifica la interacción entre $x$ y $z$ |
| $d_3$ | Tasa de disminución de la población $z$ |
| $\rho$ | Parámetro de control positivo |

[Volver al contenido](#contenido)

---

<a id="analisis"></a>
## Análisis matemático

<a id="positividad"></a>
### 1. Positividad e invariancia del sistema

Debido a que las variables representan poblaciones celulares, el modelo requiere soluciones no negativas. Para examinar la invariancia del octante no negativo se evalúa el campo vectorial sobre las fronteras $x=0$, $y=0$ y $z=0$.

Para la primera ecuación:

$$
\left.\dot{x}\right|_{x=0}=0.
$$

Para la segunda ecuación:

$$
\left.\dot{y}\right|_{y=0}=0.
$$

Para la tercera ecuación:

$$
\left.\dot{z}\right|_{z=0}=(r_3-a_{31})x+\rho.
$$

Por tanto, la condición sobre la frontera $z=0$ es no negativa si, por ejemplo, $r_3\geq a_{31}$, dado que $x\geq0$ y $\rho>0$. Bajo esta condición, las tres fronteras apuntan hacia el interior o son tangentes al octante no negativo.

El dominio de interés se define como

$$
\mathbb{R}_{+,0}^{3}
=
\left\{
(x,y,z)\in\mathbb{R}^{3}:
x\geq0,\ y\geq0,\ z\geq0
\right\}.
$$

**Resultado — Positividad e invariancia.** Si el campo vectorial satisface las condiciones de frontera anteriores y las condiciones iniciales pertenecen a $\mathbb{R}_{+,0}^{3}$, entonces el octante no negativo es positivamente invariante: las soluciones permanecen en dicho dominio para todo tiempo en el que estén definidas.

> **Nota sobre la condición de positividad:** al sustituir $z=0$ en la tercera ecuación, los términos que contienen $z$ se anulan y queda $\left.\dot z\right|_{z=0}=\rho>0$. Por tanto, la frontera $z=0$ apunta hacia el interior del octante no negativo. Junto con las evaluaciones en $x=0$ y $y=0$, esto respalda la invariancia positiva del dominio para condiciones iniciales no negativas.

[Volver al contenido](#contenido)

---

<a id="equilibrios"></a>
### 2. Puntos de equilibrio libres de células patológicas

El objetivo es determinar los equilibrios en los que la población patológica desaparece, es decir, aquellos para los cuales $x=0$.

Los puntos de equilibrio se obtienen igualando a cero las tres derivadas:

$$
r_1x(1-b_1x)-a_{12}xy-a_{13}xz=0,
$$

$$
r_2y(1-b_2y)-a_{21}xy=0,
$$

$$
(r_3-a_{31})xz-d_3z+\rho=0.
$$

Al imponer $x=0$, el sistema se reduce a

$$
x=0,
\qquad
r_2y(1-b_2y)=0,
\qquad
-d_3z+\rho=0.
$$

De la segunda ecuación se obtienen dos posibilidades:

$$
y_0^*=0,
\qquad
y_1^*=\frac{1}{b_2}.
$$

De la tercera ecuación:

$$
z^*=\frac{\rho}{d_3}.
$$

Por consiguiente, los dos equilibrios libres de células patológicas son

$$
E_0=
\left(0,0,\frac{\rho}{d_3}\right),
$$

y

$$
E_1=
\left(0,\frac{1}{b_2},\frac{\rho}{d_3}\right).
$$

El equilibrio $E_0$ representa la ausencia de las tres poblaciones salvo el nivel de equilibrio impuesto por el parámetro de control en $z$. El equilibrio $E_1$ representa la eliminación de la población $x$, mientras que la población $y$ alcanza su nivel de saturación $1/b_2$ y la variable $z$ alcanza $\rho/d_3$.

[Volver al contenido](#contenido)

---

<a id="estabilidad"></a>
### 3. Estabilidad asintótica local

Para estudiar la estabilidad local de los puntos de equilibrio se calcula la matriz Jacobiana del sistema.

$$
J(x,y,z)=
\begin{bmatrix}
r_1-a_{12}y-a_{13}z-2b_1r_1x & -a_{12}x & -a_{13}x\\
-a_{21}y & r_2-a_{21}x-2b_2r_2y & 0\\
(r_3-a_{31})z & 0 & (r_3-a_{31})x-d_3
\end{bmatrix}.
$$

#### 3.1 Estabilidad del equilibrio $E_1$

Se evalúa la Jacobiana en

$$
E_1=
\left(0,\frac{1}{b_2},\frac{\rho}{d_3}\right).
$$

La matriz resultante es

$$
J(E_1)=
\begin{bmatrix}
r_1-\dfrac{a_{12}}{b_2}-\dfrac{a_{13}\rho}{d_3} & 0 & 0\\
-\dfrac{a_{21}}{b_2} & -r_2 & 0\\
\dfrac{\rho}{d_3}(r_3-a_{31}) & 0 & -d_3
\end{bmatrix}.
$$

La matriz es triangular inferior, por lo que sus valores propios corresponden a los elementos de su diagonal:

$$
\lambda_1=
r_1-\frac{a_{12}}{b_2}-\frac{a_{13}\rho}{d_3},
$$

$$
\lambda_2=-r_2,
\qquad
\lambda_3=-d_3.
$$

Como los parámetros $r_2$ y $d_3$ son positivos, se tiene $\lambda_2<0$ y $\lambda_3<0$. Para que el tercer equilibrio sea localmente asintóticamente estable también se requiere $\lambda_1<0$:

$$
r_1-\frac{a_{12}}{b_2}-\frac{a_{13}\rho}{d_3}<0.
$$

Despejando el parámetro de control:

$$
\rho>
\frac{d_3}{a_{13}}
\left(
r_1-\frac{a_{12}}{b_2}
\right).
$$

**Resultado — Condición de eliminación local.** Si se satisface la desigualdad anterior, entonces el equilibrio $E_1$ es localmente asintóticamente estable. En consecuencia, las condiciones iniciales suficientemente cercanas a este equilibrio convergen hacia un estado con $x=0$.

**Resultado complementario — Persistencia local.** Si

$$
\rho<
\frac{d_3}{a_{13}}
\left(
r_1-\frac{a_{12}}{b_2}
\right),
$$

entonces $\lambda_1>0$ y el equilibrio $E_1$ es inestable. Esto permite que la población patológica persista para condiciones iniciales cercanas al equilibrio, aunque por sí solo no demuestra persistencia para todas las condiciones iniciales.

#### 3.2 Estabilidad del equilibrio $E_0$

Para el equilibrio

$$
E_0=
\left(0,0,\frac{\rho}{d_3}\right),
$$

la matriz Jacobiana evaluada es

$$
J(E_0)=
\begin{bmatrix}
r_1-\dfrac{a_{13}\rho}{d_3} & 0 & 0\\
0 & r_2 & 0\\
\dfrac{\rho}{d_3}(r_3-a_{31}) & 0 & -d_3
\end{bmatrix}.
$$

Al ser triangular, sus valores propios son

$$
\lambda_1=r_1-\frac{a_{13}\rho}{d_3},
\qquad
\lambda_2=r_2,
\qquad
\lambda_3=-d_3.
$$

Se observa que $\lambda_2>0$ y $\lambda_3<0$. Además, $\lambda_1<0$ cuando

$$
\rho>\frac{r_1d_3}{a_{13}}.
$$

Aun cuando se cumpla esta última condición, existe un valor propio positivo ($\lambda_2=r_2$) y otro negativo ($\lambda_3=-d_3$). Por lo tanto, $E_0$ es un **punto silla** y no es localmente asintóticamente estable.

[Volver al contenido](#contenido)

---

<a id="compactos"></a>
### 4. Conjuntos compactos invariantes

Para estudiar el dominio en el que se localiza la dinámica del sistema se buscan límites inferiores y superiores para las variables $x(t)$, $y(t)$ y $z(t)$.

El dominio biológicamente relevante es el octante no negativo:

$$
\mathbb{R}_{+,0}^{3}
=
\left\{
(x,y,z)\in\mathbb{R}^{3}:
x,y,z\geq0
\right\}.
$$

#### 4.1 Límite de la variable $x(t)$

Se propone la función localizadora

$$
h_1=x.
$$

Su derivada a lo largo de las trayectorias es

$$
\dot{h}_1=
r_1x(1-b_1x)-a_{12}xy-a_{13}xz.
$$

Al igualar a cero:

$$
x(r_1-b_1r_1x-a_{12}y-a_{13}z)=0.
$$

De aquí se identifica la frontera $x=0$, que establece el límite inferior

$$
x(t)\geq0.
$$

La otra superficie puede despejarse como

$$
x=
\frac{1}{b_1}
-\frac{a_{12}}{b_1r_1}y
-\frac{a_{13}}{b_1r_1}z.
$$

Como $y,z\geq0$, se obtiene la cota

$$
0\leq x(t)\leq\frac{1}{b_1}.
$$

#### 4.2 Límite de la variable $y(t)$

Se propone

$$
h_2=y.
$$

Su derivada es

$$
\dot{h}_2=
r_2y(1-b_2y)-a_{21}xy.
$$

Al factorizar:

$$
y(r_2-b_2r_2y-a_{21}x)=0.
$$

La frontera $y=0$ proporciona el límite inferior. Despejando la otra superficie:

$$
y=
\frac{1}{b_2}
-\frac{a_{21}}{b_2r_2}x.
$$

Dado que $x\geq0$, se obtiene

$$
0\leq y(t)\leq\frac{1}{b_2}.
$$

#### 4.3 Límite inferior de la variable $z(t)$

Se propone

$$
h_3=z.
$$

Su derivada es

$$
\dot{h}_3=
(r_3-a_{31})xz-d_3z+\rho.
$$

Al igualar a cero y despejar $z$:

$$
z=
\frac{\rho}{d_3}
+
\frac{r_3-a_{31}}{d_3}xz.
$$

Si se cumple $r_3-a_{31}>0$, el término adicional es no negativo para $x,z\geq0$. De acuerdo con el desarrollo de la práctica, se propone entonces el límite inferior

$$
z(t)\geq\frac{\rho}{d_3}.
$$

**Conjunto de cotas propuesto.** Las regiones de localización consideradas son

$$
K_x=
\left\{
0\leq x(t)\leq\frac{1}{b_1}
\right\},
$$

$$
K_y=
\left\{
0\leq y(t)\leq\frac{1}{b_2}
\right\},
$$

$$
K_z=
\left\{
z(t)\geq\frac{\rho}{d_3}
\right\}.
$$

> **Consideración sobre las cotas:** las superficies donde las derivadas se anulan permiten identificar fronteras candidatas. Para afirmar que las cotas superiores son válidas desde todo instante, deben verificarse las condiciones iniciales y la dirección del campo vectorial sobre esas fronteras. En particular, $x\leq1/b_1$ y $y\leq1/b_2$ son cotas naturales del análisis cuando las trayectorias parten dentro de esos límites; no se deduce que cualquier condición inicial mayor quede instantáneamente dentro de ellos.

[Volver al contenido](#contenido)

---

<a id="lyapunov"></a>
### 5. Estabilidad asintótica global: condiciones de eliminación

Para establecer condiciones de eliminación de la población de células patológicas se propone la función candidata de Lyapunov

$$
V(x)=x.
$$

La elección se debe a que la variable que se desea controlar es $x(t)$; llevarla a cero representa la eliminación de la población patológica.

En el dominio no negativo:

$$
V(x)\geq0,
\qquad
V(0)=0.
$$

La derivada temporal de la función candidata es

$$
\dot{V}=\dot{x}
=r_1x(1-b_1x)-a_{12}xy-a_{13}xz.
$$

Factorizando $x$:

$$
\dot{V}
=
(r_1-b_1r_1x-a_{12}y-a_{13}z)x.
$$

Al evaluar sobre las cotas propuestas para el sistema, en particular $x_{\inf}=0$, $y_{\inf}=0$ y $z_{\inf}=\rho/d_3$, se obtiene la estimación

$$
\dot{V}
\leq
\left(r_1-\frac{a_{13}\rho}{d_3}\right)x.
$$

Para que la derivada sea no positiva se requiere

$$
r_1-\frac{a_{13}\rho}{d_3}\leq0.
$$

Una condición suficiente estricta es

$$
\rho>\frac{r_1d_3}{a_{13}}.
$$

**Resultado — Condición de eliminación global.** Bajo las hipótesis de positividad, acotamiento e invariancia utilizadas en el análisis, si

$$
\boxed{\rho>\frac{r_1d_3}{a_{13}}},
$$

entonces la derivada de la función candidata es negativa para $x>0$ dentro del conjunto considerado. Esto permite concluir que la población de células patológicas disminuye y converge a cero. El equilibrio límite indicado en el desarrollo es

$$
E_1=
\left(0,\frac{1}{b_2},\frac{\rho}{d_3}\right).
$$

Cuando la derivada de Lyapunov es únicamente semidefinida negativa, el principio de invariancia de LaSalle permite analizar el conjunto donde $\dot V=0$ para establecer la convergencia asintótica, siempre que se satisfagan sus hipótesis.

> **Alcance de la conclusión:** la función $V=x$ es positiva definida respecto de la variable objetivo $x$, pero no es radialmente no acotada respecto del vector completo $(x,y,z)$. Por ello, una demostración rigurosa de estabilidad global del equilibrio tridimensional requiere justificar por separado la acotación e invariancia del conjunto, así como aplicar el principio de LaSalle al conjunto donde $\dot V=0$. La desigualdad de control anterior se presenta como la condición suficiente obtenida en el desarrollo de la práctica.

[Volver al contenido](#contenido)

---

<a id="actividades"></a>
## Actividades y desarrollo de la práctica

El desarrollo proporcionado para esta práctica se organiza alrededor de los siguientes análisis matemáticos:

### 1. Modelo matemático

- Identificación de las tres variables de estado.
- Interpretación de los parámetros positivos.
- Incorporación del parámetro de control $\rho$.
- Formulación del sistema de ecuaciones diferenciales.

### 2. Positividad del sistema

- Evaluación del campo vectorial sobre las fronteras $x=0$, $y=0$ y $z=0$.
- Definición del octante no negativo.
- Establecimiento de las condiciones para la invariancia positiva.

### 3. Puntos de equilibrio libres de células patológicas

- Imposición de la condición $x=0$.
- Resolución de las ecuaciones restantes.
- Obtención de $E_0$ y $E_1$.

### 4. Estabilidad asintótica local

- Cálculo de la matriz Jacobiana.
- Evaluación de la Jacobiana en $E_1$.
- Obtención de los valores propios.
- Determinación de la condición local sobre $\rho$.
- Análisis de estabilidad del equilibrio $E_0$.

### 5. Conjuntos compactos invariantes

- Selección de funciones localizadoras $h_1=x$, $h_2=y$ y $h_3=z$.
- Cálculo de las derivadas a lo largo de las trayectorias.
- Identificación de límites inferiores y superiores.
- Construcción de la región de localización del sistema.

### 6. Estabilidad asintótica global

- Selección de la función candidata $V=x$.
- Cálculo de $\dot V$.
- Evaluación de la derivada utilizando los límites del sistema.
- Obtención de la condición de control para la eliminación.
- Consideración del principio de invariancia de LaSalle.

[Volver al contenido](#contenido)

---

<a id="resultados"></a>
## Resultados analíticos principales

Las condiciones principales obtenidas en el desarrollo se resumen en la siguiente tabla.

| Análisis | Resultado |
|---|---|
| Equilibrio libre de células patológicas 1 | $E_0=(0,0,\rho/d_3)$ |
| Equilibrio libre de células patológicas 2 | $E_1=(0,1/b_2,\rho/d_3)$ |
| Valores propios en $E_1$ | $\lambda_1=r_1-a_{12}/b_2-a_{13}\rho/d_3$, $\lambda_2=-r_2$, $\lambda_3=-d_3$ |
| Condición de estabilidad local de $E_1$ | $\rho>(d_3/a_{13})(r_1-a_{12}/b_2)$ |
| Valores propios en $E_0$ | $\lambda_1=r_1-a_{13}\rho/d_3$, $\lambda_2=r_2$, $\lambda_3=-d_3$ |
| Estabilidad de $E_0$ | Punto silla, debido a que $\lambda_2>0$ y $\lambda_3<0$ |
| Cota superior propuesta para $x$ | $x\leq1/b_1$ |
| Cota superior propuesta para $y$ | $y\leq1/b_2$ |
| Cota inferior propuesta para $z$ | $z\geq\rho/d_3$ |
| Condición suficiente de eliminación global | $\rho>r_1d_3/a_{13}$ |

La condición de eliminación global es más restrictiva que la condición local de estabilidad de $E_1$ cuando $a_{12}/b_2>0$. Esto es consistente con que una condición global suficiente debe garantizar un resultado sobre un conjunto más amplio de condiciones iniciales que una condición de estabilidad local.

[Volver al contenido](#contenido)

---

<a id="alcance"></a>
## Alcance y consideraciones

El material proporcionado desarrolla principalmente el análisis cualitativo del sistema: positividad, equilibrios, estabilidad local, cotas para las variables y una condición de eliminación mediante una función candidata de Lyapunov.

Aunque el título de la práctica hace referencia al caos en sistemas biológicos, el desarrollo matemático disponible no incluye pruebas numéricas o gráficas que permitan afirmar la presencia de caos. En particular, no se proporcionan exponentes de Lyapunov, secciones de Poincaré, diagramas de bifurcación ni evidencia de atractores caóticos. Por esta razón, el documento se limita a describir los análisis efectivamente incluidos en el material fuente.

Tampoco se proporcionan valores numéricos de los parámetros, condiciones iniciales concretas ni resultados de simulación. En consecuencia, no se agregan gráficas ni resultados computacionales que no estén respaldados por el material de la práctica.

[Volver al contenido](#contenido)

---

<a id="referencias"></a>
## Referencias

[1] P. A. Valle, *Syllabus para Biología de Sistemas y Gemelos Digitales*, Tecnológico Nacional de México / Instituto Tecnológico de Tijuana, Tijuana, B.C., México, 2026. Disponible en: https://biomath.xyz/course/

[2] De Leenheer y Aeyels, trabajo citado en el material de la práctica para el análisis de positividad del sistema. La referencia bibliográfica completa no aparece en el documento fuente.

---

## Uso académico

Este documento se utiliza con fines docentes en la asignatura **Modelado Matemático** de la **Maestría en Ciencias de la Ingeniería**. El análisis matemático debe complementarse con la interpretación biológica de las variables, los parámetros y las condiciones de estabilidad. Las condiciones analíticas aquí presentadas no sustituyen la verificación de las hipótesis matemáticas necesarias para demostrar invariancia y convergencia global.
