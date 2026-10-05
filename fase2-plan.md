# Plan de Implementación - Fase 2: CRUD Clientes y Carros

## Objetivo General
Implementar los módulos completos de Clientes y Carros (Vehículos) con operaciones CRUD, validaciones y interfaces de usuario.

## Fecha Estimada: 4-5 días de desarrollo

## Dependencias
- ✅ **Fase 1 completada**: Setup del proyecto, autenticación, base de datos
- ✅ **Diseño técnico aprobado**: design.md
- ✅ **Base de datos**: Tablas clientes y carros creadas

## Componentes a Implementar

### 1. Backend - Módulo Clientes
**Modelo (Cliente.ts):**
```typescript
interface Cliente {
  identificacion: string;  // PK, VARCHAR(20)
  nombres: string;        // VARCHAR(100)
  apellidos: string;      // VARCHAR(100)
  correo: string;         // VARCHAR(100), UNIQUE
  celular: string;        // VARCHAR(15)
  created_at: Date;
}
```

**Endpoints (clientes.routes.ts):**
- `GET /api/clientes` - Listar clientes (con paginación)
- `POST /api/clientes` - Crear cliente
- `GET /api/clientes/:identificacion` - Obtener cliente por ID
- `PUT /api/clientes/:identificacion` - Actualizar cliente
- `DELETE /api/clientes/:identificacion` - Eliminar cliente (solo si no tiene servicios)

**Validaciones (express-validator):**
- Identificación: 5-20 caracteres, único
- Nombres/Apellidos: 2-100 caracteres, solo letras y espacios
- Correo: formato válido, único
- Celular: 10-15 dígitos, solo números

### 2. Backend - Módulo Carros
**Modelo (Carro.ts):**
```typescript
interface Carro {
  placa: string;          // PK, VARCHAR(10)
  marca: string;          // VARCHAR(50)
  modelo: string;         // VARCHAR(50)
  created_at: Date;
}
```

**Endpoints (carros.routes.ts):**
- `GET /api/carros` - Listar carros (con paginación)
- `POST /api/carros` - Crear carro
- `GET /api/carros/:placa` - Obtener carro por placa
- `PUT /api/carros/:placa` - Actualizar carro
- `DELETE /api/carros/:placa` - Eliminar carro (solo si no tiene servicios)

**Validaciones:**
- Placa: 3-10 caracteres, mayúsculas, números, sin espacios, único
- Marca/Modelo: 2-50 caracteres

### 3. Frontend - Interfaz Clientes

#### Páginas (frontend/src/pages/Clientes/):
1. **AgregarCliente.tsx**
   - Formulario con todos los campos
   - Validación en tiempo real
   - Botones: Guardar, Cancelar, Limpiar
   - Integración con backend

2. **ConsultarCliente.tsx**
   - Campo de búsqueda (ID o nombre)
   - Resultados en tabla
   - Botón "Ver detalles"
   - Opción editar/eliminar

3. **ListarClientes.tsx**
   - Tabla paginada
   - Filtros: por nombre, ID, correo
   - Ordenamiento por columnas
   - Exportar a CSV/Excel

#### Componentes (frontend/src/components/forms/):
- **ClienteForm.tsx**: Formulario reutilizable
- **ClienteTable.tsx**: Tabla con acciones

#### Servicios (frontend/src/services/):
- **clientes.service.ts**: API calls al backend
- **clientes.types.ts**: TypeScript interfaces

### 4. Frontend - Interfaz Carros

#### Páginas (frontend/src/pages/Carros/):
1. **AgregarCarro.tsx**
   - Formulario simple (placa, marca, modelo)
   - Validación de placa única
   - Integración con backend

2. **ConsultarCarro.tsx**
   - Búsqueda por placa o marca
   - Resultados en tabla
   - Opción editar/eliminar

3. **ListarCarros.tsx**
   - Tabla paginada de carros
   - Filtros por marca, modelo
   - Integración con selectores de servicios

#### Componentes:
- **CarroForm.tsx**: Formulario reutilizable
- **CarroTable.tsx**: Tabla con acciones

#### Servicios:
- **carros.service.ts**: API calls al backend
- **carros.types.ts**: TypeScript interfaces

## Plan de Implementación por Días

### Día 1: Backend Clientes
**Objetivo:** Endpoints CRUD completos para clientes
1. Crear modelo Cliente con validaciones
2. Implementar controlador clientes.controller.ts
3. Crear rutas clientes.routes.ts
4. Configurar validadores con express-validator
5. Escribir pruebas unitarias básicas
6. Verificar con Postman/Insomnia

**Entregables:**
- Modelo Cliente.ts
- Controlador clientes.controller.ts
- Rutas clientes.routes.ts
- Validadores específicos
- Pruebas unitarias

### Día 2: Backend Carros
**Objetivo:** Endpoints CRUD completos para carros
1. Crear modelo Carro con validaciones
2. Implementar controlador carros.controller.ts
3. Crear rutas carros.routes.ts
4. Configurar validadores
5. Escribir pruebas unitarias
6. Verificar integración

**Entregables:**
- Modelo Carro.ts
- Controlador carros.controller.ts
- Rutas carros.routes.ts
- Validadores específicos
- Pruebas unitarias

### Día 3: Frontend Clientes
**Objetivo:** Interfaces completas para gestión de clientes
1. Crear páginas Clientes (Agregar, Consultar, Listar)
2. Implementar ClienteForm.tsx componente reutilizable
3. Crear clientes.service.ts para API calls
4. Implementar validaciones frontend con Yup
5. Crear tabla de clientes con paginación
6. Integrar con backend

**Entregables:**
- Páginas: AgregarCliente.tsx, ConsultarCliente.tsx, ListarClientes.tsx
- Componente: ClienteForm.tsx
- Servicio: clientes.service.ts
- Validaciones frontend
- Integración completa

### Día 4: Frontend Carros
**Objetivo:** Interfaces completas para gestión de carros
1. Crear páginas Carros (Agregar, Consultar, Listar)
2. Implementar CarroForm.tsx componente reutilizable
3. Crear carros.service.ts para API calls
4. Implementar validaciones frontend
5. Crear tabla de carros con paginación
6. Integrar con backend

**Entregables:**
- Páginas: AgregarCarro.tsx, ConsultarCarro.tsx, ListarCarros.tsx
- Componente: CarroForm.tsx
- Servicio: carros.service.ts
- Validaciones frontend
- Integración completa

### Día 5: Integración y Pruebas
**Objetivo:** Integración completa y pruebas E2E
1. Integrar módulos en el menú principal
2. Crear navegación entre páginas
3. Implementar manejo de errores consistente
4. Realizar pruebas E2E con Cypress
5. Optimizar rendimiento (lazy loading)
6. Documentar API y componentes

**Entregables:**
- Integración completa en Dashboard
- Navegación funcionando
- Manejo de errores robusto
- Pruebas E2E básicas
- Documentación actualizada

## Consideraciones Técnicas

### Validaciones Coordinadas
- **Frontend**: Validación en tiempo real con Yup + React Hook Form
- **Backend**: Validación estricta con express-validator
- **Base de datos**: Constraints (UNIQUE, CHECK, NOT NULL)

### Manejo de Errores
- Backend: Middleware de errores centralizado
- Frontend: Componente AlertMessage.tsx reutilizable
- API: Formatos de error estándar (ApiError interface)

### Seguridad
- Todos los endpoints protegidos con middleware auth
- Validación de inputs para prevenir SQL injection
- Sanitización de datos
- Rate limiting para endpoints públicos

### Performance
- Paginación server-side para listados grandes
- Lazy loading de rutas React
- Memoización de componentes
- Optimización de queries SQL

## Estructura de Carpetas a Crear

### Backend:
```
backend/src/
├── controllers/
│   ├── clientes.controller.ts
│   └── carros.controller.ts
├── models/
│   ├── Cliente.ts
│   └── Carro.ts
├── routes/
│   ├── clientes.routes.ts
│   └── carros.routes.ts
├── validators/
│   ├── clientes.validator.ts
│   └── carros.validator.ts
└── tests/
    ├── clientes.test.ts
    └── carros.test.ts
```

### Frontend:
```
frontend/src/
├── pages/
│   ├── Clientes/
│   │   ├── AgregarCliente.tsx
│   │   ├── ConsultarCliente.tsx
│   │   └── ListarClientes.tsx
│   └── Carros/
│       ├── AgregarCarro.tsx
│       ├── ConsultarCarro.tsx
│       └── ListarCarros.tsx
├── components/
│   ├── forms/
│   │   ├── ClienteForm.tsx
│   │   └── CarroForm.tsx
│   └── tables/
│       ├── ClienteTable.tsx
│       └── CarroTable.tsx
├── services/
│   ├── clientes.service.ts
│   └── carros.service.ts
├── hooks/
│   ├── useClientes.ts
│   └── useCarros.ts
└── types/
    ├── cliente.ts
    └── carro.ts
```

## Criterios de Aceptación

### Backend:
1. ✅ Todos los endpoints responden correctamente
2. ✅ Validaciones funcionan (frontend y backend)
3. ✅ Manejo de errores apropiado
4. ✅ Pruebas unitarias con >80% cobertura
5. ✅ Conexión a base de datos estable

### Frontend:
1. ✅ Interfaces responsivas (mobile y desktop)
2. ✅ Validaciones en tiempo real
3. ✅ Integración completa con backend
4. ✅ Manejo de estados de carga/error
5. ✅ Navegación fluida entre páginas

### Integración:
1. ✅ Módulos integrados en menú principal
2. ✅ Usuario puede realizar CRUD completo
3. ✅ Errores mostrados apropiadamente
4. ✅ Performance aceptable (<2s respuesta)

## Estrategia de Git para Fase 2

### Ramas:
- **feature/clientes-crud**: Para módulo clientes
- **feature/carros-crud**: Para módulo carros
- **feature/fase2-integration**: Para integración final

### Flujo:
1. Crear rama desde `develop`: `git checkout -b feature/clientes-crud develop`
2. Desarrollar módulo clientes
3. Crear PR a `develop`
4. Repetir para carros
5. Rama de integración final
6. Merge a `develop` después de aprobación

### Commits:
- `feat(clientes): agregar endpoints CRUD`
- `feat(clientes): implementar interfaz agregar cliente`
- `feat(carros): agregar modelo y validaciones`
- `fix(clientes): corregir validación de celular`
- `test(carros): agregar pruebas unitarias`

## Próximos Pasos después de Fase 2

1. **Revisión de código**: Code review entre módulos
2. **Pruebas de integración**: Verificar que módulos funcionan juntos
3. **Optimización**: Mejorar performance donde sea necesario
4. **Documentación**: Actualizar documentación de API y componentes
5. **Preparar Fase 3**: CRUD Servicios + Consultas

## Riesgos y Mitigación

### Riesgo 1: Complejidad de validaciones cruzadas
- **Mitigación**: Implementar validaciones por capa (frontend, backend, BD)
- **Mitigación**: Crear validadores reutilizables

### Riesgo 2: Performance en listados grandes
- **Mitigación**: Implementar paginación server-side desde el inicio
- **Mitigación**: Índices en base de datos para búsquedas frecuentes

### Riesgo 3: Integración frontend-backend
- **Mitigación**: Definir interfaces TypeScript compartidas
- **Mitigación**: Crear servicios frontend con error handling robusto

### Riesgo 4: Mantenimiento de código
- **Mitigación**: Seguir convenciones estrictas de código
- **Mitigación**: Documentar componentes y endpoints

---

**Nota:** Este plan asume que la Fase 1 está completa y funcionando. Los días estimados son para desarrollo a tiempo completo. Ajustar según disponibilidad del equipo.

**Estado:** 🟡 Esperando finalización de Fase 1