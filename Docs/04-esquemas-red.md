# 04. Esquemas de Red, Mapeo de Puertos y Topología (Maqueta MIDEX DWDM)

## 1. Diagrama de Conexiones Físicas
La topología física de la maqueta de laboratorio DWDM de INACAP La Serena integra equipos de instrumentación VeEX, conmutación MikroTik y chasis de transporte óptico modular HT6000.

*(Nota: Los archivos editables correspondientes a los diagramas vectoriales se encuentran respaldados en la carpeta `diagramas/esquemas-drawio/` y las exportaciones gráficas en la carpeta `imagenes/`)*.

---

## 2. Tabla de Direccionamiento IP (Gestión de Red)
Para la supervisión y control de los dispositivos activos en la red de laboratorio, se establece el siguiente esquema de direccionamiento IP dentro de la subred `192.168.1.0/24`:

| # | Dispositivo / Instrumento | Dirección IP | Máscara / Prefijo |
| :-: | :--- | :---: | :---: |
| **1** | Chasis DWDM 1 (HT6000) | `192.168.1.101` | `/24` |
| **2** | Chasis DWDM 2 (HT6000) | `192.168.1.102` | `/24` |
| **3** | Analizador Ethernet (MTX150x) | `192.168.1.201` | `/24` |
| **4** | Analizador de Espectro Óptico - OSA (RXT4510) | `192.168.1.202` | `/24` |
| **5** | Estación de Control / PC | `192.168.1.10` | `/24` |

---

## 3. Etiquetado y Matriz de Conexión en ODF (Optical Distribution Frame)
El panel de distribución óptica centraliza las conexiones físicas del rack de acuerdo con la siguiente estandarización de puertos:

| Puerto ODF | Conexión Asociada | Descripción de Conexión Física |
| :---: | :--- | :--- |
| **1-A** | MON DWDM 1 | Puerto de Monitoreo Óptico (2%) del Chasis DWDM 1 hacia OSA |
| **1-B** | MON DWDM 2 | Puerto de Monitoreo Óptico (2%) del Chasis DWDM 2 |
| **3** | CLI 1 DWDM 1 | Interfaz de Cliente 1 en Chasis DWDM 1 |
| **4** | CLI 1 DWDM 2 | Interfaz de Cliente 1 en Chasis DWDM 2 |
| **6** | FIBRA 1 | Extremo de entrada/salida del Carrete de Fibra Óptica 1 (25 km) |
| **7** | FIBRA 2 | Extremo de entrada/salida del Carrete de Fibra Óptica 2 (25 km) |
| **9** | LIN DWDM 1 | Conector de Línea / Troncal Óptico del Chasis DWDM 1 |
| **10** | LIN DWDM 2 | Conector de Línea / Troncal Óptico del Chasis DWDM 2 |

---

## 4. Matriz de Interconexión del Enlace (Patch Cords)

| Enlace # | Equipo Origen (TX) | Puerto Origen | Equipo Destino (RX) | Puerto Destino | Tipo de Medio / Conector |
| :---: | :--- | :---: | :--- | :---: | :--- |
| **1** | Analizador Ethernet (MTX150x) | Port 1 | Switch Ethernet (CSS610) | Port 1 | UTP Cat6 / RJ45 |
| **2** | Switch Ethernet (CSS610) | Port SFP 1 | Chasis DWDM 1 | Client Port 1 (OTU 1) | Fibra Monomodo / LC-LC UPC |
| **3** | Chasis DWDM 1 (Línea) | Line Port | ODF (Panel Local) | Port 9 (LIN DWDM 1) | Latiguillo Óptico / LC-LC UPC |
| **4** | ODF (Panel Local) | Port 9 OUT | Carrete de Fibra Óptica 1 | Start (AB 25 km) | Latiguillo Óptico / SC-LC UPC |
| **5** | Carrete de Fibra Óptica 1 | End (25 km) | Carrete de Fibra Óptica 2 | Start (BA 25 km) | Latiguillo Óptico / LC-LC UPC |
| **6** | Carrete de Fibra Óptica 2 | End (25 km) | ODF (Panel Remoto) | Port 10 (LIN DWDM 2) | Latiguillo Óptico / LC-LC UPC |
| **7** | ODF (Panel Remoto) | Port 10 IN | Chasis DWDM 2 (Línea) | Line Port | Latiguillo Óptico / LC-LC UPC |
| **8** | Chasis DWDM 2 | Client Port 1 (OTU 1) | Analizador Ethernet (MTX150x) | Port 2 | Fibra SFP / RJ45 |
| **9** | Chasis DWDM 1 (Monitor) | Mon Port (2%) | ODF (Panel Local) | Port 1-A (MON DWDM 1) | Latiguillo Óptico / FC-APC |
| **10** | ODF (Panel Local) | Port 1-A OUT | Analizador de Espectro (OSA)| Optical Input | Latiguillo Óptico / FC-APC |

---

## 5. Flujo de la Señal (Descripción Paso a Paso)

1.  **Generación de Tráfico:** El Analizador VeEX MTX150x genera flujos de tráfico Ethernet de prueba (Capa 2/3) y los inyecta hacia el Switch MikroTik CSS610 y las tarjetas de cliente (OTU) del Chasis DWDM 1.
2.  **Multiplexación Óptica:** El Chasis DWDM 1 realiza la conversión electro-óptica, adaptando la señal del cliente a una longitud de onda específica de la grilla ITU-T (ej. Canal C21 o superior) mediante sus módulos ODM08.
3.  **Transmisión y Propagación:** La señal óptica abandona el puerto de línea del Chasis 1, cruza el ODF y se propaga a través de los dos carretes de fibra óptica en serie (**50 km totales**, simulando el canal de transmisión de ida y vuelta).
4.  **Recepción y Demultiplexación:** La señal llega al Chasis DWDM 2, donde el módulo DEMUX separa la longitud de onda correspondiente para entregarla al transpondedor receptor y restaurar el flujo eléctrico.
5.  **Análisis y Validación:** El Analizador MTX150x (en su puerto de recepción P2) evalúa métricas críticas como tasa de error de bits (BER), pérdida de tramas y latencia, mientras que el Analizador de Espectro Óptico (OSA RXT4510) supervisa de manera concurrente la potencia por canal y la relación OSNR desde el puerto de monitoreo del ODF.
