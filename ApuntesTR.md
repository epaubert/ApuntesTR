---
title: "Apuntes para teoría"
subtitle: "Tecnologías de Red"
author: 
- "Enrique Paubert Reca"
geometry: margin=2.5cm
mainfont: LiberationSerif-Regular.ttf
mathfont: latinmodern-math.otf
monofont: monospace
toc: true
indent: true
lang: es-ES
documetclass: report
classoption: 
- 12pt
- a4paper
- notitlepage
- twocolumn
---
<!-- pandoc ApuntesTR.md -o ApuntesTR.pdf --pdf-engine=pdflatex -->
# Tema 1: Introducción
* **Fuente** o **Emisor**: origen de la información.
* **Destino**: destinatario de la información transmitida.
* **Canal** o **Medio de transmisión**: Soporte fisico que realiza el transporte de la información.
* **Transmisor**: interfaz entre fuente y canal.
* **Información**: Conjunto de datos al que se dota e significado.

## Redes de computadores:
### Características:
* **Interconexión:** existen uno o varios canales de transmisión que permmiten la comunicación entre los distintos equipos de la red.
* **Autonomía:** Cada equipo de la red es independiente, al contrario que en el caso de un mainframe con terminales.

### Elementos:
* **Nodo:** uno de los equipos que componen la red
* **Host:** nodos o quipos terminales de datos.
* **Subred:** conjunto de elementos que posibilitan la Interconexión entre los hosts. Formados por:
	* **Nodos de conmutación:** transportan los datos de un origen a un destino.
	* **Lineas de conmutación:** canales de conmunicación.

### Tipos de Interconexión:
* **Difusión:** Todos los nodos están conecados a un único medio.
* **Punto a Punto:** Cada nodo está conectado a al menos otro nodo por un medio exclusivo a ellos dos.

### Tipos de Comunicaciones:
* **Salto a salto:** entre cada par de nodos adjacentes.
* **Extremo a extremo:** entre los nodos terminales, suele necesitar de otros nodos intermedios.

### Clasificación de redes:
* **PAN**: weareables.
* **LAN**: casas, oficinas, edificios...
* **WAN**: intranets que cubren paises o continentes enteros o Internet.

## Modelos OSI y TCP/IP:
### OSI
* **Aplicación:** servicio final.
* **Presentación:** cifrado o codificación.
* **Sesión:** gestiona turno de palabra.
* **Transporte:** control de flujo y errores extremo a extremo.
* **Red:** encaminamiento y control de congestión.
* **Enlace:** control de flujo y errores salto a salto.
* **Fisica:** intercambio de bits en el medio de transmisión.

### TCP/IP
* **Aplicación:** servicio final.
* **Transporte:** control de flujo, errores, congestión y conexión extremo a extremo.
* **Red:** encaminamiento y fragmentación.

TCP/IP es una red software, existen protocolos para capas inferiores pero consisten en adaptar la red física subyacente a este modelo, no depende de una tecnología concreta.

\begin{table}[]
\begin{tabular}{|c|c|}
\hline
\textbf{OSI} & \textbf{TCP/IP}\\ \hline
Aplicación   & Aplicación     \\ 
Presentación &                \\ \hline
Sesión       & Transporte     \\ 
Transporte   &                \\ \hline
Red          & Red            \\ \hline
Enlace       & Red Subyacente \\ 
Fisica       &                \\ \hline
\end{tabular}
\end{table}

### Terminología:
* Las capas inferiores *proveen* servicios y las superiores son *usuarias de servicios*.
* *Entidades de nivel N*: Los elementos de cada capa, siendo N la capa en la que están.
* *Entidades paritarias*: Entidades de nivel N en el emisor y receptor.
* Comunicación:
	* *Real* o *vertical*: El flujo entre capas adjacentes.
	* *Virtual* u *horizontal*: Desde el punto de vista de entidades paritarias, extremo a extremo, capa a capa. Encapsulación usando cabezeras.
* *Protocolo*: conjunto de reglas y convenciones a aplicar en una comunicación entre dos entidades paritarias con objeto de llevar a cabo una cierta función o servicio.
* *Arquitectura de red*: Conjunto de capas y protocolos asociados.
* *Pila de protocolos*: Especificación en capas de protocolos que constituyen una arquitectura.

OSI no es una arquitectura de red porque no tiene pila de protocolos, TCP/IP si.

* *SAP* o *Service Access Point*: interfaz entre capas adjacentes.
* *SDU* o *Service Data Unit*: datos manejados por la entidad que proceden de la capa inmediatamente superior.
* *PDU* o *Protocol Data Unit*: Añadida a la SDU para realizar una función específica.
* *Orientado a conexión*: se establece la conexión antes e enviar datos (TCP).
* *No orientado a conexión*: se envian los datos sin establecer conexión previa (UDP).
* Servicios *confirmados* o *no confirmados*.
* *Primitiva (de servicio)*: cada uno de los procesos elementales que en que se desarrolla un servicio. Existen 4:
	* *Solicitud*
	* *Indicación*
	* *Respuesta*
	* *Confirmación*

# Tema 2: Transmisión de datos
* **Señal:** Parámetro físico que varía a lo largo del tiempo, espacio u otra variable. Suelen ser:
* **Señal analógica:** Señal continua tanto en tiempo como en amplitud.
* **Señal digital:** Señal discreta tanto en tiempo como en amplitud.

## Fourier
* **Series de Fourier:** Toda función puede aproximarse mediante sumatorias de las funciones seno y conseno.
* **Transformada de Fourier:** Representación espectral de una señal no periódica.
* **Ancho de banda:** el rango de frecuencias donde se concentra toda o la mayor parte de la energía espectral de una señal  
El análisis de Fourier permite representar una señal tanto en base al tiempo como a la frecuencia, lo que facilita su estudio.

## Muestreo de señales
* **Teorema de Nyquist:** Para muestrear una señal sin perder información la frecuencia de muestreo debe de ser al menos el doble que la frecuencia máxima de la señal. $f_s \ge 2*f_m$

## Medios de transmisión
Los canales de comunicación reales tienen un ancho de banda finito, actuan como un filtro (de paso baja generalmente) y siempre introducen distorsiones y ruido que pueden dar lugar a pérdida de información y errores.

* **Capacidad de canal:** la velocidad de transmisión de datos de un canal $= C = V_{trans-max} = 2*W (pulsos/s)$, siendo $W$ el ancho de banda del canal en Hz.
* **Baudio:** Unidad utilizada para denotar la velocidad de modulación, 1 baudio = 1 estado de señalización/segundo.
* **Velocidad de transmisión:** $V_{transmisión} (bits/segundo) = V_{modulación}*log_2 N$, siendo N el número de bits que puede transmitirse en un pulso.
* **SNR:** Signal-to-Noise-Ratio, el cocciente de la potencia de la señal y la potencia del ruido, $\frac{S}{R}$. Suele expresarse en decibelios, $SNR_{dB} = 10*log_{10} SNR$. Hay que intentar maximizarlo.
* Es demostrable que $N \le \sqrt{1+\frac{S}{R}}$ 
* La **velocidad de transmisión máxima** para un canal de $W$ Hz y $SNR = \frac{S}{R}$: 
$C = W*log_2(1+\frac{S}{R})$. (Teorema de Shannon).

### Limitaciones
* **Atenuación:** Cuanto decae la señal con la distancia. En decibelios: $10 * log_{10}\frac{A_o}{A_d}$, siendo $A_o$ la amplitud de la señal original y $A_d$ la amplitud a la distancia $d$. Se mitiga con repetidores, y en caso de que los fitro de paso baja o bando, con ecualizadores de señal.
* **Distorsión de retardo:** Dado que las frecuencias diferentes viajan a velocidades diferentes puede ocurrir *interferencia intersimbólica*. Se mitiga igualmente con repetidores y retrasando las señales más rápidas.
* **Ruido:** puede tener muchas fuentes:
	- Térmico.
	- Intermodulación.
	- Eco.
	- Diafonía, *crosstalk*.
	- Impulsivo.

### Tipos de medios de transmisión

**Guiados:** cables, ver tabla.
\begin{table}[]
\begin{tabular}{|l|lll}
\hline
\textbf{Med. Guiados} & \multicolumn{1}{l|}{Par trenz.} & \multicolumn{1}{l|}{Coax.} & \multicolumn{1}{l|}{Fibra} \\ \hline
Ancho de banda  & M-GHz  & GHz  & THz  \\ \cline{1-1}
Velocidad       & M-Gbps & Gbps & Tbps \\ \cline{1-1}
Aten. (dB/km)   & 3      & 2    & 0,3  \\ \cline{1-1}
Km entre repet. & 2      & 10   & 50   \\ \cline{1-1}
\end{tabular}
\end{table}

**No guiados:** la atmósfera.

\begin{table}[]
\begin{tabular}{|c|cc}
\hline
\textbf{No Guiados} & \multicolumn{1}{c|}{Frec.} & \multicolumn{1}{c|}{Direcionalidad} \\ \hline
Radio            & 3-300 MHz                        & Omnidirecional                       \\ \cline{1-1}
Microondas       & 0,3-30G Hz                      & 3-4 grados                           \\ \cline{1-1}
Infrared/láser & \textgreater 30 GHz                & Extrema                                \\ \cline{1-1}
\end{tabular}
\end{table}

* Atenuación: $A = 10 * log_{10}(\frac{4\pi d}{\lambda})^2$ dB, $d$ distancia, $\lambda$ longitud de onda. Aumenta con la frecuencia.
* Tipos:
	* Radio: Afectado por meteorología. Difusión de radio y televisión, WLAN, redes móviles.
	* Microondas: Afectado por meteorología. Altamente direccional -> comunicaciones punto a punto. 
		- Terrestres: < 3GHz, ondas reflejadas en ionosfera.
		- Satelitales: > 3GHz, GEO (36.000 km, 250 ms) o LEO
			- Separación mínima entre satélites de entre 3 y 4 grados dependiendo de la frecuencia.
			- Frecuencias upstream y downstream distintas para evitar interferencias. 
	* Infrarojos/láser: extremadamente direccionales, gran atenuación, afectado por cualquier objeto en el haz. Controles remotos.

## Modos de transmisión, modulación
1. *Simplex*: Un solo sentido.
2. *semi-duplex*: *(half-duplex)* Un solo sentido en cada momento, reversible.
3. *duplex*: *(full-duplex)* bidireccional en todo momento.

### Señal analógica, transmisión digital
* Conversión AD:
	1. Muestreo (Nyquist).
	2. Cuantización:
		- Unifome o logarítimica.
		- Absoluta o diferencial.
	3. Codificación:
		- PAM: Pulse Amplitude Modulation.
		- PWM: Pulse Width Modulation.
		- PPM: Pulse Position Modulation.
		- **PCM**: Pulse Code Modulation. $b_{bits/s} = f*log_2N$
		- modulación delta.

### Señal digital, transmisión digital
Distintos tipos de códigos PCM. Características:

* Espectro.
* Capacidad de sincronismo.
* Capacidad de detección de errores.
* Complejidad.

Tipos:

#### **NRZ**: *Non-Return to Zero*. 
* Representación: dos valores, $0$ y $+V$
* Variantes: NRZ, NRZ-I(nverted), NRZ-L(evel), NRZ-M(ark).
* Ancho de banda reducido.
* componente continua.
* Sincronismo nulo o poco dependiendo de la variante.
* Detección de errores nula.
* Sencillo de implementear.

#### **Bipolar AMI**: *Alternate Mark Inversion*. 
* Representación: tres valores, $0$, $+V$ y $-V$
* Más frecuencias para el mismo ancho de banda que NRZ.
* no existe componente continua.
* Sincronismo mejorado, posible *violación de código*.
* Más compleja que NRZ.

#### **Manchester**:
* Representación: 
	- Transición en medio de cada bit.
	- $0$ y $+V$.
	- 0 baja 1 sube.
* Ancho de banda: 2 x NRZ
* Componente continua eliminable cambiando $0$ por $-V$.
* Sincronismo: *código de autoreloj*.
* Detección de errores casi nula.
* Implemetación igual de sencilla que NRZ.

#### **Manchester diferencial**:
* Representación:
	- Transición en medio de cada bit.
	- $0$ -> transición al inicio del intervalo
	- $1$ -> NO transición al inicio del intervalo
* Muy similar a Manchester.
* Detección de algunos errores.
* Mayor complejidad.

#### Otros:
* *B8ZS*: Bipolar with 8-Zeros Sustitution.
* *HDB3*: High Density with Bipolar 3-zeros.
* *4B/5B-NRZI*: Redes LAN.

### Señal digital, transmisión analógica
* **Señal modulante:** d(t), datos originales.
* **Señal portadora:** c(t), en la que se basa la transmisión.
* **Señal modulada:** m(t), señal final.

#### Tipos de transmisión:
* **ASK:** *Amplitude Shift Keyring*, se asigna una una amplitud al 1 y y otra al 0.
* **FSK:** *Frequency Shift Keyring*, se asigna una una frecuencia al 1 y y otra al 0.
* **PSK:** *Phase Shift Keyring*, se cambia e fase dependiendo de si el valor es 1 o 0.
* **QAM:** *Quadrature Shift Keyring*, combinación de ASK y PSK.

Estado de señalización: Cada uno de los valores que puede tomar la señal modulada.

### Señal analógica, transmisión analógica
#### AM (Amplitude Modulation)  
* **AM-PS:** *Portadora Suprimida*, muy sensible a variaciones de frecuencia o fase.
	* $m(t) = d(t) * cos(w_ct)$
* **AM-AP:** *Alta Potencia*
	* $m(t) = [A + d(t)] * cos(w_ct)$, con $A > |d(t)_{max}|$

AMDBL-PS y AMDBL-PS **(Doble Banda Lateral)** solo utilizan la mitad del ancho de banda, AMBLU-PS y AMBLU-PS **(Banda Lateral Única)** son más eficientes eliminando una de las bandas laterales.

*BLR o banda lateral residual:* No se puede filtrar perfectamente una banda lateral.

#### Modulación angular
* $m(t) = A * cos( w_ct + \Phi(t))$
* **PM:** *Phase Modulation*
	* $\Phi(t) = k_p * d(t)$
	* $k_p$: índice de modulación de fase.
* **FM:** *Frequency Modulation*
	* $\frac{d\Phi(t)}{dt} = k_f * d(t)$
	* $k_f$: índice de modulación de frecuencia.

La televisión analógica usan AMBLR para el video y FM para el audio.

## Interfaces
* **DTE**: Data Terminal Equipment
* **DCE**: Data Cricuit Equipment

Transmisión en paralelo: más velocidad pero más coste -> solo en muy cortas distancias.

**Problema:** Sincronización e relojes para la comunicación.  
**Soluciones:**

1. Transmisión asincrona:
	* Corta duración.
	* Patrones acordados.
	* Bloques pequeños.
	* Marca de inicio.
2. Transmisión sincrona:
	* Grandes bloques de datos.
	* Delimitadores preestablecidos al inicio y fin.
	* Información de reloj en la transmisión.

**Especificaciones:**

* *Mecánicas*: conectores
* *Eléctricas*: valores de 0 y 1
* *Funcionales*: interpretar señales
* *De procedimiento*: protocolos

#### RS-232
* Basado en UART.

**Especificaciones:**

* *Mecánicas*: 25 o 9 contactos
* *Eléctricas*:
	* 1 lógico $\le$ -3V; 0 $\ge$ +3 voltios
	* cables de: datos, control, temporización y tierra
* *Funcionales*: interpretar señales
* *De procedimiento*: RTS-CTS

#### USB
Universal Serial Bus.

* *Mecánicas*: 4 conectores en 2.0 y 9 en 3.0.
* *Eléctricas*: 1 de 5V, 2 de datos, 1 GND.
* *Funcionales*: software.
* *De procedimiento*: software.

#### RJ-45
* *Mecánicas*: 8 contactos.
* *Eléctricas*: 2 pares para comunicación full duplex.
* *Funcionales*: depende de la aplicación.
* *De procedimiento*: depende de la aplicación.

# Tema 3: Control de acceso al medio
Capa enlace: 2 subcapas
	- Subcapa de enlace.
	- Subcapa MAC.

## Multiplexación
* **División de frecuencias:** Todos transmiten a la vez, cada uno en su frecuencia. Radiodifusión y ADSL. *Banda ancha*.
* **División de tiempo:** Transmiten por turnos utilizando el ancho de banda completo. Telefonía digital. *Banda base*.

### FDM (*Frequency Division Multiplexing*)
* Tramsmisión analógica, señal analógica o digital.
* Cada emisor tiene una frecuencia portadora asignada.
* Envio utilizando modulación AM, ASK, FM, PSK, PM...
* Recepción o sintonización: 
	1. Paso banda al rango de frecuencia deseado.
	2. Demodulación para obtener la señal original.

$B > \Sigma_{i=1}^n B_i$: el ancho de banda total ($B$) debe de ser superior a la suma de los anchos de banda de la señales moduladas multiplexadas ($B_i$). Esta diferencia son las **bandas de guarda** para evitar interferencias.

* También conocida como FDMA.
* WDMA (*Wavelenght Division Multiple Access*), variante para fibra óptica.

### TDM (*Time Division Multiplexing*)
* Señales normalmente digitales.
* (De)multiplexores -> Conmutadores sincrnonizados temporalmente.
* Toma $l$ bits de las $n$ fuentes -> *tramas de bits* con $n$ *slots*
* Delimitadores entre *tramas* para detectar pérdida de sincronización.

$V > \Sigma_{i=1}^n v_i$, $v_i$ la velocidad de transmisión de la fuente $i$ y $V$ la velocidad de salida del mutiplexor.

* Si la relación entre velocidades de las fuentes no es entera, se insertan bits de relleno para hacerla entera y poder cuadrar la división.
* Bufferes en cada entrada de los multiplexores para almacenar mientras se procesa otra entrada y amortiguar variaciones en el tiempo.
* También conocida como TDMA.

Tanto FDM como TDM implican una división estática => Desaprovechamiento si no todas las fuentes están transmitiendo:

$E_{ficiencia} = \frac{K_{num-medio-emisiones}}{N_{fuentes-totales}}$

**Solución:** Técnicas de acceso dinámicas -> ATDM (*Anyncronus Time Division Multiplexing*).

$E_{ficiencia} = \frac{K_{num-medio-emisiones}}{D_{atos(bits)}+H_{eader(bits)}}$
 
### Técnicas de espectro expandido
Uso de más ancho de banda del necesario para:

1. Reducir interferencias
2. Dificultar la detección cuando hay ruido
3. Mejorar la privacidad.

Expansión del expectro mediante secuencias pseudoaleatorias en la codificación y decodificación. Dos(2) tipos: *secuencia directa* y *salto de frecuencias*.

#### Secuencia directa (DSSS o CDMA)
* Duración bit de secuencia pseudoaleatoria < Duración bit señal original -> *minibit* o *chip*.
* Emisor: función XOR -> modulación -> transmisión
* Receptor: transmisión -> modulación -> función XOR
* Ancho de banda secuencia transmitida = ancho de banda de la secuencia pseudoaleatoria > ancho de banda señal original.

#### Salto de frecuencia (FHSS o solo FH)
* Secuencia pseudoaleatoria para elegir la frecuencia utilizada para modular.
* Distintas frecuencias portadoras a lo largo del tiempo.

Las secuencias pseudoaleatorias (SPAs) deben ser:

* Ortogonales: Garantiza la recuperación de datos. $$m(t)= \begin{cases} 0 $ si $SPA \neq recepcción \\ 1 $ si $SPA = recepcción  \end{cases}$$
* Infinitas: para evitar la predicción, privacidad. necesidad de sincronización emisor-receptor.

### Discusión
Según la teoría de colas, las técnicas estáticas tienen un retardo de acceso al medio $N$ veces mayor que las dinámicas o multiplexadas, siendo $N$ las divisiones estáticas del canal.

## Técnicas de contención
* Naturaleza aleatoria, competición entre estaciones para acceder al medio.
* Se desconoce cuando una estación concreta podrá hacer una transmisión.
* El acceso al canál no está garantizado en un tiempo finito. 
* Colisiones inevitables, habrá que retrasmitir las tramas dañadas tras un *tiempo de retroceso* aleatorio.
* Ausencia de coordinación entre estaciones, reglas de protocolo comunes que todas las estaciones comparten y respetan.
* Se intenta evitar colisiones y minimizar el retraso cuando ocurren.

### Aloha puro y ranurado
* Originaria de Hawaii para comunicación entre islas.
* Cada estación transmite cuando tiene datos para hacerlo.
* $T_{trama} (seg) = \frac{L_{ongitud-trama-datos} (bits)} {V_{elcidad-transmision} (bits/seg)}$
* $S$: Tasa ofertada (tasa de salida), $0 \le  S \le 1$.
* $G$: Tasa demandada (velocidad e llegada total) (peticiones/ranura).
* $S_{ALOHA-PURO}=G*e^{-2G}$
* $prob_{éxito} = \frac{G}{S} = e^{-2G}$
* $\varepsilon = \frac{G}{S} -1 = e^{-2G} -1$, valor esperado del número medio de intentos fallidos.
* $E[T_{ALOHA}] = t_{trama} + \varepsilon*(t_{trama}+B)$, $B$: tiempo de retroceso medio.
* Aloha ranurado, variante mejorada en la que solo se puede transmitir en instantes de tiempo específicos:
	* $S_{ALOHA-RANURADO}=G*e^{-G}$
	* $prob_{éxito} = \frac{G}{S} = e^{-G}$
	* $\varepsilon = \frac{G}{S} -1 = e^{-G} -1$
	* Más eficiente que ALOHA *puro*.

### CSMA (*Carrier Sense Multiple Access*)
Antes de transmitir la estación comprueba si el medio está libre. 3 variantes:

1. 1-persistente:
	* si el canal está ocupado espera a que esté libre.
	* si el canal está libre transimte
2. no-persistente:
	* si el canal está ocupado espera un tiempo aleatorio.
	* si el canal está libre transimte
3. p-persistente:
	* si el canal está ocupado espera a que esté libre.
	* si el canal está libre transmite o espera con probabilidades p y 1-p respectivamente
* **Colisiones** si 2 (o más) estaciones intentan transmitir a la vez o por retardo del canal.
* Baja carga: $E_{ficiencia}[1-persistente] > E[no-persistente]$
* Alta carga: $E[1-persistente] < E[no-persistente]$
* p-persistente: $p$ se puede ajustar dependiendo de la carga esperada, pero es estático.
* Más eficiente que los esquemas ALOHA.

### CSMA/CD
* CSMA desaprovecha el canal ya que sigue transmitiendo cuando se ha producido una colisión.
* Solución: Detección de colisiones mientras se transmite y interrupción de la transmisión en caso de colisión.
* /CD: *Colisión detection*.
* *Intervalo de contención*: $\tau = 2t_p$, tiempo que tardaría en darse cuenta de una colisión.
* $R =$ número medio de intervalos de contención hasta tener éxito.
* $t_p = \frac{D_{istancia-max}}{V_{elocidad-propagación}}$
<!-- * $P_{éxito-transmitir} = \binom{N}{1}*P*(1-P)^{N-1} = \frac{N!}{1!*(N-1)!}*P*(1-P)^{N-1}$ -->
* $E_{speranza}[R] = \frac{1-P_{éxito}}{P_{éxito}}$
* $a = \frac{t_p}{t_{trama}}$  
* **Eficiencia:** $U = \frac{t_{trama}}{t_{trama}+R*2*T_{p}} = \frac{1}{1+2a(\frac{1-P_{éxito}}{P_{éxito}})}$
* Las técnicas de contención en general comporta mejor en baja carga:
	* si $N -> 1, P_{éxito} = U = 1$
	* si $N -> \infty, P_{éxito} = U = 0$
* El tiempo de acceso al medio no está garantizado.

### CSMA/CA o MACA
* /CA: *Colision avoidance*.
* Diseñada para redes inalámbricas para solucionar el problema de la estación oculta.
* Implementa *sondeo de portadora virtual* o *virtual carrier sense*.
	* $RTS$: Request to send
	* $CTS$: Clear to send
* **Colisiones:** en tramas RTS.
* $t_{sondeo} = t_{RTS} + t_{CTS} + 2*t_p$
* $t_{RTS} \approx t_{CTS} \rightarrow t_{CTRL} \ll t_{datos}$, generalmente despreciables.
* $U = \frac{t_{trama}}{t_{datos} + R*t_{sondeo}} = \frac{1}{1+a(\frac{2-P_{éxito}}{P_{éxito}})}$
* Menos eficiente que CSMA/CD, pero necesario si puede haber estación oculta.

## Protocolos libres de colisión
Son esquemas planificados.

### Basados en reserva
Intervalo de tiempo *de reserva* con tantas "minirarnuras" como estaciones.

1. Cada estación hace reserva en su "miniranura".
2. Las estaciones que reservaron transmiten de forma secuencial.
3. Vuelta al 1.

* $d$: tamaño de las tramas de datos (bits).
* $N$: número de estaciones.
* $U_{baja-carga} = \frac{d}{d+N}$
* $U_{alta-carga} = \frac{d}{d+1}$
* Mejor eficiencia en alta carga.
* Tiempo máximo de acceso al medio acotado.
* Rotación de posiciones en el intervalo *de reserva* para asegurar equidad.

### Basados en consulta
Métodos de consulta:

1. *Centralizados:* Central lanza una trama de sondeo, el resto responden si quieren transmitir o no.
2. *Distribuidos:* También llamados *paso de testigo* porque utilizan un *testigo* o *token*.
	1. El testigo se encuentra libre en el medio.
	2. Una estación que desea transmitir lo "captura", transmite y devuelve el testigo al medio.

**Utilización:**

* $U_{baja-carga} = \frac{t_{trama}}{t_{trama} + t_p}$
* $U_{alta-carga} = \frac{t_{trama}}{t_{trama} + \frac{t_p}{N}}$

Estas fórmulas suponen que:

1. Cada estación solo transmite una trama cada vez que tiene el testigo.
2. Es una red en anillo equiespaciada.
3. El tiempo de generación de testigo es despreciable.

* Deben de establecerse mecanismos para posibles problemas como la posible pérdida de *testigo* o la monopolización del mismo.
* Tiempo máximo de acceso al medio acotado.


\begin{table}[]
\begin{tabular}{|l|ll}
\hline
\textbf{Contención}\\\textbf{limitada} & \multicolumn{1}{l|}{Colisión} & \multicolumn{1}{l|}{Planificados} \\ \hline
Alta carga    & Peor       & Mejor   \\ \cline{1-1}
Baja carga    & Mejor      & Peor    \\ \cline{1-1}
Tiempo acceso & No Acotado & Acotado \\ \cline{1-1}
\end{tabular}
\end{table}

## Jerarquias digitales síncronas
### EEUU, Canadá y Japón:
* Telefonía: Sistema T-[0-5]/DS-[0-5], B8ZS
* Fibra: SONET

### Internacional:
* Telefonía: Sistema E-[0-5], HDB3
* Fibra: SDH

# Tema 4: Control de enlace
## Delimitación de tramas
* Para transmitir un mensaje es necesario fragmentarlo en tramas o *frames*.
* Problemas: Tamaño y delimitación.

### Tamaño
* Si son muy grandes:
	* Son más vulnerables a errores.
	* Ocupan durante más tiempo el canal.
	* Se necesitan memorias más grandes.
* Si son muy cortos:
	* Ineficiencia.

En cada caso se elije un tamaño de trama razonablemente eficiente dependiendo del entorno de transmisiones reales.

### Delimitación
Caracteres de inicio y fin de bloque de datos. 2 tipos:

1. Delimitación mediante **caracteres** de principio y fin con inserción de **caracteres**.
	* 1 o más caracteres especiales para indicar el principio y fin de una trama.
	* ASCII: DLE STX y DLE ETX.
	* Si normalmente en el mensaje del emisor habría un DLE, se añade otro para denotar que no se está usando como delimitador.
	* Mismo principio que usar "\\\\" para poner "\\" en LaTeX y otros lenguajes.
2. Delimitación mediante **bits** de principio y fin con inserción de **bits**.
	* En lugar de caracteres ASCII, secuencias de bits.
	* LLC utiliza la cadena 01111110 (~ en ASCII) como octeto delimitador.
	* El emisor siempre inserta un 0 después de cada 5 valores 1 consecutivos para evitar falsos delimitadores.
3. Otros esquemas:
	* Cuenta de caracteres: La cabecera indica cuantos bytes se van a enviar para que receptor sepa cuándo termina la trama.
	* Violación de código: Utilización de símbolos no previstos en el protocolo.
* En la realidad es habitual que se combinen técnicas como la delimitación y la cuenta de caracteres.
* Esta delimitación es el último paso realizado por la capa de enlace de la entidad emisora.

## Códigos de gestion de errores
### Definiciones:
* *Codificación de errores*: técnias para determinar la ocurrencia o no de errores debidos al canal de transmisión. Redundancia utilizando **códigos**.
* La mayoría son **códigos de bloque**: bloques de longitud $n$, con $2^n$ combinaciones posibles pero no todas válidas.
* Dados $k$ bits de datos, se transforman en un bloque de $n$ bits.
* *palabra código* o *codeword*: combinación de bits válida en un código de bloque.
* *Vocabulario*: todas las *codewords* de un código de bloque.
* *Check bits*: $r = n-k$, bits de comprobación o redundancia. Obtenidos a partir de los datos y normalmente añadidos al final.
* Se denominan como "código $(n, k)$" y $\frac{k}{n}$ es su *velocidad* o *razón de código*.
* *Distancia de Hamming*: el número de posiciones que difieren entre dos secuencias de bits.
* *Distancia de Hamming de un código*, $d_H$: La distancia de Hamming mínima en un vocabulario.

### Proceso:
* El receptor sabra si ha habido un error si la palabra recibida no está en el vocabulario.
* Para **detectar** $e$ errores, $d_H \ge e+1$.
* Para **corregir** $e$ errores, $d_H \ge 2*e+1$.
* Es mucho más eficiente detectar errores y solicitar un reenvio (ARQ).

### Códigos de corrección
Ejemplo: Código de Hamming: los datos se colocan en las posiciones no potenicia de 2 y la paridad en los potencia de 2. Tipo entrelazado.

### Códigos de detección
* Ejemplo 1: Paridad
	* Bit de paridad.
	* Esquiemas de paridad (matrices).
	* Internet: *complemento a 1 de la suma complemento a 1 de las palanras de 16 bits que componen la secuencia de bits a transmitir*. Se envían los datos y un *chechsum*.
* Ejemplo 2: Códigos CRC (Cyclic Redundance Code)
	* Si se realiza una rotación de una *codeword* se obtiene otra palabra código.
	* Lineal: cualquier combinación lineal de dos *codewords* es otra *codeword*.
	* Todo el vocabulario se puede obtener a partir de un **polinomio generador** de grado $n$.
	* El polinomio generador tiene ciertas resticciones:
		* Al menos 2 términos.
		* No ser divisor de errores de 2 bits.
		* Debe de poder descomponerse en factores $(x+1)$.
		* Siendo un polinomio de grado $r$, debe demostrar que puede detectar errores a ráfagas de longitud $\le r$.

### Códigos convolucionales
* Para canales en lugar de bloques.
* Existe memoria, la codificación depende de la historia previa.
* Pueden describirse a partir de su matriz generadora, especificada como:
	* Diagrama de arbol.
	* Diagrama trellis.
	* Diagrama de estados.
* Decodificación: La *codeword* más cercana ($d_H$) a la recibida mediante el *algoritmo de Viterbi*.

## Control de flujo
Técnicas o esquemas que consigan una **transmisión ordenada, dialogada y eficiente** entre el emisor y el receptor.  
El receptor debe marcar el ritmo de la transmisión $\Rightarrow$ **realimentación** $\Rightarrow$ no es posible en *simplex*.

#### Eficiencia y tasas de transferencia
* **Tasa de transferencia** $(R)$ o *velocidad de transmisión* $(v_t)$: cantidad de información transmitida por unidad de tiempo (bits/segundo).
	* *Tasa de transferencia nominal* $(R)$: Velocidad de transmisión máxima del enlance.
	* *Tasa de transferencia efectiva* $(R_{ef})$: Cantidad de información útil transmitida.
* **Utilización del enlace** $(U)$: La fracción de la capacidad del enlace que se usa para transmitir información.
	* $U = \frac{R_{ef}}{R}$.
	* $U \le 1$.
	* Suele expresarse en %.
* Supondremos que todos los bits de trama son útiles, por tanto:
	* $R_{ef} = \frac{t_{útil}}{t_{total}} R$
	* $U = \frac{t_{útil}}{t_{total}}$

#### Representación del intercambio de tramas
* **Tiempo de trama** $(t_f)$: lo tarda en emitirse una trama. Desde que se empieza a emitir el primer bit hasta que termina de emitir el último.
* **Tiempo de propagación** $(t_p)$: lo que tarda una trama en propagarse por el medio desde el emisor al receptor. Desde que el emisor termina de enviar la trama hasta que el receptor termina de recibirla.

Ver imagen 4.10, pág. 120.

### Señalización
2 Esquemas:

1. Emisor envia datos, receptor manda señales de parada y de continación.
2. Emisor manda señal e solicitud y receptor manda señal de aceptación (RTS-CTS).

Estos dos a su vez pueden usar:

* Señalización en banda (*in-band*): las señales de control usan el mismo canal que los datos.
* Señalización fuera de banda (*out-of-band*): las señales de control y de datos utilizan distintos canales.

### Protocolo de parada y espera
* El emisor no manda una trama hasta que no recibe la trama $ACK_{nowledgment}$ del receptor.
* Inviable en caso de errores.
* Muy simple.
* Muy poco eficiente.
* $U_{PyE} = \frac{t_f}{t_{total}} = \frac{1}{1+2a}$
* Recordatorios:
	* $a = \frac{t_p}{t_f} = \frac{d*v_t}{L*v_p}$
	* $d$: distancia entre emisor y receptor.
	* $L$: longitud de la trama de bits.
	* $v_t$: velocidad de transmisión sobre el canal.
	* $v_p$: velocidad de propagación del canal.
* Adecuada para entornos LAN, muy ineficiente para comunicaciones satélite.

### Esquema de ventana deslizante
* Se permite el envío de varias tramas de datos consecutivas son tener que confirmar cada una.
* Las confirmaciones son acumulativas, si se confirma una trama se confirman todas las anterioes.
* Dados $n$ bits, se pueden utilizar $N = 2^n$ **etiquetas** posibles, de $0$ a $N-1$.
* Las tramas enviadas se etiquetan secuencial y ciclicamente.
* Las tramas ACK llevan la etiqueta de la siguiente trama esperada.

* **Ventana de envío** (o emisión):
	* Tamaño de ventana ($N_{envio} \le 2^n$): número de tramas que pueden estar en circualción.
	* Limite superior: puntero que separa las tramas enviadas de las tramas por enviar.
	* Límite inferior: separa las tramas confirmadas de las tramas por confirmar.
* **Ventana de recepcción** o *buffer de entrada*:
	* Tamaño $N_{rec}$
	* Existe un puntero de confimaciones para indicar la última trama de la que se envió confirmación.
	* Límite inferior: entre la última trama recibida correctamente y la que se espera recibir a continuación.
	* Límite superior: la distancia entre este y el puntero de confirmaciones debe ser $\le N_{envio}$

* Cuando hablemos de tamaño de ventana , generalmente hablamos del tamaño de ventana de envío ($N = N_{envio}$).
* Al poder usar bloques de tramas es más eficiente que parada y espera.
* **Eficiencia**, 2 casos:
	1. $N*t_f \ge t_f + 2t_p$ es decir, $N \ge 1+2a \rightarrow$ Se pueden recibir las confirmaciones de trama antes de enviar todas las tramas en la ventana de envío, $U = 1$.
	2. $N*t_f < t_f + 2t_p$ es decir, $N < 1+2a \rightarrow$ Se envíaran todas las tramas de la ventana de emisión antes de recibir una confirmación, $U = \frac{N}{1+2a} < 1$.
* Parada y espera es un caso particular de ventana deslizante con $N = 1$
* Con un $N$ lo suficientemente grande **siempre se puede obtener un $U = 1$** sea cual sea el valor de $a$, pero sería necesaria mucha memoria.

#### Mejoras
* Incorporación de confiraciones o **piggybacking**: Si se está transmitiendo información en ambos entidos, se pueden evitar las tramas ACK explicitas incluyendo las confirmaciones en tramas de datos. Usado en HDLC y LLC.
* Permiso para continuar (**RNR** y **RR**): Los ACK pueden incluir información que indique Reciever Not Ready o Reciever Ready para el control de flujo por parte del receptor.

## Técnicas ARQ *(Automatic Retransmision reQuest)*
* La corrección de errores es muy ineficiente, optamos por la detección de errores:
1. El emisor genera los bits de redundancia y mandamos la trama con ellos.
2. El receptor comprueba si la trama es correcta. Si no lo es solicita el reenvío de la trama.
* Requierer *semi-duplex* o *full-duplex*.
* Si hay **alta probabilidad de error**, más eficiente es la **corrección** de errores.
* Si hay **baja probabilidad de error**, más eficiente es la **detección** de errores.
* Existen técnias híbridas que usan corrección o ARQ dependiendo del nivel de errores.
* En ARQ las tramas se envían y se deben recibir secuencialmente y en orden.
* Existen 2 errores de interés: **trama perdida** y **trama dañada**.
* Tipos de ARQ: *Parada y espera*, *Adelante y atrás N* y *Repetición selectiva*.

### ARQ de parada y espera
* ACK (ACKnowledgment) y NACK (Negative ACKnowledgment).
* **Temporizadores** para gestionar la pérdida de tramas. El emisor vuelve a enviar una trama si no recibe confirmación en $t_{out}$.
* $t_{out} > 2*t_p + t_f$, pero suficientemente pequeño para no degradar la eficiencia.
* Las NACK no son necesarias pero mejoran la eficiencia.
* **Etiquetas** en tramas y confirmaciones para evitar ambiguedad por los temporizadores.
* 1 bit de etiqueta es suficiente ya que se deben confirmar todas las tramas.
* **Control de flujo** limitado ya que el emisor seguirá enviando tramas cada $t_{out}$
* Situaciones de **error y soluciones**:
	* Trama datos erronea: NACK.
	* (N)ACK erronea: se descarta.
	* Pérdida trama datos: temporizador.
	* Pérdida (N)ACK: equivale a NACK.
* **Utilización:** $U_{PyE} = \frac{1-P}{1+2a}$
	* $P$: probabilidad de error en el medio para una trama.
	* $P=1 \Rightarrow U=0$ 

### ARQ de vuelta atrás N
* En caso de error se reenvía la erroena y se continúa desde esa trama, es decir:
* El extremo superior de la ventana de envío vuelve a atrás $N$ posiciones.
* El receptor solo admite la trama que corresponde, $N_{rec} = 1$
* Obliga a la recepción ordenada de tramas.
* Utiliza **temporizadores** para evitar problemas por tramas perdidas.
* $N_{envio} \le 2^n-1$ para evitar ambiguedades en las confirmaciones.
* $N_{envio} > 1$ aumenta la utilización del canal.
* ACKs acumulativos, un ACK$n$ confirma también los anteriores a $n$ por confirmar.
* Situaciones de **error y soluciones**:
	* Trama datos erronea: NACK$n$, se reenvía a partir de $n$.
	* (N)ACK erronea: se descarta. Puede que llegue otra que confirme por acumulación.
	* Pérdida trama datos: NACK al llegar una trama no esperada o temporizador.
	* Pérdida (N)ACK: equivale a NACK, atrás N.
* **Utilización:** depende de la realción entre $N$ y $a$
	* $N \ge 1+2a$
		* $U_{AAN} = \frac{1-P}{1+2aP}$
	* $N < 1+2a$
		* $U_{AAN} = \frac{N(1-P)}{(1+2a)(1-P+NP)}$

### ARQ de repetición selectiva
* $1 < N_{rec} \le 2^{n-1}$ se pueden recibir varias tramas desordenadas dentro de la ventana.
* Se reenvían solo las tramas para las que se reciba un NACK.
* Los ACK positivos son acumulativos.
* Los NACK NO son acumulativos.
* El tamaño óptimo de $N_{rec} = 2^{n-1}$.
* $N_{envio} = 2^{n-1}$, ó $N_{envio} = 2^n-1$ si se usan confirmaciones negativas en cuanto se detecte el error (aproximación optimista).
* La ventana de recepción puede estar dividida.
* Situaciones de **error y soluciones**: igual que *adelante atrás N*, pero solo tiene que reenviar las tramas erroneas.
* **Utilización:** depende de $N$ y $a$
	* $N \ge 1+2a$
		* $U_{RS} = 1-P$
	* $N < 1+2a$
		* $U_{RS} = \frac{N(1-P)}{(1+2a)}$
	* $P$ probabilidad de que una trama sea erronea.

Aunque $U_{RS} > U_{AAN}$, también requiere mayor complejiad y memoria. Dado que $P$ suele ser bajo la inversión en *repetición selectiva* no suele ser rentable por un pequeño aumento de rendimiento frente a *adelante atrás N*.

## LLC *(Logical Link Control)*
* Protocolo de IEEE en uso por la mayoría de las redes LAN actuales.-
* Hereda de HDLC (High level Data Link Control).
* Tipos de servicios:
	1. no orientado a conexión sin confirmación.
	2. orientado a conexión sin confirmación.
	3. no orientado a conexión con confirmación.
* Campos de la trama LLC **[pág. 142 img. 4.23]**:
	1. DSAP *(Destination Service Access Point)*: 8 bits, contiene la dirección lógica de destino.
	2. SSAP *(Source Service Access Point)*: 8 bits, contiene la dirección lógica de origen.
	3. Control: 8 o 16 bits. Control de flujo y gestion de enlace. Indica el tipo: **I**nformación, **S**upervisión o no n**U**meradas
	4. Datos: Hasta 1.492 bytes. Información de capas superiores.

\begin{table}[]
\begin{tabular}{|c|c|c|c|}
\hline
\textbf{LLC:} Campo & \textbf{I}nfor- & \textbf{S}uper- & \textbf{U}nnu- \\
de control          &   mation        & vision          & mbered         \\ \hline
1                   & 0               & 1               & 1              \\ \cline{1-2}
2                   &                 & 0               & 1              \\ \cline{1-1} \cline{3-4} 
3                   & N(S)            & S               & M              \\ \cline{1-1}
4                   &                 &                 &                \\ \hline
5                   & P/F             & P/F             & P/F            \\ \hline
6                   &                 &                 &                \\ \cline{1-1}
7                   & N(R)            & N(R)            & M              \\ \cline{1-1}
8                   &                 &                 &                \\ \hline
\end{tabular}
\end{table}

* Tipos de trama LLC:
	1. Información: tramas de datos. 
		* Dependiendo del tamaño del campo de control:
			* $N(S) = 3 bits \rightarrow N=7$ 
			* $N(S) = 7 bits \rightarrow N=127$ 
		* Forma: $[0|N_{um}(S_{ec})|P/F_{in}|N(R)_{piggybacking}]$
	2. Supervisión: (N)ACKs
		* Tipos: RR, RNR, REJ o SREJ. 
		* Forma: $[10|S_{tipo}|P_{ooling}/F|N(R)_{secuencia}]$
	3. No numeradas: Establecimiento de conexiones y desconexiones. Tipos destacados:
		* SAMB/E: $S_{et}A_{syncronus}B_{alanced}M_{ode}/E_{xtended}$
		* DISC: $DISC_{onnect}$
		* UA: $U_{nnumbered}A_{cknowledgment}$
		* FRMR: $FR_aM_eR_{eject}$
		* UI: $U_{nnumbered}I_{nformation}$
		* Forma: $[11|M|P/F|M]$

# Tema 5: Redes de área local y corporativas
## Redes de area local
### Arquitectura de redes LAN
* Espeficiación IEEE 802: 
	* Capa fisica y capa de enlace, subcapas MAC y de enlace.
	* Independiente de las capas superiores.

#### Capa física
* Inalámbricas: Banda ancha con mucha variación.
* Cableadas:
	* Banda base $\rightarrow$ *X*BASE*Y*.
		* Codificación: 
			* Ethernet: 4B5B/NRZI
			* Eth. Gigabit: 4D-PAM5
	* Banda ancha: $\rightarrow$ *X*BROAD*Y*.
		* Codificación: QPSK o QAM + OFDM.
	* *X*: velocidad en Mbps.
	* *Y*: característica del medio de transmisión.
	* Topologías: bus, arbol, anillo y estrella.

### Redes Ethernet
#### Ethernet DIX:
* IEEE 802.3(a)
* Topología en bus.
* 10 Mbps.
* banda base.
* Codificación Manchester.
* Cable coaxial.
* 2,5km de distancia máxima entre estaciones.
* CSMA/CD 1-persistente.
* 10BASE5 (*Thick Ethernet*) o 10BASE2 (*Thin Ethernet*).
* BEB: *Binary Exponential Backoff*, retroceso exponencial binario.
* 64 bytes de longitud mínima de trama.
* *semi-duplex*.

#### Trama MAC IEEE 802.3
* Norma IEEE802.1D
* Campos:
	* Preámbulo (7 bytes): "10101010" 7 veces para sincronizar relojes. 5,6 $\mu$s a 10 Mbps.
	* Delimitador de comnienzo de trama (1 byte): "10101011" para indicar el comienzo de la trama
	* Dirección de destino (2 o 6 bytes):
		* Si $MSB = 1$ el destino es un grupo (*multicast*).
		* Si todos los bits son 1 es un mensaje de difusión (*broadcast*).
	* Dirección de origen (2 o 6 bytes):
	* Logitud (2 bytes): longitud del campo de datos.
	* Datos (hasta 1500 bytes): el máximo se llama MTU, *Maximum Transfer Unit*.
	* Relleno (0-46 bytes): al usar CSMA/CD, la duración mínima de la trama debe ser $2t_p \rightarrow 51,2 \mu s \rightarrow 64$ bytes, suponiendo 2,5 km y 10Mbps.
	* FCS (4 bytes): Control de errores, CCITT-32 como polinomio generador.

#### Ethernet de alta velocidad y Gigabit
* *Fast Ethernet*:
	* IEEE 802.3u (1995).
	* Compatible con *Ethernet*, misma trama MAC.
	* 100 Mbps mediante: (OR)
		* $\times10$ a la longitud mínima de trama (640 bytes).
		* $\div10$ a la distancia máxima entre estaciones (250 metros)
	* *full-duplex*
	* Par trenzado hasta 100m (200 en f-duplex) 
	* Fibra hasta 400m (2000 en f-duplex).
	* 4B5B o 8B5T
	* Topología de estrella (*switches* recomendados).
* *Gigabit Ethernet*:
	* IEEE 802.3z (1998)
	* 1000 Mbps (1Gbps).
	* Fibra óptica, luego CAT-5 o superior (802.3ab).
	* Full-duplex.
	* Topología en estrella conmutada (concetradores en semi-duplex).
	* *Extensión de portadora*: relleno al final de las tramas cortas para llegar a 4.096 bits (512 bytes).
	* *Ráfaga de tramas*: emisión consecutiva de tramas cortas sin espera de acceso al medio.
	* 1000BASE-$Y$:
		* $Y=$ T: CAT-5 o superior (los 4 pares).
		* $Y=$ CX: par trenzado STP especial.
		* $Y=$ LX: fibra óptica monomodo.
		* $Y=$ SX: fibra óptica multimodo.
	* Codificación 8B/10B.
	* Interconexión entre conmutadores, serividores de alta demanda.
* *10G Ethernet*:
	* IEEE 802.3ae (2003).
	* 10 Gbps.
	* Redes LAN y WAN.
	* Fibra, CAT-6, CAT-7 y cables especiales.

Se está trabajando en estándares de 40 y 100 Gbps.

### Redes WLAN
* Wireless LAN
* Usadas habitualmente en SOHO (Small office Home Office)
	* Interconexión de edificios fácil y cómoda.
	* Estaciones móviles (portátiles, móviles...).
	* Puede ser usadas para soluciones puntuales o temporales.
* Puntos de acceso (AP) o estaciones base (BE) que conectan con estaciones móviles (ME).
* IEEE 802.11

## Redes PAN
### Bluetooth
### USB
### ZigBee

## Redes de acceso
### Tecnologías ADSL
### Redes de cable
### Redes celulares

# Tema 6: Gestión de redes
<!-- Saber por encima, conceptos. -->

* Gestión de redes (OAM): supervisión y mantenimiento de todas las facetas de un sistema de red que puedan afectar a las prestaciones de éste en cuanto a número y características de los servicios y recursos ofertados, la eficiencia, accesos permitidos...
* OAM (Operations, Administration and Management): **Conocimiento y Control** sobre el estado de la red y sus elementos.

## Modelo FCAPS


# Tema 7: Seguridad en redes LAN y corporativas (Capítulo 12)
<!-- Transparencias -->

* IDS detecta cosas que pueden ser intrusiones
* Servicios de seguridad:

\pagebreak
# Datos, definiciones y fórmulas
## Datos:
* $V_{luz} = C = 3 * 10^8 m/s$
* $V_{atmósfera} = 2,8 * 10^8 m/s$
* $V_{cable} = 2 * 10^8 m/s$
* Órbitas GEOestacionarias:
	* 36.000 km de altura.
	* 250 ms de retardo.

## Definiciones:
* **Baudio:** 1 baudio = 1 estado de señalización/segundo.
* **Tiempo de trama** $(t_f)$: lo tarda en emitirse una trama. Desde que se empieza a emitir el primer bit hasta que termina de emitir el último.
* **Tiempo de propagación** $(t_p)$: lo que tarda un bit en propagarse por el medio desde el emisor al receptor. Desde que el emisor termina de enviar un bit hasta que el receptor lo recibe.
* Parámetro adimensional $a = \frac{t_p}{t_f}$ utilizado en muchas fórmulas.
* $R$ num de intervalos de contención o intentos hasta tener éxito en una transmisión.
* $E_{speranza}[R] = \frac{1-P_{rob-error}}{P_{rob-error}}$.

## Fórmulas:
### **Teorema de Nyquist:** 
* $f_s \ge 2*f_m$

### **Capacidad de canal:**
* $V_{trans-máx} = 2*W (pulsos/s)$
* $W$ (Hz) ancho de banda del canal.

### **Velocidad de transmisión:**
* $V_t (bits/segundo) = V_{modulación}*log_2 M$
* $M$ el número de bits que puede transmitirse en un pulso.

### **Signal-to-Noise-Ratio:**
* $SNR = \frac{S}{R}$.
* En decibelios, $SNR_{dB} = 10*log_{10} SNR$.
* Es demostrable que $M \le \sqrt{1+\frac{S}{R}}$

### **Teorema de Shannon:**
* $C = W*log_2(1+\frac{S}{R})$. 
* La **velocidad de transmisión máxima** para un canal de $W$ Hz.

### **Atenuación:** (dB)
* $A = 10 * log_{10}\frac{A_{orig}}{A_{en-dist}}$
* $A_{no-guiados} = 10 * log_{10}(\frac{4\pi d}{\lambda})^2$
	* $d$ distancia.
	* $\lambda$ longitud de onda.

### Aloha:
* $S$: Tasa ofertada (tasa de salida), $0 \le  S \le 1$.
* $G$: Tasa demandada (velocidad e llegada total) (peticiones/ranura).
* **Aloha puro**
	* $S_{ALOHA-PURO}=G*e^{-2G}$
	* $P_{rob-éxito} = \frac{G}{S} = e^{-2G}$
	* $E_{colisiones} = \varepsilon = \frac{g}{s} -1 = e^{-2g} -1$
	* $E[T_{retardo-ALOHA}] = t_{trama} + \varepsilon*(t_{trama}+B)$
		* $B$: tiempo de retroceso medio.
* **Aloha ranurado:**
	* $S_{ALOHA-RANURADO}=G*e^{-G}$
	* $prob_{éxito} = \frac{G}{S} = e^{-G}$
	* $\varepsilon = \frac{G}{S} -1 = e^{-G} -1$

### CSMA/CD:
* Intervalo de contención $\tau = 2t_p$
* $R$ num de $\tau$ hasta tener éxito
* $U = \frac{t_f}{t_f+R*2*t_p}$
<!-- * $P_{éxito-transmitir} =$ -->
<!-- 	* $= \binom{N}{1}*P*(1-P)^{N-1}$ -->
<!-- 	* $= \frac{N!}{1!*(N-1)!}*P*(1-P)^{N-1}$ -->
* $E_{speranza}[R] = \frac{1-P_{éxito}}{P_{éxito}}$
* $U = \frac{t_{trama}}{t_{trama}+R*2*T_{p}} = \frac{1}{1+2a(\frac{1-P_{éxito}}{P_{éxito}})}$

### CSMA/CA:
* $U = \frac{t_f}{t_f+t_p+R*t_{sondeo}}$
* $t_{sondeo} = t_{RTS} + t_{CTS} + 2*t_p$
* $t_{RTS} \approx t_{CTS} \rightarrow t_{CTRL} \ll t_{datos}$
* $U = \frac{1}{1+a(\frac{2-P_{éxito}}{P_{éxito}})}$

### Protocolos libres de colisión:
* **Basados en reserva:**
	* $d$: bits de una trama de datos (bits).
	* $N$: número de estaciones.
	* $U_{baja-carga} = \frac{d}{d+N}$
	* $U_{alta-carga} = \frac{d}{d+1}$
* **Basados en consulta:**
	* $U_{baja-carga} = \frac{t_{trama}}{t_{trama} + t_p}$
	* $U_{alta-carga} = \frac{t_{trama}}{t_{trama} + \frac{t_p}{N}}$

### Control de errores:
* Detectar: $d_H \ge e+1$
* Corregir: $d_H \ge 2e+1$

### Control de flujo:
* Parada y espera:
	* $U_{PyE} = \frac{t_f}{t_{total}} = \frac{1}{1+2a}$
* Ventana deslizante:
	* $N < 1+2a \Rightarrow U=\frac{N}{1+2a}$
	* $N \ge 1+2a \Rightarrow U=1$

### Técnicas ARQ
* **Parada y espera:** $U = \frac{1-P}{1+2a}$
* **Adelante y atrás N:**
	* $N < 1+2a$
		* $U = \frac{N(1-P)}{(1+2a)(1-P+N*P)}$
	* $N \ge 1+2a$ 
		* $U = \frac{N(1-P)}{1+2aP}$
* **Repetición selectiva:**
	* $N < 1+2a$
		* $U = \frac{N(1-P)}{1+2a}$
	* $N \ge 1+2a$ 
		* $U = 1-P$

\pagebreak
# Biliografía
* [1] P. G. Teodoro, J. E. D. Verdejo, and J. M. L. Soler, "Transmisión de datos y redes de computadores, segunda edición", Madrid: PEARSON EDUCACIÓN S.A., 2014.

# Preguntas
* ¿De donde viene la f en $t_f$?
	* R: *frame*
* ¿Cuál es la diferencia entre la velocidad de transmisión y la velocidad de propagación de un canal? ¿Cuando te dan la velocidad del enlace es la velocidad de transmisión del nodo al medio y las velocidades de cada medio nos las tenemos que saber?
	* R: $V_t$ es la velocidad con la que un nodo pone bits en el medio, $V_p$ es la velocidad de transmisión del medio.
* En los campos de la trama MAC, ¿Por qué dice octetos en vez de bytes? ¿No es lo mismo?
	* R: es lo mismo
* En el libro se menciona 8b6b como condificación para 100BASE-T4 (pág. 159) pero en internet solo encuentro 6b8b, ¿es una errata?
	* R: Si es una errata.

* La velocidad de transmisión de un canal está limitada el ancho de banda y el ruido (Teorema de Shannon).
