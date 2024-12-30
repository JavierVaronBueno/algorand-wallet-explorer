# Analizador de Transacciones de Wallet Algorand

Una herramienta avanzada en Python para analizar transacciones de wallets Algorand y monitorear el comportamiento de las "ballenas" (whales) en la red Algorand. Esta herramienta proporciona análisis detallado de transacciones, capacidades de generación de informes y seguimiento de movimientos de grandes carteras.

## Características

- **Análisis de Transacciones de Wallet**
  - Recuperación detallada del historial de transacciones
  - Soporte para transacciones ALGO y ASA
  - Clasificación de transacciones (enviadas/recibidas)
  - Decodificación de notas
  - Generación de informes CSV con detalles completos
  - Visualización interactiva de transacciones y balances

- **Análisis de Movimientos de Whales**
  - Identificación de las principales wallets
  - Análisis de patrones de comportamiento
  - Seguimiento de volúmenes
  - Análisis de tenencia de activos
  - Informes automatizados de actividades

## Requisitos

- Python 3.12+
- Entorno Virtual (venv)
- Paquetes requeridos:
  - py-algorand-sdk
  - python-dateutil
  - pandas
  - typing-extensions
  - requests
  - aiohttp
  - msgpack
  - plotly
  - numpy

## Instalación

1. Clonar el repositorio:
```bash
git clone <url-repositorio>
cd algorand-wallet-analyzer
```

2. Crear y activar el entorno virtual:
```bash
# Crear entorno virtual
python -m venv myenv

# Activar entorno virtual
# En Windows:
myenv\Scripts\activate
# En Unix o MacOS:
source myenv/bin/activate
```

3. Instalar paquetes requeridos:
```bash
pip install py-algorand-sdk python-dateutil pandas typing-extensions requests aiohttp msgpack plotly numpy
```

## Uso

### Análisis Básico de Wallet

```python
from transaction_analyzer import TransactionConfig, WalletAnalyzer

# Configurar parámetros de análisis
config = TransactionConfig(
    start_date="2023-01-01",
    end_date="2024-12-27",
    output_dir="algorand_reports"
)

# Inicializar analizador
wallet_address = "TU_DIRECCION_WALLET"
analyzer = WalletAnalyzer(wallet_address, config)

# Obtener y analizar transacciones
transactions = analyzer.fetch_transactions()
processed_transactions = analyzer.process_transactions(transactions)

# Generar informe
report_path = analyzer.generate_report(processed_transactions, wallet_address)
```

### Procesamiento de Datos y Visualización

```python
# Procesar archivos de transacciones
from data_processor import process_wallet_transactions

stats = process_wallet_transactions(
    input_directory="algorand_reports",
    input_pattern="wallet_transactions_*.csv",
    output_file="wallet_transactions_consolidated.csv"
)

# Generar visualizaciones
from transaction_visualizer import plot_transactions

plot_transactions("wallet_transactions_consolidated.csv")
```

### Análisis de Whales

```python
from whale_analyzer import WhaleAnalyzer

config = TransactionConfig(
    output_dir="whale_reports",
    start_date="2024-01-01",
    end_date="2024-12-27"
)

whale_analyzer = WhaleAnalyzer(config)
report_path = whale_analyzer.generate_whale_report()
```

## Detalles de Características

### Clase TransactionConfig
- Dirección del indexer configurable
- Rangos de fechas personalizables
- Configuración flexible del directorio de salida
- Control de precisión decimal

### Clase WalletAnalyzer
- Obtención de transacciones con paginación
- Procesamiento integral de transacciones
- Soporte para transferencias ASA
- Generación detallada de informes CSV

### Procesamiento de Datos
- Carga y combinación de múltiples archivos CSV
- Limpieza y validación de datos
- Creación de ventanas temporales de 15 minutos
- Agregación de datos por intervalos

### Visualización
- Gráficos interactivos con Plotly
- Visualización de montos por tipo de transacción
- Seguimiento de balance acumulado
- Estadísticas básicas y resúmenes

## Salida

El analizador genera informes CSV detallados que contienen:

- Marcas de tiempo de transacciones
- Tipos de transacción (enviado/recibido)
- IDs de activos
- Montos de transacciones
- Direcciones de remitente/receptor
- IDs de transacción
- Números de bloque
- Notas decodificadas

## Mejores Prácticas

1. Siempre usar un entorno virtual
2. Mantener rangos de fechas razonables
3. Monitorear logs para posibles errores
4. Verificar actualizaciones de dependencias
5. Procesar grandes conjuntos de datos en lotes

## Manejo de Errores

La herramienta incluye manejo integral de errores para:
- Direcciones de wallet inválidas
- Problemas de conectividad
- Timeouts de API
- Formatos de fecha inválidos
- Operaciones del sistema de archivos

## Contribuciones

¡Las contribuciones son bienvenidas! Por favor, siéntete libre de enviar un Pull Request.

## Descargo de Responsabilidad

Esta herramienta es solo para fines de análisis. Siempre verifica los datos de transacciones de forma independiente y úsala bajo tu propio riesgo.