# Estrategia de GitHub para Serviteca ADSO

## Visión General

Este documento complementa el diseño técnico con estrategias específicas para el control de versiones usando Git y GitHub, permitiendo desarrollo colaborativo y mantenimiento de ramas organizadas.

## 1. Configuración del Repositorio

### 1.1 Creación del Repositorio en GitHub
1. Crear nuevo repositorio en GitHub llamado `serviteca-adso`
2. Visibilidad: **Privado** (para desarrollo inicial, cambiar a público si es open source)
3. Incluir: README.md, .gitignore (Node), LICENSE (MIT)
4. Branch inicial: `main`

### 1.2 Estructura Recomendada del Repositorio
```
serviteca-adso/
├── .github/
│   ├── workflows/
│   │   ├── backend-tests.yml
│   │   ├── frontend-tests.yml
│   │   └── deploy.yml (opcional para fases avanzadas)
│   └── PULL_REQUEST_TEMPLATE.md
├── backend/                 # Código del backend
├── frontend/                # Código del frontend
├── database/                # Scripts de base de datos
├── docs/                    # Documentación adicional
├── .gitignore
├── README.md
├── CONTRIBUTING.md
├── LICENSE
└── package.json (workspace root opcional)
```

## 2. Estrategia de Ramas

### 2.1 Git Flow Simplificado
```
main (producción)
    ↑
develop (integración)
    ↑
feature/* (nuevas funcionalidades)
bugfix/* (correcciones)
hotfix/* (urgentes)
```

### 2.2 Ramas Principales
- **`main`**: Contiene código de producción estable. Solo se actualiza mediante releases.
- **`develop`**: Rama de integración continua donde se fusionan las características completadas.

### 2.3 Ramas de Soporte
- **`feature/*`**: Para desarrollar nuevas funcionalidades
  - Ejemplo: `feature/clientes-crud`, `feature/autenticacion-jwt`
  - Se crean desde `develop`
  - Se fusionan de vuelta a `develop` mediante Pull Request
- **`bugfix/*`**: Para corregir bugs en desarrollo
  - Ejemplo: `bugfix/login-validation`
  - Se crean desde `develop`
- **`hotfix/*`**: Para correcciones urgentes en producción
  - Ejemplo: `hotfix/security-patch`
  - Se crean desde `main`
  - Se fusionan tanto a `main` como a `develop`

## 3. Flujo de Trabajo por Fases

### Fase 1: Setup Inicial (Días 1-3)
```bash
# 1. Clonar repositorio
git clone https://github.com/tu-usuario/serviteca-adso.git
cd serviteca-adso

# 2. Configurar ramas iniciales
git checkout -b develop
git push -u origin develop

# 3. Crear estructura base
mkdir backend frontend database docs
# ... crear archivos iniciales

# 4. Primer commit
git add .
git commit -m "chore: initial project structure"
git push origin develop
```

### Fase 2: Desarrollo por Característica
```bash
# Para cada característica (ej: CRUD Clientes)
git checkout develop
git pull origin develop
git checkout -b feature/clientes-crud

# Desarrollo... commits frecuentes
git add .
git commit -m "feat(clientes): agregar modelo y migraciones"
git commit -m "feat(clientes): implementar endpoints CRUD"
git commit -m "test(clientes): agregar pruebas unitarias"

# Finalizar característica
git checkout develop
git pull origin develop
git merge --no-ff feature/clientes-crud
git branch -d feature/clientes-crud
git push origin develop
```

## 4. Convenciones de Commits

### 4.1 Formato Conventional Commits
```
<tipo>(<ámbito>): <descripción>

[ cuerpo opcional ]

[ pie opcional ]
```

### 4.2 Tipos de Commits
- `feat`: Nueva funcionalidad
- `fix`: Corrección de bug
- `docs`: Cambios en documentación
- `style`: Cambios de formato (espacios, comas, etc.)
- `refactor`: Refactorización de código
- `test`: Agregar o corregir pruebas
- `chore`: Cambios en herramientas, configuración, etc.

### 4.3 Ejemplos
```
feat(clientes): agregar endpoint POST /api/clientes
fix(servicios): corregir validación de fecha futura
docs(readme): actualizar guía de instalación
refactor(auth): extraer lógica de validación a middleware
test(carros): agregar pruebas para búsqueda por placa
chore: actualizar dependencias a versiones seguras
```

## 5. Pull Requests y Code Review

### 5.1 Plantilla de Pull Request (.github/PULL_REQUEST_TEMPLATE.md)
```markdown
## Descripción del Cambio

<!-- Describe qué hace este PR y por qué es necesario -->

## Tipo de Cambio
- [ ] Nueva funcionalidad (non-breaking change)
- [ ] Corrección de bug (non-breaking change)
- [ ] Cambio breaking (corrección o funcionalidad que causa incompatibilidad)
- [ ] Refactorización (sin cambios funcionales)
- [ ] Mejora de documentación

## Checklist
- [ ] Mi código sigue las guías de estilo del proyecto
- [ ] He realizado una auto-revisión de mi código
- [ ] He comentado mi código, especialmente en partes complejas
- [ ] He agregado pruebas que prueban mi funcionalidad
- [ ] Las pruebas nuevas y existentes pasan localmente
- [ ] Los cambios afectan la documentación y la he actualizado

## Screenshots (si aplica)

## Notas Adicionales
```

### 5.2 Proceso de Review
1. **Crear PR** desde rama de característica a `develop`
2. **Asignar revisores**: Al menos 1 revisor para cambios significativos
3. **CI/CD**: GitHub Actions ejecuta pruebas automáticamente
4. **Approval**: Revisor aprueba después de revisar código y pruebas
5. **Merge**: Una vez aprobado, merge con `squash` o `merge commit`

## 6. Configuración de GitHub Actions

### 6.1 Workflow Básico para Backend
```yaml
# .github/workflows/backend-tests.yml
name: Backend Tests
on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [develop]

jobs:
  test:
    runs-on: ubuntu-latest
    defaults:
      run:
        working-directory: ./backend
        
    steps:
    - uses: actions/checkout@v3
    
    - name: Setup Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '18'
        cache: 'npm'
        cache-dependency-path: backend/package-lock.json
        
    - name: Install dependencies
      run: npm ci
      
    - name: Run tests
      run: npm test
      
    - name: Run linting
      run: npm run lint
```

### 6.2 Workflow para Frontend
```yaml
# .github/workflows/frontend-tests.yml
name: Frontend Tests
on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [develop]

jobs:
  test:
    runs-on: ubuntu-latest
    defaults:
      run:
        working-directory: ./frontend
        
    steps:
    - uses: actions/checkout@v3
    
    - name: Setup Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '18'
        cache: 'npm'
        cache-dependency-path: frontend/package-lock.json
        
    - name: Install dependencies
      run: npm ci
      
    - name: Run tests
      run: npm test
      
    - name: Run linting
      run: npm run lint
      
    - name: Build
      run: npm run build
```

## 7. Gestión de Releases

### 7.1 Versiones Semánticas (SemVer)
- **Major**: Cambios incompatibles (1.0.0 → 2.0.0)
- **Minor**: Nuevas funcionalidades compatibles (1.0.0 → 1.1.0)
- **Patch**: Correcciones compatibles (1.0.0 → 1.0.1)

### 7.2 Proceso de Release
```bash
# 1. Asegurar que develop está actualizada
git checkout develop
git pull origin develop

# 2. Crear rama de release
git checkout -b release/v1.0.0

# 3. Actualizar versiones
# - package.json (backend y frontend)
# - CHANGELOG.md
# - Documentación

# 4. Merge a main
git checkout main
git merge --no-ff release/v1.0.0
git tag -a v1.0.0 -m "Release v1.0.0"
git push origin main --tags

# 5. Merge de vuelta a develop
git checkout develop
git merge --no-ff release/v1.0.0
git branch -d release/v1.0.0
```

## 8. Seguridad y Permisos

### 8.1 Configuración de Branch Protection
- **`main` branch**:
  - Require pull request reviews (1 aprobación mínima)
  - Require status checks to pass (GitHub Actions)
  - Require branches to be up to date before merging
  - Restrict who can push to matching branches
  - Require linear history

- **`develop` branch**:
  - Require status checks to pass (GitHub Actions)
  - Require branches to be up to date before merging

### 8.2 Acceso al Repositorio
- **Owner/Admin**: Configuración completa
- **Maintainers**: Merge permisos, gestión de issues/PRs
- **Developers**: Push a ramas de características, crear PRs
- **Read-only**: Solo lectura para stakeholders

## 9. Herramientas Adicionales Recomendadas

### 9.1 GitHub Projects
- Tablero Kanban para gestión de tareas
- Integración con Issues y Pull Requests
- Columnas sugeridas: Backlog, To Do, In Progress, Review, Done

### 9.2 GitHub Issues
- Plantillas para bugs, features, documentation
- Labels organizados: `bug`, `enhancement`, `documentation`, `good first issue`
- Milestones para agrupar issues por versión

### 9.3 GitHub Wiki (Opcional)
- Documentación técnica detallada
- Guías de desarrollo
- Arquitectura y decisiones técnicas

## 10. Migración de Código Existente

Si ya hay código desarrollado localmente:
```bash
# 1. Inicializar Git localmente (si no existe)
git init

# 2. Agregar archivos al staging
git add .

# 3. Commit inicial
git commit -m "chore: initial commit from local development"

# 4. Agregar remote de GitHub
git remote add origin https://github.com/tu-usuario/serviteca-adso.git

# 5. Forzar push inicial (solo si el repositorio está vacío)
git branch -M main
git push -u origin main

# 6. Crear rama develop
git checkout -b develop
git push -u origin develop
```

## Conclusión

Esta estrategia proporciona:
- ✅ **Organización clara** de ramas y flujos de trabajo
- ✅ **Calidad de código** mediante code review y CI/CD
- ✅ **Trazabilidad completa** de cambios
- ✅ **Colaboración eficiente** en equipo
- ✅ **Preparación para despliegue** continuo

Se recomienda implementar esta estrategia desde el **día 1** del proyecto para establecer buenas prácticas desde el inicio.