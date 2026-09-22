# 03. Manual de Configuración, Seguridad y Procedimientos de Medición

## 1. Medidas de Seguridad Óptica
La manipulación de sistemas láser en telecomunicaciones requiere protocolos estrictos de seguridad para prevenir lesiones oculares permanentes (la radiación infrarroja utilizada en DWDM, típicamente en torno a 1550 nm, es invisible al ojo humano pero enfocada por la córnea directamente sobre la retina).

*   **Clasificación Láser:** Los equipos DWDM y transceptores empleados corresponden habitualmente a **Clase 1M** o **Clase 3R**. Se prohíbe mirar directamente al núcleo de los conectores ópticos o latiguillos (*patch cords*) energizados.
*   **Uso de Instrumentos de Inspección:** Utilice siempre un microscopio de inspección óptica (*fiber scope*, ej. 200x/400x) antes de conectar cualquier fibra para verificar la ausencia de polvo o suciedad.
*   **Limpieza de Conectores:** 
    *   Utilizar limpiadores de tipo one-click o toallitas de celulosa libre de pelusa impregnadas con alcohol isopropílico de alta pureza (>99%).
    *   Mantener tapados los conectores y puertos no utilizados con capuchones protectores anti-polvo.
*   **Distinción APC vs. UPC:** Nunca interconecte conectores de tipo **APC** (*Angled Physical Contact*, biselados a 8°, color verde) con conectores **UPC** (*Ultra Physical Contact*, planos, color azul/gris), ya que se provocan daños mecánicos severos en las ferulas y reflexiones de retorno elevadas (ORL).

---

## 2. Configuración del Chasis HT6000 (Aprovisionamiento)
Pasos operativos para la puesta en marcha de los servicios en el chasis multiplexor:

1.  **Acceso al Sistema de Gestión:**
    *   Conectar el puerto de gestión del chasis HT6000 a la estación de trabajo mediante cable Ethernet.
    *   Configurar la dirección IP en la interfaz de red del PC (ej. `192.168.1.100 / 24`) e ingresar a la interfaz Web o CLI mediante PuTTY/SSH con credenciales de operador.
2.  **Inventario y Verificación de Tarjetas:**
    *   Verificar en el panel de control de slots que el chasis reconozca correctamente las tarjetas de transpondedores (Client/Line cards) y los MUX/DEMUX ópticos.
3.  **Aprovisionamiento de Servicios y Mapeo de Puertos:**
    *   Navegar al menú de configuración de servicios (*Service Provisioning*).
    *   Asignar el puerto de cliente (ej. Client Port 1 configurado a 1GbE) hacia la tarjeta transpondedora correspondiente.
    *   Configurar la longitud de onda de transmisión en el puerto de línea (*Line Port*), seleccionando el canal exacto según la grilla ITU-T G.694.1 (ej. Canal 34 - 193.4 THz / 1550.92 nm).
    *   Guardar la configuración (*Commit / Save Configuration*) para asegurar la persistencia ante reinicios.

---

## 3. Procedimiento de Prueba y Medición
Flujo de validación técnica en el banco de laboratorio:

1.  **Verificación Inicial en Vacío:**
    *   Conectar el Analizador Óptico de Espectro (OSA RXT4510) al puerto de monitoreo (*Monitor Port*) del Chasis DWDM 1 para comprobar la potencia de salida de los láseres y la alineación de la grilla espectral.
2.  **Inserción del Enlace y Atenuador (OVA):**
    *   Interconectar el Chasis 1 con los Carretes de Fibra Óptica (25 km + 25 km = 50 km) a través del Atenuador Óptico Variable (OVA JW3303) para simular pérdidas configurables.
    *   Ajustar el OVA para introducir incrementos de atenuación (ej. empezar con 0 dB, luego 10 dB, 15 dB) y observar el impacto en la recepción.
3.  **Medición Espectral y OSNR (con OSA RXT4510):**
    *   Capturar el trazo espectral en el extremo receptor (Chasis 2).
    *   Medir la potencia óptica por canal y calcular el valor de OSNR. Registrar el umbral donde el sistema comienza a degradar.
4.  **Pruebas de Tráfico Ethernet (con MTX150x):**
    *   Conectar el analizador MTX150x a los puertos de cliente en el extremo remoto.
    *   Ejecutar la prueba **RFC 2544** para validar:
        *   *Throughput* (Rendimiento máximo sin pérdida de tramas).
        *   *Latencia* de propagación a través de los 50 km de fibra.
        *   *Packet Loss* y *Burstability*.
    *   Ejecutar la prueba de Tasa de Error de Bit (**BER Test**) durante un periodo prolongado para certificar la estabilidad del enlace DWDM bajo condiciones nominales y de atenuación inducida.
