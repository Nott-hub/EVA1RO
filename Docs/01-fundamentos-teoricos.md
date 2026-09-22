# 01. Fundamentos Teóricos de la Tecnología DWDM

## 1. Definición de DWDM y Diferencias con CWDM
La **Multiplexación por División de Longitud de Onda Densa (DWDM)** (*Dense Wavelength Division Multiplexing*) es una tecnología de transmisión óptica que permite combinar múltiples señales portadoras ópticas (canales) sobre una única fibra óptica mediante el uso de diferentes longitudes de onda de luz láser. 

*   **Capacidad y Espaciamiento:** DWDM utiliza un espaciamiento espectral muy estrecho (típicamente 100 GHz, 50 GHz o menor según la grilla flexible), lo que permite alojar decenas o cientos de canales (lambdas) dentro de la Banda C (convencional) y Banda L (larga), logrando capacidades de transporte del orden de Terabits por segundo (Tbps).
*   **Diferencias con CWDM (*Coarse Wavelength Division Multiplexing*):**
    *   **Espaciamiento:** CWDM utiliza un espaciamiento de canales mucho más amplio (20 nm entre canales), limitando su capacidad total típica a 8 o 18 canales en el rango de 1270 nm a 1610 nm. DWDM opera con separaciones de fracciones de nanómetro (ej. 0.8 nm o 0.4 nm).
    *   **Alcance y Amplificación:** CWDM está diseñado para distancias metropolitanas cortas (hasta ~70-80 km) sin amplificación óptica debido a las mayores pérdidas en las zonas de dispersión y la imposibilidad de usar amplificadores ópticos de fibra dopada con erbio (EDFA) económicos. DWDM requiere amplificación EDFA y compensación de dispersión cromática, permitiendo enlaces de larga distancia (cientos o miles de kilómetros).
    *   **Costo de Transceptores:** Los láseres DWDM requieren control térmico estricto (láseres DFB refrigerados con TEC) para mantener la longitud de onda exactamente alineada con la grilla ITU-T, encareciendo el componente frente a CWDM.

---

## 2. Espectro y Longitudes de Onda (Grilla ITU-T G.694.1)
La normalización del espectro óptico para sistemas DWDM está definida por la recomendación **ITU-T G.694.1**, la cual establece la grilla de frecuencias de referencia anclada a la frecuencia central de **193.10 THz** (equivalente a aproximadamente 1552.52 nm en el vacío).

*   **Banda C (Conventional Band):** Se extiende desde 1530 nm hasta 1565 nm (aprox. 191.6 THz a 196.1 THz). Es la zona donde las fibras de sílice estándar presentan la menor atenuación intrínseca (~0.2 dB/km) y donde operan eficientemente los amplificadores EDFA.
*   **Espaciamiento de Canales:**
    *   *Grilla de 100 GHz:* Canales separados por 0.8 nm (100 GHz), albergando típicamente 40 o más canales en la Banda C.
    *   *Grilla de 50 GHz:* Canales separados por 0.4 nm (0.8 nm), duplicando la densidad a 80 o más canales.
    *   *Flexible Grid (Grilla Flexible):* Introducida para sistemas de transporte coherente avanzados (supercanales y modulación de orden superior), permitiendo asignar ancho de banda variable en múltiplos de 12.5 GHz.

---

## 3. Modulación Óptica y Conversión Electro-Óptica
La conversión de señales eléctricas provenientes de equipos de datos (Ethernet, SDH) a señales ópticas se realiza mediante transpondedores y muxponders. Los formatos de modulación determinan la eficiencia espectral (bits/s/Hz):

*   **NRZ (Non-Return-to-Zero):** Formato binario clásico de encendido/apagado (OOK). Simple y robusto para velocidades de 10 Gbps por canal, pero limitado en tolerancia a efectos no lineales en altas velocidades.
*   **PAM4 (Pulse Amplitude Modulation 4-level):** Modulación de amplitud de pulso con 4 niveles, duplicando la tasa de bits por símbolo respecto a NRZ, ampliamente utilizada en enlaces intra-datacenter y redes de acceso de alta velocidad.
*   **QPSK (Quadrature Phase Shift Keying) y QAM (Quadrature Amplitude Modulation):** Formatos de modulación coherente (ej. PM-QPSK, 16-QAM). Modulan tanto la fase como la amplitud de la onda portadora en polarizaciones duales (X e Y). Permiten velocidades de 100G, 200G, 400G y superiores por longitud de onda, ofreciendo alta tolerancia a la dispersión cromática y modo de polarización (PMD) mediante procesamiento digital de señales (DSP) en el receptor.

---

## 4. Estándares y Normativas de Referencia
*   **ITU-T G.694.1:** Define las grillas de frecuencias espectrales para aplicaciones DWDM en sistemas WDM.
*   **ITU-T G.709 (OTN - Optical Transport Network):** Define la estructura de trama, jerarquía de multiplexación, FEC (Forward Error Correction) y mecanismos de OAM (Operation, Administration, and Maintenance) para redes de transporte óptico, garantizando robustez y visibilidad de errores en el nivel físico y de transporte.
*   **ITU-T G.652 (Fibra Monomodo Estándar - SSMF):** Fibra óptica de dispersión optimizada en la ventana de 1310 nm, con una longitud de onda de dispersión cromática cero ($D_0$) alrededor de 1310 nm y un coeficiente de dispersión de ~$17 \text{ ps/(nm}\cdot\text{km)}$ en la Banda C (1550 nm).
*   **ITU-T G.655 (Fibra No-Zero Dispersion-Shifted Fiber - NZ-DSF):** Fibra diseñada para sistemas DWDM de larga distancia, donde la longitud de onda de dispersión cero se desplaza fuera de la Banda C (ej. hacia 1490 nm o 1600 nm), reduciendo efectos no lineales como la mezcla de cuatro ondas (FWM) en los canales de 1550 nm.
