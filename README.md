# 🚗 SubaseApp - Rideshare Intermunicipal Colombia

[![Flutter](https://img.shields.io/badge/Flutter-02569B?style=for-the-badge&logo=flutter&logoColor=white)](https://flutter.dev)
[![Node.js](https://img.shields.io/badge/Node.js-43853D?style=for-the-badge&logo=node.js&logoColor=white)](https://nodejs.org)
[![AWS](https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=white)](https://aws.amazon.com)
[![Google Maps](https://img.shields.io/badge/Google_Maps-4285F4?style=for-the-badge&logo=google-maps&logoColor=white)](https://developers.google.com/maps)

> MVP de aplicación móvil para centralizar viajes intermunicipales en Colombia

## 📋 Descripción del Proyecto

### Resumen del Proyecto

El proyecto es un **MVP (Producto Mínimo Viable)** de una aplicación móvil para centralizar viajes intermunicipales en Colombia, inspirada en un modelo tipo Uber pero con un enfoque único: **los conductores publican ofertas de viajes entre ciudades** (e.g., Bogotá a Medellín), y **los pasajeros pueden ver y reservar estos viajes**.

La app permite que **múltiples pasajeros se unan al mismo viaje**, optimizando asientos disponibles. Es para **pruebas internas y presentación** (no publicación en stores), usada por el equipo de 3 desarrolladores junior y presentada a un grupo cerrado. Los **pagos se manejan en efectivo al llegar al destino**, sin integración de pagos online.

El objetivo es **validar la idea en ~1 mes**, con un enfoque en simplicidad, bajo costo (usando free tiers) y rapidez, dado que el equipo tiene **experiencia limitada en desarrollo móvil**.

## ⭐ Funcionalidades del MVP

El MVP es **una sola app móvil** (Android, con opción de iOS si hay Mac), con **roles diferenciados por login**: conductor y pasajero. Las funciones clave son:

### 🔐 1. Autenticación

- **Registro y login** con email/teléfono (usando AWS Cognito)
- **Roles**: Conductor (publica viajes) o Pasajero (reserva viajes)
- **Verificación básica para conductores**: Subir foto de licencia (almacenada en AWS S3, aprobada manualmente por el equipo)

### 🚗 2. Publicación de Viajes (Conductor)

**Formulario para crear viaje:**
- Ciudades de origen y destino (e.g., Bogotá → Medellín)
- Fecha y hora de salida
- Precio por pasajero (en COP, fijo por viaje)
- Número de asientos disponibles
- Detalles del vehículo (e.g., marca, modelo, opcional)

**Viaje se publica y aparece en lista para pasajeros.**

### 🎫 3. Búsqueda y Reserva de Viajes (Pasajero)

- **Lista de viajes disponibles**, filtrada por ciudades (origen/destino)
- **Detalles del viaje**: Conductor, precio, hora, asientos disponibles
- **Botón "Unirme"** para reservar asiento (reduce asientos disponibles en DB)
- **Muestra ruta aproximada** (usando Google Maps)

### 💵 4. Pago en Efectivo

- Pasajero ve precio al reservar
- **Al llegar al destino**, paga en efectivo al conductor
- **Conductor marca "Pagado"** en app (actualiza estado en DB: `pagado: true`)

### 💬 5. Chat In-App

- **Comunicación básica** entre conductor y pasajeros del mismo viaje (real-time via AWS AppSync)
- **Ejemplo**: Confirmar punto de encuentro

### 🔔 6. Notificaciones

**Push notifications (AWS SNS) para:**
- **Pasajero**: Confirmación de reserva
- **Conductor**: Nuevo pasajero se unió
- **Opcional**: Alertas de viaje próximo

### 🗺️ 7. Mapas

**Integración Google Maps para:**
- Mostrar ruta estimada (ciudad X a Y)
- Calcular distancia aproximada (visible en detalles del viaje)

### 👤 8. Verificación y Perfil

- **Perfil básico**: Nombre, teléfono, foto (opcional)
- **Conductores**: Suben foto de licencia (almacenada en S3, revisión manual)

## 🛠️ Herramientas y Tecnologías

El proyecto usa herramientas **accesibles para un equipo junior**, con énfasis en **free tiers** para mantener costos en **~$0-20/mes**. Todo se desarrolla en **una sola codebase** para Android (iOS opcional) y **backend serverless**.

### 📱 Frontend (App Móvil)

- **Flutter (Dart)**: Framework cross-platform para una sola app (Android/iOS). Fácil para UI, con paquetes para mapas, auth, real-time
- **VS Code**: IDE con extensiones Flutter, Dart, Prettier, GitLens
- **Figma (opcional)**: Prototipos UI (pantallas: login, dashboard, formulario viaje)

### ⚙️ Backend

- **Node.js con Express**: APIs REST para lógica (publicar/ver viajes, reservas). Deploy en AWS Lambda (serverless)
- **AWS Amplify**: Gestiona backend, auth, DB, storage. Fácil integración con Flutter
- **AWS DynamoDB**: Base de datos NoSQL para viajes, usuarios, reservas
- **AWS Cognito**: Autenticación (email/teléfono, roles)
- **AWS S3**: Almacenamiento de fotos (licencias, perfiles)
- **AWS AppSync**: Chat real-time con GraphQL
- **AWS SNS**: Notificaciones push

### 🌐 Servicios Externos

- **Google Maps API**: Rutas y distancias entre ciudades. **$200 crédito gratis/mes**
- **Postman**: Testeo de APIs

### 🤝 Colaboración y Gestión

- **GitHub**: Repo privado (SubaseApp) para version control. Estructura: `/frontend`, `/backend`, `/docs`
- **Trello/Notion**: Kanban board para tasks (To Do, In Progress, Done)
- **Git**: Control de versiones, con branches (`main`, `develop`, `feature/xxx`)

### 🧪 Testing

- **Emuladores**: Android Studio (Android), Xcode (iOS, si Mac)
- **Sideload**: Instalar APK manualmente en Android físico para pruebas
- **Manual testing**: Equipo prueba flujos (login, publicar, reservar)
- **Unit tests (opcional)**: Flutter built-in o Jest para backend

## 📁 Estructura del Repositorio

```
SubaseApp/
├── frontend/           # Proyecto Flutter (app móvil)
├── backend/            # Node.js APIs (Express, deploy en Lambda)
├── docs/              # User stories, notas, diagramas
├── README.md          # Setup instructions, descripción
└── .gitignore         # Ignora builds, claves, etc.
```

## 📊 Contexto Adicional

### 👥 Equipo
- **3 desarrolladores junior**, sin experiencia avanzada en móvil
- **Aprendiendo Flutter/Node.js**

### ⏱️ Duración
- **~1 mes** para pruebas y presentación (no publicación en stores)

### 💵 Presupuesto
- **Bajo (~$0-20/mes)**, usando free tiers de AWS y Google

### 🎯 Uso
- **Pruebas internas** (equipo + grupo cerrado)
- **No público externo**

### 💰 Pagos
- **En efectivo**, sin integración online
- **Conductor marca "Pagado" en app**

### 📱 Plataforma
- **Android prioritario** (emuladores o dispositivos físicos)
- **iOS opcional** (simulador si hay Mac)

### 🌍 Idioma
- **Español** (interfaz y datos)

### ⚖️ Regulaciones
- **Disclaimer en app**: "No responsables de viajes, verifica conductores"
- **Revisión manual de licencias**

## 🚀 Instalación y Configuración

### Prerrequisitos
- Flutter SDK
- Node.js (v16+)
- Git
- Android Studio / VS Code

### Clonar el Repositorio
```bash
git clone https://github.com/tu-usuario/SubaseApp.git
cd SubaseApp
```

### Configurar Frontend (Flutter)
```bash
cd frontend
flutter pub get
flutter doctor
```

### Configurar Backend (Node.js)
```bash
cd backend
npm install
npm run dev
```

## 🧪 Testing y Desarrollo

### 📱 Emuladores
- **Android Studio** (Android)
- **Xcode** (iOS, si Mac)

### 📦 Sideload
- Instalar APK manualmente en Android físico para pruebas

### 🔍 Manual Testing
- Equipo prueba flujos (login, publicar, reservar)

### ⚡ Unit Tests (Opcional)
- **Flutter built-in** o **Jest** para backend

### Generar APK para Pruebas
```bash
# En el directorio frontend
flutter build apk --debug
```

## 💡 Contribuir

### 🔄 Control de Versiones
- **GitHub**: Control de versiones
- **Branches**: `main`, `develop`, `feature/xxx`

### 📋 Gestión de Tareas
- **Trello/Notion**: Kanban board (To Do, In Progress, Done)

### Flujo de Trabajo
1. Fork el proyecto
2. Crear branch de feature (`git checkout -b feature/nueva-funcionalidad`)
3. Commit cambios (`git commit -m 'Agregar nueva funcionalidad'`)
4. Push al branch (`git push origin feature/nueva-funcionalidad`)
5. Crear Pull Request

## 📝 Notas para Desarrolladores

- ✅ Proporcionar código **simple y funcional** (Flutter/Dart, Node.js/Express)
- 📚 Sugerir tutoriales **accesibles** (YouTube, docs oficiales) para juniors
- 💰 Priorizar **free tiers** (AWS, Google Maps) y minimizar costos
- 🔧 Incluir ejemplos de código para: login, publicación viaje, reservas, chat, notificaciones
- 🚨 Si hay errores (e.g., Flutter doctor), ofrecer pasos específicos para resolver
- 🚫 **No mencionar pagos online** (Stripe/PayU); enfócate en flujo efectivo
- 🇪🇸 Responder en español, con pasos claros y prácticos

## 📄 Licencia

Este proyecto es para **uso interno y pruebas**. No está destinado para producción comercial.

---

**Desarrollado con ❤️ en Colombia 🇨🇴**