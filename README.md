# BCV P2P Scraper - Microservicio (Fork from binance-microservice)

Microservicio para extraer la ponderacion del dolar BCV y actualizar automáticamente el precio paralelo en la aplicación de inventario.

## Características

- **Scraping automático** de precios del BCV
- **Compatible con Replit** y entornos serverless (En pruebas aun)
- **Bypass de anti-bot** automático con Puppeteer
- **API RESTful** con múltiples endpoints
- **Logging detallado** de todas las operaciones

## Instalación (En replit, etc... Todavía no se ha implementado)

### En Replit (Recomendado)

1. **Crear un nuevo Repl** e importar este repositorio
2. **Establecer variables de entorno** en Secrets:
   ```
   REPLIT=true
   APP_BASE_URL=https://tu-aplicacion.com
   UPDATE_RATE_ENDPOINT=/index.php?r=site/update-usdt-rate
   ```
3. **Ejecutar**:
   ```bash
   npm install
   npm start
   ```

### En Local (Windows/Mac/Linux)

1. **Clonar el repositorio**:
   ```bash
   git clone <repo-url>
   cd binance-microservice
   ```

2. **Instalar dependencias**:
   ```bash
   npm install
   ```

3. **Configurar variables** en `.env`:
   ```env
   PORT=3000
   APP_BASE_URL=https://tu-aplicacion.com
   UPDATE_RATE_ENDPOINT=/index.php?r=site/update-usdt-rate
   ```

4. **Ejecutar**:
   ```bash
   npm start
   ```

## Endpoints

### `GET /health`
Verif Estado del servicio.

**Respuesta:**
```json
{
  "status": "OK",
  "timestamp": "2025-12-03T12:00:00.000Z",
  "service": "Binance P2P Scraper",
  "version": "1.0.0"
}
```

### `GET /scrape`
Scrapea los precios de Binance P2P.

**Respuesta:**
```json
{
  "success": true,
  "timestamp": "2025-12-03T12:00:00.000Z",
  "data": {
    "bestPrice": 399.25,
    "avgPrice": 401.48,
    "maxPrice": 419.00,
    "totalOffers": 11,
    "prices": [...]
  }
}
```

### `GET /get-averages`
Obtiene solo los promedios y precios resumidos.

**Respuesta:**
```json
{
  "success": true,
  "timestamp": "2025-12-03T12:00:00.000Z",
  "data": {
    "mejorPrecio": 399.25,
    "precioPromedio": 401.48,
    "precioMaximo": 419.00,
    "mejorPrecioObtenido": 399.25
  }
}
```

### `POST /update-rate`
Scrapea y actualiza el precio en la aplicación principal.

**Respuesta:**
```json
{
  "success": true,
  "message": "Precio actualizado correctamente",
  "statusCode": 200,
  "duration": {
    "total": 5340,
    "request": 1250
  },
  "data": {
    "newPrice": 399.25,
    "scrapeInfo": {...}
  }
}
```

### `GET /config`
Obtiene la configuración actual del servicio.

## 🔧 Tecnologías

- **Node.js** + Express
- **puppeteer-core** + **@sparticuz/chromium** (optimizado para serverless)
- **axios** para HTTP requests
- **dotenv** para configuración

## Configuración

### Variables de Entorno

| Variable | Descripción | Default |
|----------|-------------|---------|
| `PORT` | Puerto del servidor | `3000` |
| `APP_BASE_URL` | URL de la aplicación destino | - |
| `UPDATE_RATE_ENDPOINT` | Endpoint para actualizar precio | `/index.php?r=site/update-usdt-rate` |
| `P2P_URL` | URL de Binance P2P | `https://p2p.binance.com/...` |
| `PAGE_TIMEOUT` | Timeout para navegación (ms) | `30000` |
| `REPLIT` | Si está en Replit | `false` |

## Troubleshooting

### En Replit

- Asegúrate de tener `REPLIT=true` en las variables de entorno
- El scraping puede tomar entre 10-30 segundos
- Si falla, revisa los logs en la consola

### En Local

- Asegúrate de tener **Google Chrome** instalado
- En Windows, verifica las rutas del ejecutable
- En Linux, instala: `apt-get install chromium-browser`

### Error "No se pudo encontrar el ejecutable de Chrome"

**Solución para Windows:**
- Instala Google Chrome en la ubicación estándar
- O modifica la ruta en `scraper.js` línea 22-28

**Solución para Linux/Replit:**
- El código usa automáticamente @sparticuz/chromium
- No requiere instalación adicional

## Autor

DiegoPtit
