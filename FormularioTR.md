---
title: "Formulario"
subtitle: "Tecnologías de red"
author: 
- "Enrique Paubert Reca"
geometry: margin=2cm
mainfont: LiberationSerif-Regular.ttf
mathfont: latinmodern-math.otf
monofont: monospace
toc: false
indent: false
lang: es-ES
documetclass: article
classoption: 
- 10pt
- a4paper
- notitlepage
- twocolumn
---
# Datos:
* $V_{luz} = C = 3 * 10^8 m/s$
* $V_{atmósfera} = 2,8 * 10^8 m/s$
* $V_{cable} = 2 * 10^8 m/s$
* Órbitas GEOestacionarias:
	* 36.000 km de altura.
	* 250 ms de retardo.

# Definiciones:
* **Baudio:** 1 baudio = 1 estado de señalización/segundo.
* **Tiempo de trama** $(t_f)$: lo tarda en emitirse una trama. Desde que se empieza a emitir el primer bit hasta que termina de emitir el último.
* **Tiempo de propagación** $(t_p)$: lo que tarda un bit en propagarse por el medio desde el emisor al receptor. Desde que el emisor termina de enviar un bit hasta que el receptor lo recibe.
* Parámetro adimensional $a = \frac{t_p}{t_f}$ utilizado en muchas fórmulas.
* $R$ num de intervalos de contención o intentos hasta tener éxito en una transmisión.
* $E_{speranza}[R] = \frac{1-P_{rob-error}}{P_{rob-error}}$.

# Fórmulas:
## **Teorema de Nyquist:** 
* $f_s \ge 2*f_m$

## **Capacidad de canal:**
* $V_{trans-máx} = 2*W (pulsos/s)$
* $W$ (Hz) ancho de banda del canal.

## **Velocidad de transmisión:**
* $V_t (bits/segundo) = V_{modulación}*log_2 M$
* $M$ el número de bits que puede transmitirse en un pulso.

## **Signal-to-Noise-Ratio:**
* $SNR = \frac{S}{R}$.
* En decibelios, $SNR_{dB} = 10*log_{10} SNR$.
* Es demostrable que $M \le \sqrt{1+\frac{S}{R}}$

## **Teorema de Shannon:**
* $C = W*log_2(1+\frac{S}{R})$. 
* La **velocidad de transmisión máxima** para un canal de $W$ Hz.

## **Atenuación:** (dB)
* $A = 10 * log_{10}\frac{A_{orig}}{A_{en-dist}}$
* $A_{no-guiados} = 10 * log_{10}(\frac{4\pi d}{\lambda})^2$
	* $d$ distancia.
	* $\lambda$ longitud de onda.

## Aloha:
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

## CSMA/CD:
* Intervalo de contención $\tau = 2t_p$
* $R$ num de $\tau$ hasta tener éxito
* $U = \frac{t_f}{t_f+R*2*t_p}$
<!-- * $P_{éxito-transmitir} =$ -->
<!-- 	* $= \binom{N}{1}*P*(1-P)^{N-1}$ -->
<!-- 	* $= \frac{N!}{1!*(N-1)!}*P*(1-P)^{N-1}$ -->
* $E_{speranza}[R] = \frac{1-P_{éxito}}{P_{éxito}}$
* $U = \frac{t_{trama}}{t_{trama}+R*2*T_{p}} = \frac{1}{1+2a(\frac{1-P_{éxito}}{P_{éxito}})}$

## CSMA/CA:
* $U = \frac{t_f}{t_f+t_p+R*t_{sondeo}}$
* $t_{sondeo} = t_{RTS} + t_{CTS} + 2*t_p$
* $t_{RTS} \approx t_{CTS} \rightarrow t_{CTRL} \ll t_{datos}$
* $U = \frac{1}{1+a(\frac{2-P_{éxito}}{P_{éxito}})}$

## Protocolos libres de colisión:
* **Basados en reserva:**
	* $d$: bits de una trama de datos (bits).
	* $N$: número de estaciones.
	* $U_{baja-carga} = \frac{d}{d+N}$
	* $U_{alta-carga} = \frac{d}{d+1}$
* **Basados en consulta:**
	* $U_{baja-carga} = \frac{t_{trama}}{t_{trama} + t_p}$
	* $U_{alta-carga} = \frac{t_{trama}}{t_{trama} + \frac{t_p}{N}}$

## Control de errores:
* Detectar: $d_H \ge e+1$
* Corregir: $d_H \ge 2e+1$

## Control de flujo:
* Parada y espera:
	* $U_{PyE} = \frac{t_f}{t_{total}} = \frac{1}{1+2a}$
* Ventana deslizante:
	* $N < 1+2a \Rightarrow U=\frac{N}{1+2a}$
	* $N \ge 1+2a \Rightarrow U=1$

## Técnicas ARQ
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
