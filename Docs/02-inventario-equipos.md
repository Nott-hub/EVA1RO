# 02. Inventario y Especificaciones Técnicas de Equipamiento (Maqueta DWDM)

A continuación se detalla la función técnica, el tipo de interfaz y el rol dentro del rack de los 7 componentes principales que conforman la maqueta de laboratorio DWDM:

---

### 1. Analizador Ethernet (EXFO / VeEX - Modelo MTX150x o similar)
*   **Función Técnica:** Generación, análisis y monitorización de tráfico de red en Capa 2 y Capa 3. Permite verificar el rendimiento de los servicios de datos transportados sobre la red óptica mediante la ejecución de pruebas normalizadas como **RFC 2544** (Throughput, Latencia, Pérdida de paquetes, Back-to-Back) y **ITU-T Y.1564** (Ethernet Service Activation Test).
*   **Tipo de Interfaz:** Puertos eléctricos RJ45 (10/100/1000Base-T) y puertos ópticos SFP/SFP+ (1GbE / 10GbE).
*   **Rol en el Rack:** Actúa como equipo generador de tráfico cliente (*Traffic Generator / Tester*) conectado al puerto de acceso del Switch Ethernet o directamente al transpondedor del Chasis DWDM.

---

### 2. Analizador de Espectro Óptico - OSA (EXFO RXT4510 / FTBx-5245 o similar)
*   **Función Técnica:** Instrumento de alta precisión para medir el espectro óptico de la señal multiplexada. Permite visualizar las longitudes de onda individuales, medir la potencia óptica por canal, el ancho de banda espectral y calcular la **Relación Señal a Ruido Óptica (OSNR - *Optical Signal-to-Noise Ratio*)**, parámetro crítico para evaluar la calidad de transmisión.
*   **Tipo de Interfaz:** Interfaz óptica de entrada con conector APC/UPC (adaptable a FC/LC) y pantalla táctil de control con puerto de gestión Ethernet/USB.
*   **Rol en el Rack:** Herramienta de supervisión e instrumentación conectada a los puertos de monitoreo (*tap* óptico de 2% o 5%) del Chasis DWDM para validación espectral en origen y destino.

---

### 3. Switch Ethernet de Gestión (MikroTik / Cisco - Modelo CSS610 o similar)
*   **Función Técnica:** Conmutación y agregación de tráfico Ethernet proveniente de los terminales de usuario o generadores de tráfico, permitiendo etiquetado VLAN (IEEE 802.1Q) y transporte troncal hacia las interfaces de cliente del sistema DWDM.
*   **Tipo de Interfaz:** Puertos Gigabit Ethernet RJ45 y puertos SFP de enlace troncal.
*   **Rol en el Rack:** Nodo de agregación de Capa 2 que interconecta el tráfico emisor/receptor con las tarjetas cliente del chasis multiplexor.

---

### 4. ODF (Optical Distribution Frame)
*   **Función Técnica:** Panel de distribución óptica pasiva que centraliza, organiza y protege las terminaciones de fibra óptica. Facilita el parcheo cruzado (*cross-connect*), la segregación de hilos y la interconexión segura entre los equipos activos (Chasis DWDM, atenuadores e instrumentos).
*   **Tipo de Interfaz:** Adaptadores ópticos acopladores (acopladores LC/UPC, SC/APC o FC/PC según diseño del rack).
*   **Rol en el Rack:** Punto nodal central de interconexión física de todo el cableado óptico del banco de laboratorio.

---

### 5. Chasis DWDM 1 y Chasis DWDM 2 (FiberHome / HTFuture - Modelo HT6000 o similar)
*   **Función Técnica:** Sistema modular de transporte óptico que integra funciones de transpondedor/muxponder, multiplexación/demultiplexación por longitud de onda (MUX/DEMUX basadas en tecnología AWG o TFF), y amplificación óptica. Realiza la conversión electro-óptica de las señales de cliente a longitudes de onda específicas de la grilla ITU-T.
*   **Tipo de Interfaz:** 
    *   *Lados Cliente:* Puertos SFP/SFP+ (1G/10G).
    *   *Lados Línea:* Puertos ópticos DWDM (interfaces coloridas alineadas a la grilla ITU-T).
    *   *Gestión:* Puertos RJ45 (SNMP, CLI, Web GUI).
*   **Rol en el Rack:** Núcleo activo de la red de transporte DWDM. El Chasis 1 opera en el extremo transmisor (Tx) multiplexando los canales, y el Chasis 2 opera en el extremo receptor (Rx) demultiplexando y recuperando los servicios.

---

### 6. Carretes de Fibra Óptica (Bobinas AB - 25 KM y BA - 25 KM)
*   **Función Técnica:** Bobinas de fibra monomodo estándar (ITU-T G.652) con una longitud calibrada de 25 km cada una. Simulan las pérdidas por atenuación lineal (~0.22 dB/km a 1550 nm), la dispersión cromática y los efectos de propagación propios de un enlace real de telecomunicaciones de media distancia.
*   **Tipo de Interfaz:** Conectores ópticos en ambos extremos (ej. LC/UPC o SC/UPC).
*   **Rol en el Rack:** Elemento pasivo de canal de transmisión que interconecta el Chasis 1 y el Chasis 2, generando la distancia física simulada de 50 km total (25 km ida y 25 km retorno o enlace troncal).

---

### 7. Atenuador Óptico Variable - OVA (JW3303 o similar)
*   **Función Técnica:** Dispositivo optomecánico o digital que introduce una pérdida de inserción controlada y ajustable en la ruta óptica. Permite simular degradaciones severas de potencia, pérdida de margen de enlace (*link budget*) y evaluar la sensibilidad de recepción de los transpondedores.
*   **Tipo de Interfaz:** Entradas y salidas ópticas con adaptadores normalizados (SC/UPC o FC/UPC).
*   **Rol en el Rack:** Inserción en serie dentro del enlace de fibra para pruebas de estrés de potencia óptica y validación de umbrales operacionales del sistema DWDM.
