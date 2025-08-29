# 🚨 Sistema de Detección Temprana de Incendios Forestales - Mendoza

[![Status](https://img.shields.io/badge/Status-En%20Desarrollo-orange)](https://img.shields.io/badge/Status-En%20Desarrollo-orange)
[![Comunicación](https://img.shields.io/badge/Comunicación-LoRa%20915MHz-blue)](https://img.shields.io/badge/Comunicación-LoRa%20915MHz-blue)
[![Plataforma](https://img.shields.io/badge/Plataforma-ESP32-important)](https://img.shields.io/badge/Plataforma-ESP32-important)
[![Base de Datos](https://img.shields.io/badge/Base%20de%20Datos-Firebase-yellowgreen)](https://img.shields.io/badge/Base%20de%20Datos-Firebase-yellowgreen)

## 📖 Descripción del Proyecto

Sistema de monitoreo ambiental diseñado para la detección temprana de incendios forestales en zonas de difícil acceso de Mendoza, Argentina. Utiliza una red de nodos sensores inalámbricos que comunican datos en tiempo real mediante tecnología LoRa (Long Range), permitiendo cobertura en grandes extensiones con bajo consumo energético.

Los datos recopilados (temperatura, humedad, gases combustibles y detección de llamas) son centralizados por un gateway y subidos a la nube (Firebase), donde pueden visualizarse en un dashboard web para la toma de decisiones.

## 🎯 Objetivo

Crear una red escalable y autónoma que permita:

- Monitorear en tiempo real condiciones ambientales propicias para incendios.
- Alertar de forma temprana la presencia de fuego o humo.
- Generar datos históricos para análisis y predicción de riesgos.
- Operar en zonas remotas sin dependencia de infraestructura eléctrica o de comunicaciones tradicionales.

## 🏗️ Arquitectura del Sistema

El sistema se compone de tres capas principales:

### 1. Capa de Sensores (Nodos de Campo)

- **ESP32** + Módulo LoRa (915MHz).
- **Conjunto de sensores**:
  - BME280 o DHT22: Temperatura y humedad ambiental.
  - MQ-135 o MQ-2: Detección de gases combustibles (humo, CO, GLP).
  - Sensor de llama IR: Detección de llamas abiertas.
- **Alimentación**: Batería LiPo con panel solar.

### 2. Capa de Comunicación (Red LoRa)

- Protocolo de comunicación LoRaWAN en banda de 915MHz.
- Bajo consumo energético.
- Alcance de varios kilómetros (dependiendo de la topografía).
- Posibilidad de usar nodos repetidores para extender la red.

### 3. Capa de Nube (Base y Visualización)

- **Gateway** con ESP32 + LoRa: Recibe datos de todos los nodos.
- **Conexión WiFi/Ethernet**: Sube datos a Firebase.
- **Firebase Realtime Database**: Almacena y sincroniza datos en tiempo real.
- **Dashboard Web**: Visualización de datos y alertas.

## 📋 Lista de Componentes (Fase Piloto)

### Gateway (Base Central)

| Componente | Cantidad | Observaciones |
|------------|----------|---------------|
| Placa ESP32 DevKit C | 1 | |
| Módulo LoRa RA-01/02 (915MHz) | 1 | Chip SX1278 |
| Antena dipolo 915MHz (3-5dBi) | 1 | Crucial para el alcance |
| Fuente de alimentación 5V 2A | 1 | |

### Nodos Sensores (Mínimo para prueba: 2)

| Componente | Cantidad | Observaciones |
|------------|----------|---------------|
| Placa ESP32 DevKit C | 2 | |
| Módulo LoRa RA-01/02 (915MHz) | 2 | Misma frecuencia que el gateway |
| Antena dipolo 915MHz | 2 | |
| Sensor BME280 o DHT22 | 2 | Temp y Humedad |
| Sensor de llama IR | 2 | |
| Sensor de gas MQ-135 o MQ-2 | 2 | |
| Powerbank o batería LiPo | 2 | Para pruebas iniciales |

### Herramientas y Misceláneos

- Protoboards
- Cables Dupont (macho-hembra, macho-macho)
- Carcasas estancas (IP65+)
- Cargador solar (para despliegue real)

## 🚀 Plan de Implementación (Fases)

### Fase 1: Comunicación LoRa Básica

- Ensamblar 1 Gateway y 1 Nodo (solo módulos LoRa).
- Programar envío de mensaje de prueba ("Hola #1") cada 10 segundos.
- Realizar pruebas de campo para medir alcance real y RSSI en el terreno de Mendoza.
- Ajustar parámetros LoRa (SF, BW) para optimizar la comunicación.

### Fase 2: Integración de Sensores

- Conectar sensores (DHT22, MQ-135, llama) al nodo.
- Programar nodo para enviar paquetes estructurados con datos de sensores.
- Verificar recepción y decodificación correcta en el gateway.

### Fase 3: Conexión a la Nube (Firebase)

- Conectar gateway a WiFi.
- Crear y configurar base de datos en Firebase.
- Programar gateway para subir automáticamente los datos recibidos vía LoRa.

### Fase 4: Prueba de Red y Visualización

- Ensamblar y configurar un segundo nodo sensor.
- Desplegar nodos en ubicaciones distintas dentro del rango.
- Verificar que los datos de todos los nodos aparezcan en Firebase.
- Crear una página web simple (HTML/JS) para visualizar datos en tiempo real.

### Fase 5: Prueba de Campo y Validación

- Realizar pruebas de detección: acercar mechero (llama), generar humo (MQ-135).
- Testear autonomía con powerbanks y paneles solares.
- Validar la generación de alertas en el dashboard.

## 🔧 Configuración y Uso

### Prerrequisitos

- IDE de Arduino con soporte para ESP32.
- **Librerías necesarias**:
  - RadioLib para LoRa.
  - Firebase ESP Client para conexión a Firebase.
  - Adafruit_Sensor y Adafruit_BME280 para sensores.
- Cuenta en Firebase.

### Instalación

1. Clonar este repositorio.
2. Abrir los sketches de Arduino para el nodo y el gateway.
3. Configurar credenciales de WiFi y Firebase en el gateway.
4. Ajustar parámetros LoRa (frecuencia, SF, BW) en ambos sketches.
5. Cargar el código en los dispositivos.

### Despliegue

1. Colocar el gateway en una ubicación elevada con acceso a WiFi y energía.
2. Desplegar los nodos en las zonas a monitorizar, asegurando que estén dentro del rango.
3. Verificar la llegada de datos a Firebase.
4. Acceder al dashboard web para monitoreo.

## 🌍 Consideraciones para Mendoza

- **Topografía**: La presencia de valles y montañas puede requerir el uso de repetidores para extender la red.
- **Clima**: Las cajas deben ser estancas (IP65+) para proteger los circuitos de lluvia y polvo.
- **Energía**: Para despliegue permanente, es crucial el uso de paneles solares y baterías LiPo calculadas según el consumo.

## 📊 Estructura de Datos en Firebase

```json
{
  "nodos": {
    "nodo_001": {
      "temperatura": 28.5,
      "humedad": 45,
      "calidad_aire": 120,
      "llama_detectada": false,
      "timestamp": "2024-03-20T18:30:00Z",
      "ubicacion": "Cerro Arco"
    }
  }
}
```
 ## 👨‍💻 Contribución
¡Las contribuciones son bienvenidas! Para ello:

Haz un Fork del proyecto.

Crea una rama para tu feature (git checkout -b feature/AmazingFeature).

Commit de tus cambios (git commit -m 'Add some AmazingFeature').

Push a la rama (git push origin feature/AmazingFeature).

Abre un Pull Request.

📄 Licencia
Este proyecto está bajo la Licencia MIT. Ver el archivo LICENSE para más detalles.

✒️ Autor
Hugo Alcides Riveros - Alcides.mza@gmail.com

Estudiante de Ingeniería Electrónica (UTN Mendoza).

Apasionado por la tecnología, sistemas embebidos y IoT.

🎯 Próximos Pasos
Diseñar e imprimir carcasas estancas.

Implementar modo deep sleep en nodos para maximizar autonomía.

Desarrollar un dashboard web más completo con mapas y alertas.

Integrar notificaciones vía email/Telegram.

⭐ Si este proyecto te resulta útil, no olvides darle una estrella en GitHub.
