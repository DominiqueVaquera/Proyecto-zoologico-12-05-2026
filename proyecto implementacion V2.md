Actua como un experto desarrollador de software, crea una aplicación multiplataforma (Android, iOS, Web) para gestión y consulta de información de un zoológico. Incluirá autenticación segura, catálogo de animales, información de recintos, perfiles de usuario y sincronización en tiempo real. El desarrollo se centrará en arquitectura mantenible, UX intuitiva y escalabilidad. 
Framework: dart flutter, IDE Principal: VS Code (con extensiones oficiales), IDE Alternativo: Android Studio / IntelliJ IDEA (nota: "Antigravity" no es un IDE reconocido para Flutter; se recomienda VS Code o Android Studio) Backend / BaaS	Firebase (Auth, Firestore, Crashlytics, Analytics) Control de Versiones	Git + GitHub / GitLab Diseño UI/UX	Figma o Adobe XD (wireframes, prototipos, design system) Pruebas / Emulación	Android Emulator, iOS Simulator, Chrome Web, dispositivo físico Gestión de Entorno	Flutter SDK, Dart SDK, Firebase CLI, Node.js (si se usan scripts).
Arquitectura: Feature-first + Clean-ish (separación por capas: presentation, domain, data, core) State Management: Provider (gestión de estado local y global, inyección de dependencias, ChangeNotifier) Navegación: Enrutamiento declarativo con rutas nombradas o paquete de enrutamiento tipo go_router Persistencia Local: shared_preferences (sesión básica, preferencias) + caché de imágenes Seguridad: Reglas de Firestore, validación en cliente y servidor, manejo de errores centralizado
Dependencias Principales (pubspec.yaml) (Solo lista nominal para referencia futura en el archivo de configuración) Core Flutter: flutter, flutter_lints Firebase: firebase_core, firebase_auth, cloud_firestore, firebase_crashlytics, firebase_analytics Estado: provider Navegación: go_router o auto_route UI/Assets: cached_network_image, flutter_svg, google_fonts, intl, flutter_screenutil o responsive_framework Utilidades: shared_preferences, envied o flutter_dotenv, uuid, http o dio (si se requiere API externa), equatable / freezed (modelos inmutables, opcional) Pruebas: flutter_test, mocktail, firebase_auth_mocks, cloud_firestore_mocks
Identidad Visual: Paleta inspirada en naturaleza (verdes, tierras, azules suaves), tipografía legible, iconografía lineal/natural. Design System: Tokens de color, espaciado, elevación, bordes, estados de botón (default, hover, pressed, disabled). Accesibilidad: Contraste WCAG AA, escalado de texto, soporte para lectores de pantalla, navegación por teclado (web). Flujos Clave: Onboarding → Registro/Inicio de sesión → Home → Detalle de animal → Perfil → Ajustes Responsive: Layouts adaptativos (grid en tablets/desktop, listas en móviles), manejo de orientación y safe areas. Prototipado: Validar en Figma antes de codificar; definir estados de carga, vacío, error y éxito.
Fase 1: Configuración Inicial del Proyecto Instalar Flutter SDK, Dart y VS Code con extensiones oficiales. Ejecutar flutter create zoo_app y verificar ejecución en al menos 2 plataformas. Configurar .gitignore, estructura de carpetas inicial y repositorio remoto. Establecer convenciones de nombre, formateo (dart format) y linting. Fase 2: Integración con Firebase Crear proyecto en Firebase Console. Registrar apps para Android, iOS y Web. Descargar/agregar archivos de configuración (google-services.json, GoogleService-Info.plist, firebase-web-config). Ejecutar firebase init y flutterfire configure para generar firebase_options.dart. Verificar conexión básica imprimiendo logs de inicialización. Fase 3: Arquitectura y State Management Crear estructura por capas (lib/core, lib/features/auth, lib/features/zoo, lib/providers, lib/services, lib/models). Configurar Provider a nivel raíz (MultiProvider) con inyección de servicios y modelos. Definir ChangeNotifier para estado global (usuario autenticado, carga global, tema). Implementar router base con rutas protegidas y públicas. Fase 4: UI/UX y Navegación Base Importar design system (colores, tipografías, temas claro/oscuro). Crear widgets reutilizables: AppButton, AppTextField, LoadingOverlay, EmptyState, ErrorBanner. Implementar estructura de navegación inferior/superior según prototipo. Validar responsividad y accesibilidad en múltiples resoluciones. Fase 5: Autenticación (Email / Password) Habilitar método Email/Password en Firebase Console. Crear vistas: LoginScreen, RegisterScreen, ForgotPasswordScreen. Implementar validaciones en cliente (formato email, longitud contraseña, coincidencia). Conectar con FirebaseAuth mediante un servicio aislado (AuthService). Gestionar estados: carga, éxito, error; persistir sesión automáticamente. Implementar logout y limpieza de estado/local storage. Agregar reenvío de verificación de email (opcional pero recomendado). Fase 6: Firestore y Modelo de Datos Diseñar colecciones principales: users: perfil, rol, preferencias, historial animals: nombre, especie, hábitat, edad, estado, imágenes, recinto habitats / enclosures: nombre, capacidad, ubicación, horarios visits / bookings (si aplica): fecha, estado, usuario asociado Definir índices compuestos necesarios para búsquedas/filtros. Configurar reglas de seguridad en Firestore Console (lectura pública de catálogo, escritura restringida a roles). Crear repositorios/servicios para CRUD: AnimalRepository, UserRepository. Implementar escuchas en tiempo real (snapshots) para datos dinámicos. Habilitar persistencia offline y manejo de conflictos básicos. Fase 7: Funcionalidades del Zoológico Home/Dashboard: Carrusel destacado, categorías, acceso rápido a mapa/horarios. Catálogo de Animales: Lista con búsqueda, filtros por especie/hábitat, paginación/lazy loading. Detalle de Animal: Galería, descripción, cuidados, curiosidades, recinto asociado. Perfil de Usuario: Editar datos, cambiar contraseña, ver historial, preferencias. Mapa/Recorridos: Integración estática o con paquete de mapas, marcadores de recintos. Notificaciones (opcional): Firebase Cloud Messaging para eventos, alimentaciones o cierres. Ajustes: Idioma, tema, caché, cerrar sesión, políticas/privacidad.  Fase 8: Pruebas, Optimización y Despliegue Pruebas Unitarias: Servicios, modelos, lógica de negocio. Pruebas de Widget: Flujos de UI, validaciones, estados de carga/error. Pruebas de Integración: Auth completo, Firestore CRUD offline/online, navegación protegida. Optimización: Reducción de imágenes, lazy loading, profiling de rendimiento, análisis de memory leaks. Monitoreo: Configurar Crashlytics y Analytics para métricas en producción. Build: Generar APK/AAB, IPA (con certificado), build web estático. Despliegue: Play Console, TestFlight, Firebase Hosting (web), CI/CD básico (GitHub Actions opcional).
Seguridad: Nunca exponer claves sensibles en código; usar flutterfire configure y variables de entorno.  Reglas Firestore: Validar en servidor, no confiar solo en cliente; restringir escrituras por request.auth.uid. Estado: Mantener Provider acotado; evitar estados globales innecesarios; usar Selector para rebuilds precisos. Offline First: Diseñar UI que tolere desconexión; usar cache y sincronización diferida. Accesibilidad: Etiquetas semánticas, navegación por foco, contraste validado. Plataformas: Verificar comportamientos específicos (iOS safe area, Android back button, web routing). Versionado: Semantic versioning, CHANGELOG, releases etiquetados.
Validar este plan con stakeholders o equipo. Diseñar wireframes y prototipo navegable en Figma. Definir modelo de datos detallado y reglas de Firestore. Confirmar alcance de funcionalidades MVP vs. futuras versiones. Solicitar generación de código por fase (ej.: Fase 3 + 5 o Fase 6).
Módulo de fauna — el corazón del sistema. ANIMAL es la entidad central, vinculada a ESPECIE (con clasificación taxonómica y estado de conservación IUCN) y a HABITAT. La historia clínica de cada animal se registra en HISTORIAL_MEDICO. Módulo de instalaciones — HABITAT agrupa los recintos, que a su vez se organizan en ZONA (ej. zona africana, zona acuática). Permite controlar capacidad, clima y superficie por recinto. Módulo de personal — EMPLEADO con su CARGO (cuidador, veterinario, guía, etc.). Los VETERINARIO son una especialización implícita que puede normalizarse como subtipo o como flag en EMPLEADO. Módulo de visitantes — VISITANTE realiza VISITA a una o varias zonas. Permite llevar taquilla, control de aforo y estadísticas de asistencia. Módulo de alimentación y suministros — ALIMENTACION registra cada toma (qué animal, qué alimento, cuánto, quién lo hizo). SUMINISTRO y PROVEEDOR gestionan las entradas de insumos (alimento, medicamentos, equipos).
dame una carpeta para modelos
Aqui estan los 5 modulos en la imagen
<img width="725" height="297" alt="image" src="https://github.com/user-attachments/assets/e5d76916-91c1-454a-aba9-8dbe1385c9c3" />
Usa las siguientes imagenes
<img width="592" height="265" alt="image" src="https://github.com/user-attachments/assets/0653e1d9-72f4-4d72-aa73-437d2c5e2364" />
<img width="603" height="356" alt="image" src="https://github.com/user-attachments/assets/57576842-89be-4ed4-aa08-e019f4afb1e7" />
<img width="605" height="287" alt="image" src="https://github.com/user-attachments/assets/014d8c04-057e-4bb2-99fa-53333d57bee1" />
<img width="605" height="286" alt="image" src="https://github.com/user-attachments/assets/1707f115-18ea-4cef-acce-37dbf5ff0284" />
<img width="608" height="298" alt="image" src="https://github.com/user-attachments/assets/6de52b07-6a9c-4a6c-b9ff-9494f7406e54" />
<img width="614" height="245" alt="image" src="https://github.com/user-attachments/assets/1f9bcfb2-1490-4e25-88ae-0eaa09362521" />
<img width="608" height="363" alt="image" src="https://github.com/user-attachments/assets/3b2e8e5b-10b4-4ecf-b9e2-484f89a34d83" />
<img width="604" height="297" alt="image" src="https://github.com/user-attachments/assets/1f483870-8643-48db-bb60-29a1a0a76cc7" />
<img width="462" height="350" alt="image" src="https://github.com/user-attachments/assets/fe4a812a-d943-4a54-9f08-4f7a3a26903e" />
Aquí tienes el pubspec.yaml con las dependencias esenciales para una app Flutter multiplataforma con foco en UI y navegación, orientada al sistema de gestión del zoológico:Algunas notas importantes para el proyecto:
Para instalar todo después de copiar el pubspec.yaml, ejecuta flutter pub get. Para generar el código de Riverpod, usa dart run build_runner watch --delete-conflicting-outputs y déjalo corriendo mientras desarrollas.
Si en el futuro agregas base de datos local o conexión a API, las dependencias cambian bastante — drift o sqflite para SQLite, y dio o http para REST. ¿Te interesa que agregue alguno de esos módulos al pubspec.yaml?
name: zoo_manager
description: Sistema de gestión de zoológico
publish_to: 'none'
version: 1.0.0+1

environment:
  sdk: '^3.3.0'
  flutter: '>=3.19.0'

dependencies:
  flutter:
    sdk: flutter

  # Navegación
  go_router: ^13.2.0

  # Gestión de estado
  flutter_riverpod: ^2.5.1
  riverpod_annotation: ^2.3.5

  # UI y componentes
  flutter_adaptive_scaffold: ^0.1.9
  cached_network_image: ^3.3.1
  shimmer: ^3.0.0
  gap: ^3.0.1

  # Iconos y temas
  flex_color_scheme: ^7.3.1
  hugeicons: ^0.0.7

  # Utilidades
  intl: ^0.19.0
  equatable: ^2.0.5
  logger: ^2.3.0

dev_dependencies:
  flutter_test:
    sdk: flutter
  flutter_lints: ^4.0.0
  riverpod_generator: ^2.4.0
  build_runner: ^2.4.9
  custom_lint: ^0.6.4
  riverpod_lint: ^2.3.10

flutter:
  uses-material-design: true
  generate: true 
Recuerda usar colores atractivos y tenues
