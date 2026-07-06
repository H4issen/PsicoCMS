# PsicoCMS

**CMS monolítico para psicólogos independientes**

Construido con Laravel, PHP, MySQL y JavaScript vanilla. Cubre todo el flujo de trabajo de una psicóloga: web pública, blog, sistema de reservas, panel de administración, pacientes, historias clínicas y más.

---

## Stack tecnológico

| Capa        | Tecnología                          |
|-------------|-------------------------------------|
| Backend     | PHP 8.2+ / Laravel 11               |
| Base de datos | MySQL / MariaDB                    |
| Frontend    | HTML5 semántico, CSS3 nativo, JavaScript ES6+ |
| Editor WYSIWYG | Jodit 4.7.6                      |
| Calendario  | FullCalendar                        |
| PDF         | DomPDF                              |
| Iconos      | Font Awesome 6                      |
| Fuentes     | Lexend, Castoro, Montserrat         |

---

## Arquitectura

Aplicación web monolítica con dos caras:

### Parte pública
- Homepage con información de la psicóloga
- Sobre mí
- Servicios y especialidades
- Planes y precios (online / presencial)
- Blog con categorías
- Preguntas frecuentes
- Sistema de reserva de citas (wizard 3 pasos)
- Contacto
- 5 temas visuales seleccionables (elegante, moderno, minimalista, natural, profesional)
- Modo landing (1 página) o multipágina

### Dashboard privado (`/panel-psicologa`)
- Login seguro con email + contraseña (teléfono opcional)
- Panel de inicio con KPIs y estadísticas reales
- Gestión de citas (CRUD + calendario FullCalendar)
- Gestión de pacientes (CRUD + búsqueda AJAX)
- Gestión de historias clínicas (notas + archivos adjuntos)
- Gestión de blog (CRUD + categorías)
- Gestión de FAQ (CRUD + reorden)
- Gestión de disponibilidad (horarios semanales, descanso entre sesiones, modo vacaciones, periodos de vacaciones)
- Gestión de servicios, especialidades y planes
- Gestión de temas visuales (5 temas, preview, modo landing/multipágina)
- Gestión de galería de imágenes
- Configuración general, información pública, frases, redes sociales, email, funcionalidades
- Protección de datos (plantilla WYSIWYG + PDF por paciente)
- Buscador global (citas, pacientes, historias, blog, FAQ)
- Tema claro/oscuro con 8 colores seleccionables
- Notificaciones en tiempo real (nuevas reservas, citas próximas)
- Ayuda / tutorial integrado

---

## Funcionalidades clave

### Asistente de instalación
Wizard multi-paso que guía a la psicóloga en la configuración inicial: conexión BD, datos personales, servicios, horarios, foto, selección de tema. Todo desde el navegador, sin tocar código.

### Sistema de citas con validación de solapamiento
No se pueden crear dos citas en el mismo espacio de tiempo. La disponibilidad se configura por separado para online y presencial, con duración de sesión y descanso entre sesiones.

### Notificaciones
- Notificación en el dashboard cuando un paciente reserva una cita
- Aviso automático 10 minutos antes de una cita
- Polling cada 30 segundos, icono de campana con animación
- Panel desplegable con historial de notificaciones

### WhatsApp integrado
- En web pública: el icono de teléfono abre WhatsApp con el número de la psicóloga (+51 Perú)
- En dashboard: botón WhatsApp por paciente para contactar directamente

### 5 temas visuales
Cada tema tiene paleta de colores única, tipografías, estilos de banner y botones. El tema activo se aplica al instante desde el dashboard.

### Modo oscuro
- Dashboard: toggle claro/oscuro + 8 colores primarios seleccionables (persistente en localStorage)
- Web pública: botón flotante que sugiere instalar Dark Reader

---

## Base de datos (20 tablas)

- `psychologists` — único usuario del sistema
- `settings` — configuración clave-valor
- `services`, `specialties`, `plans` — contenido web pública
- `availability`, `availability_configs`, `vacation_periods` — disponibilidad
- `patients`, `appointments` — pacientes y citas
- `clinical_histories`, `clinical_history_files` — historias clínicas
- `blog_categories`, `blog_posts` — blog
- `faqs` — preguntas frecuentes
- `themes` — temas visuales
- `gallery_images` — galería de imágenes
- `social_networks` — redes sociales
- `public_phrases` — frases personalizables
- `data_protection_templates` — plantilla protección de datos
- `notifications` — notificaciones del dashboard

---

## Estructura del proyecto

```
psicocms/
├── app/
│   ├── Http/Controllers/     ← Controladores (Dashboard, Public, Auth, Install)
│   ├── Http/Middleware/       ← CheckInstallation, RedirectIfInstalled, InjectThemeData
│   ├── Http/Requests/         ← Validación de formularios
│   ├── Models/                ← 21 modelos Eloquent
│   ├── Services/              ← AvailabilityService, AppointmentService, SettingsService, PdfService
│   └── Mail/                  ← NewAppointmentNotification
├── database/migrations/       ← 21 migraciones
├── database/seeders/          ← Seeders con datos por defecto
├── resources/views/           ← Vistas Blade (dashboard/, public/, install/, auth/)
├── public/
│   ├── assets/                ← CSS, JS, fuentes, imágenes, vendor (Jodit, FullCalendar)
│   └── themes/                ← 5 temas visuales (CSS por tema)
├── routes/web.php             ← Todas las rutas
└── storage/                   ← Archivos subidos (fotos, PDFs, imágenes galería)
```

---

## Documentación complementaria

- [AGENTS.md](./AGENTS.md) — Especificación completa del proyecto
- [plan_implementacion.md](./plan_implementacion.md) — Plan de implementación detallado
- [tareas.md](./tareas.md) — Estado de tareas por fase
- [nuevas-funcionalidades.md](./nuevas-funcionalidades.md) — Funcionalidades añadidas post-implementación
- [ejemplo_fixes.md](./ejemplo_fixes.md) — Correcciones y mejoras realizadas
- [pre-instalacion.md](./pre-instalacion.md) — Instrucciones para la psicóloga
