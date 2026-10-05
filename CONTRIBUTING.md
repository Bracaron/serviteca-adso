# Guía de Contribución

¡Gracias por tu interés en contribuir a Serviteca ADSO! Esta guía te ayudará a entender cómo puedes colaborar con el proyecto.

## 🚀 Cómo Contribuir

### 1. Reportar Bugs
Si encuentras un bug, por favor:
1. Busca en [issues](https://github.com/tu-usuario/serviteca-adso/issues) para ver si ya fue reportado
2. Si no existe, crea un nuevo issue con:
   - Descripción clara del problema
   - Pasos para reproducir
   - Comportamiento esperado vs actual
   - Capturas de pantalla si aplica
   - Información de entorno (SO, navegador, versión)

### 2. Solicitar Funcionalidades
Para nuevas funcionalidades:
1. Busca si ya existe una solicitud similar
2. Crea un issue con:
   - Descripción detallada de la funcionalidad
   - Casos de uso
   - Beneficios esperados
   - Posible impacto

### 3. Enviar Código
Para contribuir con código:

#### Pasos:
1. **Fork** el repositorio
2. **Clona** tu fork:
   ```bash
   git clone https://github.com/tu-usuario/serviteca-adso.git
   cd serviteca-adso
   ```
3. **Configura** el entorno:
   ```bash
   git checkout develop
   git pull origin develop
   ```
4. **Crea una rama**:
   ```bash
   git checkout -b feature/nombre-funcionalidad
   ```
5. **Desarrolla** tu contribución
6. **Ejecuta tests**:
   ```bash
   # Backend
   cd backend
   npm test
   
   # Frontend
   cd frontend
   npm test
   ```
7. **Commits** con convenciones:
   ```bash
   git add .
   git commit -m "feat: descripción de los cambios"
   ```
8. **Push** a tu fork:
   ```bash
   git push origin feature/nombre-funcionalidad
   ```
9. **Crea Pull Request** a la rama `develop`

## 📋 Convenciones

### Commits
Usamos [Conventional Commits](https://www.conventionalcommits.org/):
- `feat:` Nueva funcionalidad
- `fix:` Corrección de bug
- `docs:` Cambios en documentación
- `style:` Cambios de formato
- `refactor:` Refactorización
- `test:` Cambios en pruebas
- `chore:` Cambios en herramientas/configuración

### Código
- **TypeScript**: Usa tipado fuerte
- **ESLint/Prettier**: Sigue las reglas de estilo
- **Documentación**: Comenta código complejo
- **Pruebas**: Agrega tests para nueva funcionalidad

### Ramas
- `main`: Producción
- `develop`: Desarrollo
- `feature/*`: Nueva funcionalidad
- `bugfix/*`: Corrección de bugs
- `hotfix/*`: Correcciones urgentes

## 🧪 Pruebas

### Backend
```bash
cd backend
npm test        # Ejecutar pruebas
npm run test:coverage  # Con cobertura
npm run lint    # Verificar estilo
```

### Frontend
```bash
cd frontend
npm test        # Ejecutar pruebas
npm run lint    # Verificar estilo
npm run build   # Verificar que compila
```

## 📝 Code Review

Todos los PRs requieren:
1. ✅ Tests pasan
2. ✅ Linting aprobado
3. ✅ Build exitoso
4. ✅ Al menos 1 aprobación
5. ✅ Commits siguen convenciones

## 🏷️ Etiquetas de Issues

- `bug`: Error en el sistema
- `enhancement`: Mejora de funcionalidad
- `documentation`: Cambios en docs
- `good first issue`: Ideal para nuevos contribuidores
- `help wanted`: Necesita colaboración

## 🤝 Código de Conducta

Este proyecto sigue un código de conducta para fomentar un ambiente respetuoso y colaborativo. Por favor, lee el [Código de Conducta](CODE_OF_CONDUCT.md) antes de contribuir.

## ❓ Preguntas Frecuentes

### ¿Cómo empiezo si soy nuevo?
1. Busca issues con `good first issue`
2. Pide ayuda en el issue si tienes dudas
3. Sigue los pasos de "Enviar Código"

### ¿Qué hago si mi PR no es revisado?
- Espera al menos 48 horas
- Menciona a un maintainer si es urgente
- Verifica que cumple todas las convenciones

### ¿Puedo trabajar en múltiples issues?
Sí, pero crea ramas separadas para cada uno.

## 📞 Contacto

- **Issues**: Para bugs y funcionalidades
- **Discussions**: Para preguntas y discusiones
- **Email**: Para contacto directo con maintainers

---

¡Gracias por contribuir! Tu ayuda hace que este proyecto sea mejor para todos. 🚀