# EquiSplitBack# EquiSplit — Frontend

Frontend web de **EquiSplit**, una plataforma para gestionar gastos compartidos y distribuir las responsabilidades financieras de manera proporcional a los ingresos de los participantes.

El proyecto está construido con **Angular** y está diseñado para consumir la API REST desarrollada con NestJS.

---

##  Estado del proyecto

**En desarrollo**

Actualmente EquiSplit se encuentra en fase de construcción. El desarrollo se está realizando de manera incremental mediante tareas pequeñas y verificables.

---

##  Objetivo

EquiSplit busca solucionar uno de los problemas comunes al compartir gastos: dividirlos siempre en partes iguales aunque los ingresos de las personas sean diferentes.

Ejemplo:

```text
Persona A
Ingresos: $3.000.000
Participación: 60%

Persona B
Ingresos: $2.000.000
Participación: 40%

Gasto compartido: $1.000.000

Persona A → $600.000
Persona B → $400.000
```

El frontend proporciona la interfaz necesaria para gestionar usuarios, grupos, ciclos, ingresos, gastos y liquidaciones.

---

##  Funcionalidades previstas

### Autenticación

- Registro de usuarios.
- Inicio de sesión.
- Gestión de sesión.
- Perfil de usuario.

### Grupos

- Crear grupos.
- Consultar grupos.
- Administrar participantes.
- Visualizar información del grupo.

### Ciclos

- Crear ciclos financieros.
- Consultar ciclos.
- Visualizar ciclos abiertos y cerrados.
- Consultar el resumen financiero de un ciclo.

### Ingresos

- Registrar ingresos.
- Diferenciar ingresos fijos y variables.
- Consultar ingresos por ciclo.
- Visualizar la participación proporcional.

### Gastos

- Registrar gastos.
- Seleccionar categoría.
- Indicar quién realizó el pago.
- Seleccionar participantes afectados.
- Consultar gastos del ciclo.

### Liquidación

- Visualizar obligaciones.
- Consultar saldos individuales.
- Visualizar quién debe pagar y quién debe recibir.
- Consultar la liquidación final del ciclo.

### Visualización financiera

- Resúmenes financieros.
- Estados de saldo.
- Gráficos y estadísticas.
- Historial de operaciones.

> Las funcionalidades se irán habilitando progresivamente durante el desarrollo.

---

##  Arquitectura

El frontend forma parte de una arquitectura separada por capas:

```text
┌─────────────────────────────┐
│          Angular            │
│          Frontend           │
│                             │
│  Components                 │
│  Pages                      │
│  Services                   │
│  Guards                     │
│  Interceptors               │
│  State                      │
└──────────────┬──────────────┘
               │
               │ HTTP / REST
               ▼
┌─────────────────────────────┐
│          NestJS             │
│          Backend            │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│        PostgreSQL           │
│            Neon             │
└─────────────────────────────┘
```

Infraestructura prevista:

```text
Angular  → Vercel
NestJS   → Railway
Postgres → Neon
Código   → Git
```

---

##  Tecnologías

- Angular
- TypeScript
- HTML5
- CSS / SCSS
- RxJS
- Angular Router
- Angular Forms
- API REST
- Git

Las tecnologías adicionales se incorporarán únicamente cuando aporten valor al proyecto.

---

##  Requisitos

Para ejecutar el proyecto localmente necesitas:

- Node.js
- npm
- Angular CLI
- Git

Puedes comprobar las versiones instaladas con:

```bash
node --version
npm --version
ng version
git --version
```

---

##  Instalación

Clona el repositorio:

```bash
git clone <URL_DEL_REPOSITORIO>
```

Entra al proyecto:

```bash
cd equisplit-front
```

Instala las dependencias:

```bash
npm install
```

Inicia el servidor de desarrollo:

```bash
npm start
```

La aplicación estará disponible normalmente en:

```text
http://localhost:4200
```

También puedes ejecutar Angular directamente:

```bash
ng serve
```

---

##  Variables de entorno

El frontend necesita conocer la URL de la API de EquiSplit.

La configuración debe mantenerse fuera del código fuente siempre que corresponda al entorno.

Ejemplo conceptual:

```text
API_URL=http://localhost:3000
```

Para producción:

```text
API_URL=<URL_DEL_BACKEND>
```

Las credenciales o secretos privados nunca deben almacenarse en el repositorio.

---

##  Estructura prevista

La estructura podrá evolucionar a medida que avance el proyecto, pero inicialmente se seguirá una organización orientada por funcionalidades:

```text
src/
├── app/
│   ├── core/
│   │   ├── guards/
│   │   ├── interceptors/
│   │   ├── services/
│   │   └── models/
│   │
│   ├── shared/
│   │   ├── components/
│   │   ├── pipes/
│   │   └── directives/
│   │
│   ├── features/
│   │   ├── auth/
│   │   ├── dashboard/
│   │   ├── groups/
│   │   ├── cycles/
│   │   ├── incomes/
│   │   ├── expenses/
│   │   └── settlement/
│   │
│   ├── app.routes.ts
│   └── app.config.ts
│
├── assets/
└── styles/
```

La estructura definitiva dependerá de las decisiones tomadas durante la implementación.

---

##  Autenticación

El frontend utilizará autenticación basada en JWT proporcionada por el backend.

El flujo esperado será:

```text
Login
  ↓
Backend valida credenciales
  ↓
JWT
  ↓
Frontend mantiene sesión
  ↓
Interceptor agrega token
  ↓
Requests autenticados
```

Las rutas privadas estarán protegidas mediante guards.

---

##  Comunicación con el backend

El frontend se comunicará con la API REST de EquiSplit.

Ejemplo conceptual:

```text
Angular
   │
   ├── POST /auth/login
   ├── GET  /users/me
   ├── GET  /groups/mine
   ├── GET  /groups/:id/cycles
   ├── POST /cycles
   ├── POST /incomes
   ├── POST /expenses
   └── GET  /cycles/:id/settlement
```

Los endpoints definitivos se establecerán durante el desarrollo del backend.

---

##  Lógica financiera

El frontend **no será la fuente de verdad de los cálculos financieros**.

Los valores como:

- porcentajes;
- obligaciones;
- saldos;
- liquidaciones;

serán calculados y validados por el backend.

El frontend se encargará principalmente de:

- solicitar operaciones;
- mostrar resultados;
- validar datos de entrada;
- representar visualmente la información.

---

##  Testing

El proyecto contará con pruebas para las funcionalidades principales del frontend.

Las pruebas buscarán cubrir especialmente:

- componentes;
- servicios;
- guards;
- interceptors;
- formularios;
- flujos de autenticación;
- interacción con la API.

Las reglas financieras críticas se validarán principalmente en el backend.

---

##  Build de producción

Para generar una compilación de producción:

```bash
npm run build
```

El resultado podrá desplegarse posteriormente en Vercel.

---

##  Deployment

El frontend está diseñado para desplegarse en **Vercel**.

Flujo previsto:

```text
Git
 ↓
Push
 ↓
Vercel
 ↓
Build Angular
 ↓
Deploy
```

La configuración de producción utilizará la URL pública del backend desplegado en Railway.

---

##  Flujo de desarrollo

El proyecto seguirá un flujo basado en Git.

Ramas principales:

```text
main
develop
```

Para nuevas funcionalidades:

```text
feature/<nombre>
```

Para correcciones:

```text
fix/<nombre>
```

Flujo general:

```text
develop
   ↓
feature/*
   ↓
Pull Request
   ↓
develop
   ↓
main
```

---

##  Convenciones

Se busca mantener:

- componentes pequeños y reutilizables;
- separación de responsabilidades;
- servicios enfocados;
- nombres descriptivos;
- código tipado con TypeScript;
- validación de formularios;
- manejo consistente de errores;
- evitar lógica financiera duplicada en el frontend.

---

##  Documentación

La documentación general del proyecto incluye:

```text
docs/
├── vision.md
└── business-rules.md
```

### `vision.md`

Define:

- propósito;
- problema;
- usuarios objetivo;
- MVP;
- alcance;
- arquitectura general.

### `business-rules.md`

Define:

- reglas financieras;
- distribución proporcional;
- gastos parciales;
- saldos;
- redondeos;
- liquidación;
- invariantes del sistema.

---

##  Roadmap

El proyecto se desarrolla mediante tareas identificadas con códigos `EQUI-*`.

Las primeras etapas incluyen:

```text
EQUI-001  → Alcance inicial
EQUI-002  → Reglas de negocio
EQUI-003  → Repositorio
EQUI-004  → Flujo Git
EQUI-005  → Backend
EQUI-006  → Frontend
...
```

El backlog completo contiene las tareas necesarias para llevar EquiSplit desde su estructura inicial hasta un producto desplegado y preparado para portafolio.

---

##  Capturas

Esta sección se actualizará a medida que la interfaz alcance versiones visualmente presentables.

<!--
Agregar aquí screenshots del:

- Login
- Dashboard
- Grupo
- Ciclo
- Gastos
- Ingresos
- Liquidación
-->

---

##  Proyecto

**EquiSplit** es un proyecto personal enfocado en aplicar y demostrar conocimientos de desarrollo Full-Stack, arquitectura de aplicaciones web, manejo de APIs, PostgreSQL, autenticación, reglas de negocio, testing y despliegue en la nube.

---
