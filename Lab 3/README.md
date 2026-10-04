# Guía de sustentación — Laboratorio 3

Esta guía resume y verifica el contenido del laboratorio desde **Punto 1:
Teorema del límite central** hasta el final. Las decisiones estadísticas usan
un nivel de significancia de \(\alpha=0.05\), salvo que se indique lo
contrario.

## Resumen rápido de resultados

| Sección | Resultado principal |
|---|---|
| 1.1–1.2 | La suma de uniformes se aproxima a una normal cuando aumenta \(n\). |
| 1.3 | La suma de exponenciales tiene distribución Gamma/Erlang y se aproxima a una normal para \(n\) grande. |
| 2.1 | Variables independientes, no idénticamente distribuidas: la suma sigue aproximándose a una normal. |
| 2.2 | La suma de uniformes, exponenciales y gaussianas se aproxima a una normal. |
| 2.3 | La dependencia entre variables cambia la varianza y exige analizar las correlaciones. |
| 3 | La fase aleatoria hace que la media del ensamble sea aproximadamente \(1\). |
| 4 | El promedio del ensamble del movimiento browniano se acerca a cero, pero esto **no basta para demostrar ergodicidad**. |
| 5.1 | Globalmente no se detectó diferencia estadísticamente significativa entre WiFi 5 y WiFi 6. |
| 5.2 | El resultado cambia por piso: Piso 1 es similar; Piso 2 favorece WiFi 6; Piso 3 favorece WiFi 5. |
| 5.3–5.4 | Globalmente no hay asociación entre tecnología e intermitencia; sí la hay en Pisos 2 y 3. |

---

## Punto 1: Teorema del límite central

### Conceptos y fórmulas

Para \(X\sim U(a,b)\):

\[
\mu_X=\frac{a+b}{2},\qquad
\sigma_X^2=\frac{(b-a)^2}{12}.
\]

Si \(T_n=X_1+\cdots+X_n\) y las variables son independientes:

\[
E[T_n]=n\mu_X,\qquad
\operatorname{Var}(T_n)=n\sigma_X^2,\qquad
\sigma_{T_n}=\sqrt n\,\sigma_X.
\]

El TLC indica que, bajo condiciones de independencia y varianza finita, la
distribución estandarizada de la suma se aproxima a una normal al crecer
\(n\). No afirma que la suma sea exactamente normal para todo \(n\).

### Preguntas de sustentación

**1. ¿Qué se observa al sumar 2, 5, 100 y 1000 uniformes \(U(0,1)\)?**

La forma pasa de ser menos parecida a una campana para \(n\) pequeño a ser
claramente aproximadamente normal para \(n=100\) y \(n=1000\). La media se
desplaza a \(n/2\) y la dispersión crece como \(\sqrt{n/12}\).

**2. ¿Cuáles son los valores teóricos para \(U(0,1)\)?**

\[
\mu=0.5,\quad \sigma^2=\frac1{12}\approx0.08333.
\]

Por tanto:

| \(n\) | \(E[T_n]\) | \(\operatorname{Var}(T_n)\) | \(\sigma_{T_n}\) |
|---:|---:|---:|---:|
| 2 | 1 | 0.1667 | 0.4082 |
| 5 | 2.5 | 0.4167 | 0.6455 |
| 100 | 50 | 8.3333 | 2.8868 |
| 1000 | 500 | 83.3333 | 9.1287 |

Los resultados del cuaderno son cercanos porque son estimaciones simuladas:
por ejemplo, para \(n=1000\), la media obtenida fue aproximadamente
499.963 y la varianza 83.108.

**3. ¿La suma de uniformes es exactamente normal?**

No. La suma de \(n\) uniformes tiene una distribución Irwin–Hall cuando son
uniformes \(U(0,1)\). El TLC explica la aproximación normal cuando \(n\) es
grande.

**4. Para exponenciales con \(\lambda=5\), ¿cuál es la media y la desviación
estándar de la suma?**

Cada exponencial tiene:

\[
\mu_X=\frac1\lambda=0.2,\qquad
\sigma_X=\frac1\lambda=0.2,\qquad
\sigma_X^2=\frac1{\lambda^2}=0.04.
\]

Así, para la suma:

\[
E[T_n]=0.2n,\qquad
\sigma_{T_n}=0.2\sqrt n.
\]

La suma de exponenciales iid tiene distribución Gamma (Erlang si \(n\) es
entero), no normal exactamente. Para \(n\) grande se aproxima a una normal.

> **Corrección de notación:** \( \lambda e^{-\lambda x}\) es la densidad
> \(f_X(x)\), no la función de distribución acumulada. La CDF es
> \(F_X(x)=1-e^{-\lambda x}\), para \(x\geq0\).

---

## Punto 2: Sumas de variables aleatorias

### 2.1 Variables uniformes no idénticamente distribuidas

El código usa 120 variables independientes, agrupadas en 20 variables para
cada intervalo. La independencia permite sumar medias y varianzas aunque las
variables no sean idénticamente distribuidas:

\[
E[T]=\sum_i E[X_i],\qquad
\operatorname{Var}(T)=\sum_i\operatorname{Var}(X_i).
\]

Para los primeros intervalos \((0,1),(1,2),\ldots,(5,6)\):

\[
E[T]=360,\qquad \operatorname{Var}(T)=10.
\]

La simulación obtuvo aproximadamente \(360.13\) de media y \(9.91\) de
varianza, por lo que concuerda con la teoría.

En el segundo conjunto de intervalos, el código cambia los parámetros. Para
ese conjunto los valores teóricos son:

\[
E[T]=410,\qquad \operatorname{Var}(T)=78.3333.
\]

La media simulada fue aproximadamente \(409.95\). La varianza simulada
(71.82) presenta una diferencia aleatoria apreciable, pero sigue siendo
compatible con una simulación de solo 1000 realizaciones.

**Pregunta: ¿Por qué se puede aplicar el TLC si las variables no son iid?**

Porque existen versiones del TLC para variables independientes no
idénticamente distribuidas. En este caso las variables tienen medias y
varianzas finitas y ningún grupo domina de forma extrema la suma. La forma
normal observada es una aproximación, no una igualdad exacta.

### 2.2 Uniformes, exponenciales y gaussianas

Para las 30 variables del código:

- 10 uniformes \(U(10,20)\): media total 150 y varianza total
  \(10(10^2/12)=83.3333\).
- 10 exponenciales con \(\lambda=5\): media total 2 y varianza total 0.4.
- 10 gaussianas \(N(30,5^2)\): media total 300 y varianza total 250.

Por tanto:

\[
E[T]=452,\qquad \operatorname{Var}(T)=333.7333,\qquad
\sigma_T\approx18.268.
\]

La simulación obtuvo media 450.495 y varianza 332.312. La diferencia de la
media es razonable debido a que se generaron únicamente 1000 sumas.

**Pregunta: ¿Por qué la suma se acerca a una normal aunque las distribuciones
originales sean diferentes?**

Porque son variables independientes, con varianzas finitas, y el TLC permite
que la suma estandarizada se aproxime a una normal. La distribución de cada
sumando no necesita ser normal.

### 2.3 Variables correlacionadas

El código construye dos factores exponenciales \(X\) y \(Y\):

\[
X_j=2X+j\quad (j=0,\ldots,9),\qquad
Y_j=3Y+j\quad (j=0,\ldots,9).
\]

Las variables del primer bloque dependen todas del mismo \(X\), y las del
segundo bloque dependen todas del mismo \(Y\). Por ello se esperan dos bloques
de correlaciones positivas fuertes, aproximadamente \(1\) dentro de cada
bloque, y correlación cercana a cero entre bloques porque \(X\) y \(Y\) son
independientes.

**Pregunta: ¿Por qué no se debe aplicar el TLC iid directamente aquí?**

Porque las variables no son independientes. La covarianza entre sumandos
contribuye a la varianza:

\[
\operatorname{Var}\left(\sum_i X_i\right)
=\sum_i\operatorname{Var}(X_i)+2\sum_{i<j}\operatorname{Cov}(X_i,X_j).
\]

Ignorar esas covarianzas subestimaría la dispersión del ensamble.

---

## Punto 3: Procesos aleatorios

El proceso es:

\[
S(t)=\cos(2\pi f_ct+\Phi)+1,\qquad
\Phi\sim U(0,2\pi).
\]

Como \(E[\cos(\theta+\Phi)]=0\) cuando la fase es uniforme:

\[
E[S(t)]=1
\]

para todo instante \(t\). Al aumentar el número de realizaciones de 10 a
1000, la media del ensamble fluctúa menos alrededor de 1.

**Pregunta: ¿Qué significa calcular la media del ensamble?**

Para cada instante \(t\), se promedian los valores de todas las realizaciones
en ese instante. Es una aproximación de \(E[S(t)]\).

**Pregunta: ¿La media temporal de una realización siempre es exactamente 1?**

No. Se aproxima a 1 si se observan suficientes ciclos y la discretización es
adecuada. El resultado depende de la duración, la frecuencia y la fase
particular de la realización.

---

## Punto 4: Ergodicidad y movimiento browniano

El movimiento browniano cumple \(E[W(t)]=0\) para cada \(t\). Por eso, al
promediar muchas realizaciones, la media del ensamble debe acercarse a cero.
El cuaderno obtuvo aproximadamente 0.00193, resultado compatible con cero.

**Pregunta: ¿Ese resultado demuestra que el movimiento browniano es ergódico?**

No. Demuestra principalmente convergencia del promedio del ensamble, asociada
a la Ley de los Grandes Números. La ergodicidad exige comparar correctamente
promedios temporales y promedios estadísticos. El movimiento browniano
estándar no es ergódico en el sentido usual de que el promedio temporal de
una trayectoria converja a una constante independiente de la trayectoria.

Una forma de decirlo durante la sustentación es:

> “La media del ensamble se aproxima a cero, pero el cálculo mostrado no prueba
> ergodicidad. En Browniano, el promedio temporal de una trayectoria no se
> estabiliza alrededor de cero de la misma manera que el promedio de un
> proceso estacionario.”

**Detalle de implementación:** en `brownian_motion`, si hay `M` puntos
incluyendo \(t=0\) y \(t=T\), lo más consistente es usar
`dt = T / (M - 1)` y generar `M - 1` incrementos. El código actual usa
`dt=T/M`, por lo que el tiempo final simulado queda ligeramente por debajo de
\(T\). El efecto es pequeño, pero conviene mencionarlo como mejora.

---

## Punto 5: Calidad de señal WiFi

### 5.1 Comparación global

Resultados descriptivos:

| Tecnología | Media (dBm) | Mediana | Desv. estándar | Varianza |
|---|---:|---:|---:|---:|
| WiFi 5 | -67.6622 | -67.05 | 8.9074 | 79.3419 |
| WiFi 6 | -67.0511 | -66.95 | 7.9029 | 62.4558 |

En RSSI, un valor más cercano a cero representa mejor señal. Visualmente son
parecidas, pero la inspección visual no reemplaza una prueba estadística.

**Levene:** \(p=0.4749>0.05\). No se rechaza la igualdad de varianzas.

**Shapiro:** WiFi 5 tiene \(p=0.0298<0.05\), por lo que se rechaza normalidad
para ese grupo; WiFi 6 tiene \(p=0.1312>0.05\). Como al menos un grupo no es
normal, se usa Mann–Whitney.

**Mann–Whitney bilateral:** \(p=0.8034>0.05\). No se rechaza \(H_0\); no hay
evidencia de diferencia global estadísticamente significativa.

**Pregunta: ¿Esto prueba que WiFi 5 y WiFi 6 son idénticos?**

No. Significa que con estos datos no se detectó una diferencia significativa.
“No rechazar \(H_0\)” no equivale a demostrar igualdad absoluta.

> **Error que debe corregirse en el cuaderno:** en la prueba de Mann–Whitney
> se compara `MannWhitney[0]` con 0.05, pero el p-value es `MannWhitney[1]`.
> La condición correcta es:
>
> ```python
> if MannWhitney[1] > 0.05:
>     print("No se rechaza H0: no hay diferencia detectable")
> else:
>     print("Se rechaza H0: hay diferencia estadísticamente significativa")
> ```

Además, como los mismos 90 puntos fueron medidos con ambas tecnologías, el
diseño real es pareado. Si se quiere aprovechar esa estructura, debe evaluarse
una prueba para muestras relacionadas (por ejemplo, Wilcoxon sobre las
diferencias por `punto_id`), no únicamente una prueba para muestras
independientes.

### 5.2 Comparación por piso

| Piso | Resultado | Interpretación |
|---|---|---|
| Piso 1 | \(p=0.4944\) | No hay diferencia significativa; medias similares. |
| Piso 2 | Levene \(p=0.0071\); Mann–Whitney \(p\approx1.997\times10^{-6}\) | Varianzas y distribuciones diferentes; WiFi 6 es mejor en promedio. |
| Piso 3 | Levene \(p=0.5190\); t-test \(p\approx4.14\times10^{-10}\) | Varianzas similares, pero medias diferentes; WiFi 5 es mejor. |

Como los RSSI de Piso 2 son aproximadamente -74.41 para WiFi 5 y -62.26 para
WiFi 6, WiFi 6 es mejor allí porque -62.26 está más cerca de cero. En Piso 3
ocurre lo contrario: -63.37 de WiFi 5 es mejor que -74.72 de WiFi 6.

**Pregunta: ¿Por qué el análisis global puede ocultar información?**

Porque al mezclar pisos se compensan diferencias opuestas: una tecnología
puede ser mejor en un piso y peor en otro. Por eso una decisión de migración
debe considerar la ubicación y no solo el promedio global.

### 5.3–5.4 Intermitencias

Tabla global:

| Tecnología | No | Sí | Tasa de intermitencia |
|---|---:|---:|---:|
| WiFi 5 | 44 | 46 | \(46/90=51.11\%\) |
| WiFi 6 | 45 | 45 | \(45/90=50.00\%\) |

La prueba chi-cuadrado global obtuvo \(p=0.8815>0.05\). No se rechaza la
hipótesis de independencia: no hay evidencia de asociación global entre
tecnología e intermitencia.

Por piso:

- **Piso 1:** \(p=0.6023\); no hay asociación significativa.
- **Piso 2:** \(p<0.0001\); sí hay asociación. WiFi 5 tiene 28 intermitencias
  frente a 11 de WiFi 6.
- **Piso 3:** \(p<0.0001\); sí hay asociación. WiFi 5 tiene 4 intermitencias
  frente a 22 de WiFi 6.

**Pregunta: ¿Cómo se interpreta una asociación significativa?**

Significa que las frecuencias de intermitencia dependen de la tecnología en
ese piso; no significa por sí sola que la tecnología sea la única causa. En
Piso 2 los datos favorecen WiFi 6 y en Piso 3 favorecen WiFi 5.

---

## Preguntas rápidas para practicar

1. **¿Qué diferencia hay entre media y varianza de una suma?**  
   La media siempre se suma; la varianza se suma directamente solo si los
   sumandos son independientes. Si hay dependencia, deben incluirse las
   covarianzas.

2. **¿Qué significa \(p<0.05\)?**  
   Bajo \(H_0\), el resultado observado sería poco probable. Se rechaza
   \(H_0\) al nivel del 5%; no se afirma que la hipótesis alternativa sea
   absolutamente cierta.

3. **¿Qué significa \(p>0.05\)?**  
   No hay evidencia suficiente para rechazar \(H_0\). No demuestra que \(H_0\)
   sea verdadera.

4. **¿Cuándo se usa t-test y cuándo Mann–Whitney?**  
   El t-test compara medias bajo supuestos de normalidad y, según la versión,
   varianzas apropiadas. Mann–Whitney es una alternativa no paramétrica para
   comparar la posición/distribución de dos grupos.

5. **¿Qué significan las colas de Mann–Whitney?**  
   `two-sided` busca cualquier diferencia; `less` plantea que la primera
   muestra tiende a valores menores que la segunda; `greater` plantea que la
   primera tiende a valores mayores que la segunda.

6. **¿Qué hipótesis prueba chi-cuadrado de independencia?**  
   \(H_0\): las variables categóricas son independientes.  
   \(H_1\): existe asociación entre ellas.

7. **¿Cuál es la conclusión de ingeniería más completa?**  
   No conviene migrar basándose solo en el promedio global. WiFi 6 mejora
   claramente el Piso 2, WiFi 5 funciona mejor en el Piso 3 y el Piso 1 no
   muestra diferencia significativa. La decisión debe incorporar costos,
   cobertura, intermitencias y el carácter pareado de las mediciones.

## Correcciones y observaciones finales

- Cambiar `MannWhitney[0]` por `MannWhitney[1]` en la condición de decisión.
- Escribir “no se rechaza \(H_0\)” en vez de “se acepta \(H_0\)”.
- Corregir la notación de la exponencial: \(f(x)=\lambda e^{-\lambda x}\)
  es PDF; \(F(x)=1-e^{-\lambda x}\) es CDF.
- Aclarar que \(N(\mu,\sigma^2)\) usa la varianza como segundo parámetro, no
  la desviación estándar.
- En el segundo ejemplo de 2.1, usar los valores teóricos \(410\) y
  \(78.3333\), porque los valores \(360\) y \(10\) corresponden al primer
  conjunto de intervalos.
- No presentar el promedio mostrado del Browniano como prueba de ergodicidad.
- Corregir la referencia de RSSI “80 dBm” a “-80 dBm” si se conserva esa
  frase, porque los valores de señal WiFi son negativos.
