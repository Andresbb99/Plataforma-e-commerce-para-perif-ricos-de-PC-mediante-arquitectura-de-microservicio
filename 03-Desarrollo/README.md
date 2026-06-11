# 💻 Fase 03: Desarrollo

## Descripción

Esta carpeta contiene todo el código fuente de los microservicios, incluyendo:
- Implementación de servicios
- Modelos y controladores
- Rutas y middleware
- Utilidades y helpers
- Configuración de desarrollo

## 📁 Estructura de Carpetas

```
03-Desarrollo/
├── auth-service/              # Servicio de Autenticación
├── product-service/           # Servicio de Catálogo
├── cart-service/              # Servicio de Carrito
├── order-service/             # Servicio de Órdenes
├── payment-service/           # Servicio de Pagos
├── notification-service/      # Servicio de Notificaciones
├── inventory-service/         # Servicio de Inventario
├── api-gateway/               # API Gateway
├── shared/                    # Código compartido
└── docker-compose.yml         # Composición de servicios
```

## 🔧 Stack Tecnológico

### Backend
- **Runtime**: Node.js 16+ / Java 11+ / Python 3.9+
- **Framework**: Express.js / Spring Boot / FastAPI
- **ORM**: Sequelize / Hibernate / SQLAlchemy
- **Validación**: Joi / Bean Validation / Pydantic

### Base de Datos
- **Principal**: PostgreSQL 13+
- **Cache**: Redis 6+
- **Búsqueda**: Elasticsearch 7+ (opcional)

### Messaging
- **Queue**: RabbitMQ 3.9+ / Apache Kafka 2.8+
- **Client**: AMQP / Kafka Client

### Testing
- **Unit Tests**: Jest / JUnit / Pytest
- **Integration Tests**: Postman / REST Assured / Requests
- **E2E Tests**: Cypress / Selenium

## 📋 Guías de Desarrollo

### Por Servicio

- [auth-service/README.md](./auth-service/README.md) - Servicio de Autenticación
- [product-service/README.md](./product-service/README.md) - Servicio de Productos
- [cart-service/README.md](./cart-service/README.md) - Servicio de Carrito
- [order-service/README.md](./order-service/README.md) - Servicio de Órdenes
- [payment-service/README.md](./payment-service/README.md) - Servicio de Pagos
- [notification-service/README.md](./notification-service/README.md) - Servicio de Notificaciones
- [inventory-service/README.md](./inventory-service/README.md) - Servicio de Inventario
- [api-gateway/README.md](./api-gateway/README.md) - API Gateway

### Generales

- [Guia_Desarrollo.md](./Guia_Desarrollo.md) - Guía general de desarrollo
- [Estandares_Codigo.md](./Estandares_Codigo.md) - Estándares de código
- [Convenciones_Nombres.md](./Convenciones_Nombres.md) - Convenciones de nombres
- [Testing_Strategy.md](./Testing_Strategy.md) - Estrategia de testing

## 🚀 Instalación y Configuración

### Prerrequisitos

```bash
# Node.js
node --version  # >= 16.0.0
npm --version   # >= 7.0.0

# Docker
docker --version
docker-compose --version

# Git
git --version
```

### Instalación Local

```bash
# 1. Clonar repositorio
git clone <repo-url>
cd 03-Desarrollo

# 2. Instalar dependencias
npm install

# 3. Configurar variables de entorno
cp .env.example .env

# 4. Iniciar servicios
docker-compose up -d

# 5. Ejecutar migraciones (si aplica)
npm run migrate

# 6. Ejecutar seeds (si aplica)
npm run seed
```

### Configuración por Servicio

Cada servicio tiene su propio `README.md` con instrucciones específicas de instalación.

## 📝 Variables de Entorno

```env
# General
NODE_ENV=development
PORT=3000

# Database
DB_HOST=postgres
DB_PORT=5432
DB_USER=postgres
DB_PASSWORD=postgres
DB_NAME=ecommerce

# Redis
REDIS_HOST=redis
REDIS_PORT=6379

# JWT
JWT_SECRET=your-secret-key
JWT_EXPIRES_IN=24h

# RabbitMQ
RABBITMQ_URL=amqp://user:password@rabbitmq:5672

# Email
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your-email@gmail.com
SMTP_PASSWORD=your-password
```

## 🔄 Flujo de Desarrollo

```
Feature Branch
    ↓
Desarrollo Local
    ↓
Testing Local (Unit + Integration)
    ↓
Commit y Push
    ↓
Pull Request
    ↓
Code Review
    ↓
CI/CD Pipeline
    ↓
Merge a Main
```

## 🧪 Testing

### Ejecutar Tests

```bash
# Todos los tests
npm run test

# Solo unit tests
npm run test:unit

# Solo integration tests
npm run test:integration

# Con coverage
npm run test:coverage

# Watch mode
npm run test:watch
```

### Cobertura Mínima Requerida

- **Cobertura de Líneas**: 80%
- **Cobertura de Ramas**: 75%
- **Cobertura de Funciones**: 80%
- **Cobertura de Statements**: 80%

## 📊 Estructura de un Servicio

```
service-name/
├── src/
│   ├── controllers/        # Controladores
│   ├── models/            # Modelos de datos
│   ├── routes/            # Rutas
│   ├── middleware/        # Middleware personalizado
│   ├── services/          # Lógica de negocio
│   ├── utils/             # Utilidades
│   ├── validators/        # Validadores
│   ├── config/            # Configuración
│   └── app.js             # Entrada principal
├── test/                  # Tests
├── .env.example          # Variables de ejemplo
├── package.json          # Dependencias
├── Dockerfile            # Dockerfile
└── README.md             # Documentación
```

## 🔗 Comunicación entre Servicios

### Síncrona (HTTP/REST)

```javascript
// Ejemplo: Auth Service valida token
const validateToken = async (token) => {
  const response = await axios.get(
    `http://auth-service:3001/validate`,
    { headers: { Authorization: `Bearer ${token}` } }
  );
  return response.data;
};
```

### Asíncrona (Message Queue)

```javascript
// Ejemplo: Publicar evento de orden creada
await amqp.publish('orders.created', {
  orderId: order.id,
  userId: order.userId,
  total: order.total
});
```

## ✅ Checklist de Entregables

- [ ] Todos los microservicios implementados
- [ ] APIs documentadas y funcionales
- [ ] Tests unitarios completados
- [ ] Tests de integración completados
- [ ] Coverage >= 80%
- [ ] Documentación de código
- [ ] Dockerfiles funcionales
- [ ] Variables de entorno configuradas
- [ ] Migraciones de BD ejecutadas
- [ ] Código revisado y aprobado

## 🐛 Debugging

### Logs

```bash
# Ver logs de un servicio específico
docker-compose logs -f auth-service

# Ver logs de todos los servicios
docker-compose logs -f
```

### Debug Mode

```bash
# Ejecutar con debugger habilitado
DEBUG=* npm start
```

## 🔗 Enlaces Relacionados

- [← Ir a Diseño](../02-Diseño/)
- [Ir a Pruebas →](../4-Pruebas/)
- [Guía de Contribución](../CONTRIBUTING.md)
- [Estándares de Código](./Estandares_Codigo.md)
- [README Principal](../README.md)

---

**Estado**: 🔄 En Progreso | **Última Actualización**: Junio 2026
