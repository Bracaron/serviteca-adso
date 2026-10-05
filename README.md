# Serviteca ADSO - Sistema de Gestión Automotriz

## 📋 Descripción

Sistema web para la gestión de servitecas automotrices que permite administrar clientes, vehículos y servicios prestados (Cambio de Aceite, Sincronización, Alineación, Lavado).

## 🚀 Características Principales

- **Gestión de Clientes**: CRUD completo con validaciones
- **Gestión de Vehículos**: Registro y consulta por placa
- **Gestión de Servicios**: Registro de servicios con relación cliente-vehículo
- **Autenticación**: Sistema seguro de login/logout con JWT
- **Interfaz Responsive**: Funciona en desktop y dispositivos móviles
- **Reportes**: Consulta de historial de servicios por vehículo

## 🏗️ Arquitectura

### Frontend
- **React + TypeScript + Vite**
- **Bootstrap 5** para componentes responsive
- **React Router** para navegación SPA
- **React Hook Form + Yup** para validaciones

### Backend
- **Node.js + Express.js + TypeScript**
- **PostgreSQL** base de datos relacional
- **JWT** para autenticación
- **express-validator** para validación de inputs

## 📁 Estructura del Proyecto

```
serviteca-adso/
├── backend/          # API REST con Node.js + Express
├── frontend/         # Aplicación React
├── database/         # Scripts SQL y migraciones
├── docs/            # Documentación adicional
├── .github/         # GitHub Actions y templates
└── README.md        # Este archivo
```

## 🛠️ Requisitos Previos

- Node.js 18+ y npm
- PostgreSQL 14+
- Git (para control de versiones)

## ⚡ Instalación Rápida

```bash
# 1. Clonar repositorio
git clone https://github.com/tu-usuario/serviteca-adso.git
cd serviteca-adso

# 2. Configurar base de datos
cd database
psql -U postgres -f migrations/001_initial_schema.sql

# 3. Configurar backend
cd ../backend
cp .env.example .env
# Editar .env con tus configuraciones
npm install
npm run dev

# 4. Configurar frontend
cd ../frontend
cp .env.example .env
npm install
npm run dev
```

## 📖 Documentación

### Documentos Principales
- [Requisitos](requirements.md) - Especificaciones funcionales y no funcionales
- [Diseño Técnico](design.md) - Arquitectura, modelos de datos, wireframes
- [Estrategia GitHub](github-strategy.md) - Control de versiones y colaboración

### API Documentation
La API REST sigue convenciones RESTful:
- `GET /api/clientes` - Listar clientes
- `POST /api/clientes` - Crear cliente
- `GET /api/clientes/:id` - Obtener cliente
- `PUT /api/clientes/:id` - Actualizar cliente
- `DELETE /api/clientes/:id` - Eliminar cliente

*(Ver design.md para endpoints completos)*

## 🔒 Seguridad

- Autenticación con JWT (tokens de 24 horas)
- Hashing de contraseñas con bcrypt
- Validación de inputs en frontend y backend
- Protección contra SQL injection y XSS
- CORS configurado para dominio específico

## 🧪 Testing

```bash
# Backend tests
cd backend
npm test

# Frontend tests
cd frontend
npm test
```

## 📊 Base de Datos

### Diagrama de Entidad-Relación
```
usuarios ─┬─ servicios ── clientes
          └─ carros
```

### Tablas Principales
- `usuarios`: Autenticación del sistema
- `clientes`: Información de clientes
- `carros`: Registro de vehículos
- `servicios`: Historial de servicios prestados

## 🤝 Contribución

1. **Fork** el repositorio
2. **Crear rama** para tu característica: `git checkout -b feature/nueva-funcionalidad`
3. **Commit** tus cambios: `git commit -m 'feat: agregar nueva funcionalidad'`
4. **Push** a la rama: `git push origin feature/nueva-funcionalidad`
5. **Abrir Pull Request**

### Convenciones
- **Commits**: Siguen [Conventional Commits](https://www.conventionalcommits.org/)
- **Código**: Sigue el estilo definido en ESLint/Prettier
- **PRs**: Requieren revisión de al menos un maintainer

## 📈 Roadmap

### Fase 1 (2-3 semanas): MVP
- ✅ **Requisitos y diseño completos**
- 🔄 **Setup del proyecto** (en progreso)
- ⏳ **Autenticación básica**
- ⏳ **CRUD Clientes y Carros**
- ⏳ **CRUD Servicios**
- ⏳ **Consultas e informes básicos**

### Fase 2 (1-2 semanas): Mejoras
- ⏳ **Testing exhaustivo**
- ⏳ **Optimizaciones de UI/UX**
- ⏳ **Documentación completa**

### Fase 3 (Opcional): Avanzado
- ⏳ **Facturación electrónica**
- ⏳ **Sistema de citas**
- ⏳ **Dashboard analítico**
- ⏳ **Notificaciones por email/SMS**

## 📝 Licencia

MIT License - ver [LICENSE](LICENSE) para detalles.

## 👥 Equipo

Proyecto desarrollado como parte del programa ADSO - Análisis y Desarrollo de Software.

## 🆘 Soporte

Para reportar bugs o solicitar características:
1. Revisar [issues existentes](https://github.com/tu-usuario/serviteca-adso/issues)
2. Crear nuevo issue con template apropiado
3. Proporcionar información detallada (pasos para reproducir, entorno, etc.)

---

**Estado del Proyecto**: 🟡 En desarrollo (Diseño completado, implementación en progreso)

*Última actualización: Marzo 2024*