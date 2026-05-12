# 🦁 Plan de Implementación: Aplicación "Zoológico" (Flutter + Firebase)

## 📋 1. Resumen y Alcance
Aplicación multiplataforma (Android, iOS, Web) para gestión y consulta de información de un zoológico. Incluirá autenticación segura, catálogo de animales, información de recintos, perfiles de usuario y sincronización en tiempo real. El desarrollo se centrará en arquitectura mantenible, UX intuitiva y escalabilidad.

---

## 🛠️ 2. Stack Tecnológico y Herramientas Requeridas
| Categoría | Herramientas Recomendadas |
|-----------|---------------------------|
| **Framework** | Flutter (última versión estable), Dart |
| **IDE Principal** | VS Code (con extensiones oficiales) |
| **IDE Alternativo** | Android Studio / IntelliJ IDEA *(nota: "Antigravity" no es un IDE reconocido para Flutter; se recomienda VS Code o Android Studio)* |
| **Backend / BaaS** | Firebase (Auth, Firestore, Crashlytics, Analytics) |
| **Control de Versiones** | Git + GitHub / GitLab |
| **Diseño UI/UX** | Figma o Adobe XD (wireframes, prototipos, design system) |
| **Pruebas / Emulación** | Android Emulator, iOS Simulator, Chrome Web, dispositivo físico |
| **Gestión de Entorno** | Flutter SDK, Dart SDK, Firebase CLI, Node.js (si se usan scripts) |

---

## 📐 3. Arquitectura y Patrones
- **Arquitectura:** Feature-first + Clean-ish (separación por capas: `presentation`, `domain`, `data`, `core`)
- **State Management:** `Provider` (gestión de estado local y global, inyección de dependencias, `ChangeNotifier`)
- **Navegación:** Enrutamiento declarativo con rutas nombradas o paquete de enrutamiento tipo `go_router`
- **Persistencia Local:** `shared_preferences` (sesión básica, preferencias) + caché de imágenes
- **Seguridad:** Reglas de Firestore, validación en cliente y servidor, manejo de errores centralizado

---

## 📦 4. Dependencias Principales (`pubspec.yaml`)
*(Solo lista nominal para referencia futura en el archivo de configuración)*
- **Core Flutter:** `flutter`, `flutter_lints`
- **Firebase:** `firebase_core`, `firebase_auth`, `cloud_firestore`, `firebase_crashlytics`, `firebase_analytics`
- **Estado:** `provider`
- **Navegación:** `go_router` o `auto_route`
- **UI/Assets:** `cached_network_image`, `flutter_svg`, `google_fonts`, `intl`, `flutter_screenutil` o `responsive_framework`
- **Utilidades:** `shared_preferences`, `envied` o `flutter_dotenv`, `uuid`, `http` o `dio` (si se requiere API externa), `equatable` / `freezed` (modelos inmutables, opcional)
- **Pruebas:** `flutter_test`, `mocktail`, `firebase_auth_mocks`, `cloud_firestore_mocks`

---

## 🎨 5. Diseño UI/UX: Lineamientos
1. **Identidad Visual:** Paleta inspirada en naturaleza (verdes, tierras, azules suaves), tipografía legible, iconografía lineal/natural.
2. **Design System:** Tokens de color, espaciado, elevación, bordes, estados de botón (default, hover, pressed, disabled).
3. **Accesibilidad:** Contraste WCAG AA, escalado de texto, soporte para lectores de pantalla, navegación por teclado (web).
4. **Flujos Clave:**
   - Onboarding → Registro/Inicio de sesión → Home → Detalle de animal → Perfil → Ajustes
5. **Responsive:** Layouts adaptativos (grid en tablets/desktop, listas en móviles), manejo de orientación y safe areas.
6. **Prototipado:** Validar en Figma antes de codificar; definir estados de carga, vacío, error y éxito.

---

## 🗺️ 6. Procedimiento Paso a Paso (Fases de Desarrollo)

### 🔹 Fase 1: Configuración Inicial del Proyecto
1. Instalar Flutter SDK, Dart y VS Code con extensiones oficiales.
2. Ejecutar `flutter create zoo_app` y verificar ejecución en al menos 2 plataformas.
3. Configurar `.gitignore`, estructura de carpetas inicial y repositorio remoto.
4. Establecer convenciones de nombre, formateo (`dart format`) y linting.

### 🔹 Fase 2: Integración con Firebase
1. Crear proyecto en Firebase Console.
2. Registrar apps para Android, iOS y Web.
3. Descargar/agregar archivos de configuración (`google-services.json`, `GoogleService-Info.plist`, `firebase-web-config`).
4. Ejecutar `firebase init` y `flutterfire configure` para generar `firebase_options.dart`.
5. Verificar conexión básica imprimiendo logs de inicialización.

### 🔹 Fase 3: Arquitectura y State Management
1. Crear estructura por capas (`lib/core`, `lib/features/auth`, `lib/features/zoo`, `lib/providers`, `lib/services`, `lib/models`).
2. Configurar `Provider` a nivel raíz (`MultiProvider`) con inyección de servicios y modelos.
3. Definir `ChangeNotifier` para estado global (usuario autenticado, carga global, tema).
4. Implementar router base con rutas protegidas y públicas.

### 🔹 Fase 4: UI/UX y Navegación Base
1. Importar design system (colores, tipografías, temas claro/oscuro).
2. Crear widgets reutilizables: `AppButton`, `AppTextField`, `LoadingOverlay`, `EmptyState`, `ErrorBanner`.
3. Implementar estructura de navegación inferior/superior según prototipo.
4. Validar responsividad y accesibilidad en múltiples resoluciones.

### 🔹 Fase 5: Autenticación (Email / Password)
1. Habilitar método Email/Password en Firebase Console.
2. Crear vistas: `LoginScreen`, `RegisterScreen`, `ForgotPasswordScreen`.
3. Implementar validaciones en cliente (formato email, longitud contraseña, coincidencia).
4. Conectar con `FirebaseAuth` mediante un servicio aislado (`AuthService`).
5. Gestionar estados: carga, éxito, error; persistir sesión automáticamente.
6. Implementar logout y limpieza de estado/local storage.
7. Agregar reenvío de verificación de email (opcional pero recomendado).

### 🔹 Fase 6: Firestore y Modelo de Datos
1. Diseñar colecciones principales:
   - `users`: perfil, rol, preferencias, historial
   - `animals`: nombre, especie, hábitat, edad, estado, imágenes, recinto
   - `habitats` / `enclosures`: nombre, capacidad, ubicación, horarios
   - `visits` / `bookings` (si aplica): fecha, estado, usuario asociado
2. Definir índices compuestos necesarios para búsquedas/filtros.
3. Configurar reglas de seguridad en Firestore Console (lectura pública de catálogo, escritura restringida a roles).
4. Crear repositorios/servicios para CRUD: `AnimalRepository`, `UserRepository`.
5. Implementar escuchas en tiempo real (`snapshots`) para datos dinámicos.
6. Habilitar persistencia offline y manejo de conflictos básicos.

### 🔹 Fase 7: Funcionalidades del Zoológico
1. **Home/Dashboard:** Carrusel destacado, categorías, acceso rápido a mapa/horarios.
2. **Catálogo de Animales:** Lista con búsqueda, filtros por especie/hábitat, paginación/lazy loading.
3. **Detalle de Animal:** Galería, descripción, cuidados, curiosidades, recinto asociado.
4. **Perfil de Usuario:** Editar datos, cambiar contraseña, ver historial, preferencias.
5. **Mapa/Recorridos:** Integración estática o con paquete de mapas, marcadores de recintos.
6. **Notificaciones (opcional):** Firebase Cloud Messaging para eventos, alimentaciones o cierres.
7. **Ajustes:** Idioma, tema, caché, cerrar sesión, políticas/privacidad.

### 🔹 Fase 8: Pruebas, Optimización y Despliegue
1. **Pruebas Unitarias:** Servicios, modelos, lógica de negocio.
2. **Pruebas de Widget:** Flujos de UI, validaciones, estados de carga/error.
3. **Pruebas de Integración:** Auth completo, Firestore CRUD offline/online, navegación protegida.
4. **Optimización:** Reducción de imágenes, lazy loading, profiling de rendimiento, análisis de memory leaks.
5. **Monitoreo:** Configurar Crashlytics y Analytics para métricas en producción.
6. **Build:** Generar APK/AAB, IPA (con certificado), build web estático.
7. **Despliegue:** Play Console, TestFlight, Firebase Hosting (web), CI/CD básico (GitHub Actions opcional).

---

## 📝 7. Buenas Prácticas y Consideraciones Críticas
- 🔒 **Seguridad:** Nunca exponer claves sensibles en código; usar `flutterfire configure` y variables de entorno.
- 🛡️ **Reglas Firestore:** Validar en servidor, no confiar solo en cliente; restringir escrituras por `request.auth.uid`.
- 📦 **Estado:** Mantener `Provider` acotado; evitar estados globales innecesarios; usar `Selector` para rebuilds precisos.
- 🌐 **Offline First:** Diseñar UI que tolere desconexión; usar `cache` y sincronización diferida.
- ♿ **Accesibilidad:** Etiquetas semánticas, navegación por foco, contraste validado.
- 📱 **Plataformas:** Verificar comportamientos específicos (iOS safe area, Android back button, web routing).
- 🔄 **Versionado:** Semantic versioning, CHANGELOG, releases etiquetados.

---

## 🚀 8. Siguientes Pasos
1. Validar este plan con stakeholders o equipo.
2. Diseñar wireframes y prototipo navegable en Figma.
3. Definir modelo de datos detallado y reglas de Firestore.
4. Confirmar alcance de funcionalidades MVP vs. futuras versiones.
5. Solicitar generación de código por fase (ej.: `Fase 3 + 5` o `Fase 6`).

¿Deseas que comencemos a generar la implementación por fases específicas, ajustar el alcance del MVP, o profundizar en el modelo de datos y reglas de seguridad de Firestore?
