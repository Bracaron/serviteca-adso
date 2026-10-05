# Requisitos - Aplicación Web Serviteca ADSO

## 1. Descripción General

La aplicación web Serviteca ADSO es un sistema de gestión para talleres automotrices que permite administrar la información generada en una serviteca que presta los siguientes servicios:

- Cambio de Aceite
- Sincronización  
- Alineación
- Lavado

El sistema permitirá registrar clientes, vehículos y servicios prestados, así como consultar la información histórica de cada vehículo.

## 2. Entidades y Datos

### 2.1 Cliente
- **Identificación** (única, obligatoria)
- **Nombres** (obligatorio)
- **Apellidos** (obligatorio)
- **Correo electrónico** (obligatorio, formato validado)
- **Celular** (obligatorio)

### 2.2 Carro (Vehículo)
- **Placa** (única, obligatoria)
- **Marca** (obligatorio)
- **Modelo** (obligatorio)

### 2.3 Servicio
- **Placa del carro** (relación con vehículo, obligatorio)
- **Identificación del cliente** (relación con cliente, obligatorio)
- **Fecha del servicio** (obligatorio, formato fecha)
- **Tipo de servicio** (obligatorio, selección entre: Cambio de Aceite, Sincronización, Alineación, Lavado)

## 3. Funcionalidades

### 3.1 Autenticación y Seguridad
- **Login/Logout**: Validación de usuarios mediante usuario y contraseña
- **Control de acceso**: Solo usuarios autenticados pueden acceder a las funcionalidades

### 3.2 Gestión de Clientes (CRUD)
- **Agregar cliente**: Registrar nuevos clientes con todos los datos requeridos
- **Consultar cliente**: Buscar cliente por identificación o nombre
- **Listar clientes**: Ver todos los clientes registrados con opciones de filtrado

### 3.3 Gestión de Carros (CRUD)
- **Agregar carro**: Registrar nuevos vehículos con placa, marca y modelo
- **Consultar carro**: Buscar vehículo por placa o marca
- **Listar carros**: Ver todos los vehículos registrados

### 3.4 Gestión de Servicios (CRUD)
- **Agregar servicio**: Registrar nuevo servicio con:
  - Placa del carro (validar existencia)
  - Identificación del cliente (validar existencia)
  - Fecha del servicio
  - Tipo de servicio seleccionado
- **Consultar servicio**: Buscar servicios por diferentes criterios (placa, fecha, tipo)
- **Listar servicios**: Ver todos los servicios registrados
- **Consultar servicios por carro**: Visualizar todos los servicios prestados a un vehículo específico

## 4. Interfaces de Usuario

### 4.1 Interfaz de Login
- Campos: Usuario y Contraseña
- Validación de credenciales
- Mensajes de error claros

### 4.2 Interfaz Principal (Menú)
La aplicación debe tener una interfaz con menú de opciones organizado así:

```
Menú Principal
├── Menú Clientes
│   ├── Agregar Cliente
│   ├── Consultar Cliente  
│   └── Listar Clientes
├── Menú Carros
│   ├── Agregar Carro
│   ├── Consultar Carro
│   └── Listar Carros
├── Menú Servicios
│   ├── Agregar Servicio
│   ├── Consultar Servicio
│   └── Listar Servicios
├── Menú Ayuda
│   └── Información del sistema
└── Menú Salir
```

### 4.3 Interfaz para Registrar Cliente
- Formulario con campos: Identificación, Nombres, Apellidos, Correo, Celular
- Validación de datos en tiempo real
- Botones: Guardar, Cancelar, Limpiar

### 4.4 Interfaz para Registrar Carro
- Formulario con campos: Placa, Marca, Modelo
- Validación de placa única
- Botones: Guardar, Cancelar

### 4.5 Interfaz para Registrar Servicio
- Formulario con:
  - Campo de búsqueda/select para Placa del carro
  - Campo de búsqueda/select para Identificación del cliente
  - Selector de fecha
  - Selector de tipo de servicio (dropdown con 4 opciones)
- Validación de existencia de carro y cliente
- Botones: Guardar, Cancelar

### 4.6 Interfaz para Consultar Servicios por Carro
- Campo de entrada para placa del carro
- Botón de búsqueda
- Tabla que muestre:
  - Placa del carro
  - Servicio prestado (tipo)
  - Fecha del servicio
- Opción de exportar resultados (opcional)

## 5. Flujos de Trabajo

### 5.1 Flujo de Registro de Servicio
1. Usuario selecciona "Agregar Servicio"
2. Sistema muestra formulario de registro
3. Usuario busca/selecciona placa del carro (debe existir)
4. Usuario busca/selecciona identificación del cliente (debe existir)
5. Usuario selecciona fecha y tipo de servicio
6. Sistema valida que no haya conflictos de datos
7. Sistema guarda el servicio y muestra confirmación

### 5.2 Flujo de Consulta de Historial por Carro
1. Usuario selecciona "Consultar Servicios por Carro"
2. Sistema muestra campo para ingresar placa
3. Usuario ingresa placa y hace clic en buscar
4. Sistema consulta base de datos
5. Sistema muestra tabla con todos los servicios del vehículo
6. Usuario puede ordenar por fecha o tipo de servicio

## 6. Requisitos Técnicos

### 6.1 Requisitos No Funcionales
- **Interfaz web**: Responsive design (funciona en desktop y móvil)
- **Persistencia**: Base de datos relacional (MySQL, PostgreSQL, SQLite)
- **Backend**: API RESTful para separar frontend de lógica de negocio
- **Frontend**: Framework moderno (React, Vue, Angular) o enfoque tradicional
- **Seguridad**: Protección contra inyección SQL, XSS, CSRF
- **Usabilidad**: Interfaz intuitiva y fácil de usar

### 6.2 Validaciones
- Campos obligatorios marcados claramente
- Validación de formato de correo electrónico
- Validación de placa única para vehículos
- Validación de identificación única para clientes
- Fechas no pueden ser futuras (solo servicios pasados o presente)

### 6.3 Consideraciones de Negocio
- Un cliente puede tener múltiples vehículos
- Un vehículo puede tener múltiples servicios a lo largo del tiempo
- Cada servicio está asociado a un cliente y un vehículo específico
- La relación cliente-vehículo se establece al momento del servicio

## 7. Escenarios de Uso

### 7.1 Escenario 1: Primer uso del sistema
1. Administrador inicia sesión
2. Registra clientes frecuentes
3. Registra vehículos de esos clientes
4. Comienza a registrar servicios prestados

### 7.2 Escenario 2: Consulta de historial
1. Cliente llega a la serviteca
2. Recepcionista ingresa placa del vehículo
3. Sistema muestra todos los servicios previos realizados
4. Recepcionista puede ver patrones de mantenimiento

### 7.3 Escenario 3: Reportes básicos
- Número de servicios por tipo en un período
- Clientes más frecuentes
- Vehículos con más servicios

## 8. Próximos Pasos (Fases Futuras)

1. **Fase 2**: Generación de facturas y recibos
2. **Fase 3**: Sistema de inventario de repuestos
3. **Fase 4**: Agenda de citas para servicios
4. **Fase 5**: Notificaciones por correo/SMS a clientes
5. **Fase 6**: Dashboard con métricas del negocio