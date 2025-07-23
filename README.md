# Consumo API REST - Java

Proyecto Java para el consumo de APIs REST con autenticación OAuth 2.0 y Bearer Token.

## 📋 Descripción

Este proyecto contiene un conjunto de clases Java que implementan clientes para consumir diferentes APIs REST. Cada clase está diseñada para interactuar con endpoints específicos, manejando autenticación OAuth.

## 🚀 Características

- **Autenticación OAuth 2.0**: Obtención automática de tokens de acceso
- **Manejo de Bearer Tokens**: Autenticación segura en las peticiones
- **Conexiones HTTP nativas**: Utiliza `HttpURLConnection` sin dependencias externas
- **Manejo de errores**: Control de respuestas y logging detallado
- **Configuración flexible**: Parámetros de conexión y timeouts configurables

## 📁 Estructura del Proyecto

```
consumo_api_genexus/
├── src/
│   └── testapigx/
│       ├── TestGetAllEstadosLegajos.java
│       ├── [OtraClaseAPI].java
│       └── [OtraClaseAPI].java
├── README.md
└── .gitignore
```

## 🛠️ Requisitos

- **Java**: 8 o superior
- **Maven/Gradle**: (opcional, si usas gestión de dependencias)
- **Servidor API**: Acceso al servidor REST correspondiente

## ⚙️ Configuración

Antes de ejecutar las clases, asegúrate de configurar:

### Variables de Conexión
```java
private static final String BASE_URL = "http://tu-servidor:puerto/ruta-base";
private static final String TOKEN_ENDPOINT = "/oauth/gam/v2.0/access_token";
private static final String API_ENDPOINT = "/rest/tu-endpoint";
```

### Credenciales OAuth
```java
bodyParams.put("client_id", "tu_client_id");
bodyParams.put("client_secret", "tu_client_secret");
bodyParams.put("api_key", "tu_api_key");
bodyParams.put("authentication_type_name", "tu_tipo_auth");
```

## 🏃‍♂️ Uso

### Ejecución Básica

Cada clase puede ejecutarse independientemente como aplicación Java:

```bash
# Compilar
javac -cp . src/testapigx/TestGetAllEstadosLegajos.java

# Ejecutar
java -cp src testapigx.TestGetAllEstadosLegajos
```

### Flujo de Trabajo Típico

1. **Obtención del Token**: La aplicación solicita un token de acceso OAuth
2. **Autenticación**: Utiliza el token Bearer para autenticar las peticiones
3. **Consumo de API**: Realiza las operaciones necesarias en el endpoint
4. **Procesamiento**: Maneja la respuesta y muestra los resultados

### Ejemplo de Salida

```
=== INICIANDO TEST DE API ESTADOS LEGAJOS ===

1. Obteniendo token de acceso...
✓ Token obtenido exitosamente
Token: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...

2. Obteniendo Estados de los Legajos...
✓ Estados obtenidos exitosamente
Respuesta: [{"id": 1, "estado": "Activo"}, ...]

=== TEST FINALIZADO ===
```

## 🔧 Personalización

### Modificar Timeouts
```java
connection.setConnectTimeout(30000); // 30 segundos
connection.setReadTimeout(30000);    // 30 segundos
```

### Agregar Headers Personalizados
```java
connection.setRequestProperty("Content-Type", "application/json");
connection.setRequestProperty("Accept", "application/json");
connection.setRequestProperty("User-Agent", "Mi-Cliente-Java/1.0");
```

### Configurar Proxy (si es necesario)
```java
Proxy proxy = new Proxy(Proxy.Type.HTTP, new InetSocketAddress("proxy-host", 8080));
HttpURLConnection connection = (HttpURLConnection) url.openConnection(proxy);
```

## 📝 Logging y Debugging

El proyecto incluye logging detallado que muestra:

- Códigos de respuesta HTTP
- Tokens de acceso (parciales por seguridad)
- Respuestas completas de la API
- Mensajes de error detallados

### Ejemplo con Variables de Entorno

```java
private static final String CLIENT_ID = System.getenv("API_CLIENT_ID");
private static final String CLIENT_SECRET = System.getenv("API_CLIENT_SECRET");
private static final String API_KEY = System.getenv("API_KEY");
```

### Problemas Comunes

**Error 401 - Unauthorized**
- Verifica las credenciales OAuth
- Asegúrate de que el token no haya expirado

**Error 404 - Not Found**
- Confirma que la URL base y endpoints sean correctos
- Verifica que el servidor esté funcionando

**TimeoutException**
- Aumenta los valores de timeout
- Verifica la conectividad de red

**SSL/TLS Errors**
- Para desarrollo, puedes deshabilitar verificación SSL (NO recomendado en producción)

**Nota**: Este README es genérico y debe adaptarse según las necesidades específicas de cada implementación de API.
