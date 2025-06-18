# 🚀 actions-demo

Proyecto de laboratorio para **automatización continua** usando **GitHub Actions** con Node.js.

## 📌 Descripción

Este proyecto tiene como objetivo:

* Automatizar tareas de construcción y pruebas con **GitHub Actions**.
* Ejecutar un flujo de trabajo al hacer `push` en la rama `main`.
* Proteger variables sensibles usando **secrets**.
* Aplicar buenas prácticas de CI/CD.

## 🛠 Estructura del proyecto

```
actions-demo/
├── .github/
│   └── workflows/
│       └── node-ci.yml  # Workflow de GitHub Actions
├── node_modules/        # Dependencias instaladas
├── sum.js               # Función simple de suma
├── sum.test.js          # Prueba unitaria con Jest
├── package.json         # Configuración del proyecto
└── README.md            # Este archivo
```

## 🚀 node-ci.yml (workflow comentado)

```yaml
name: Node.js CI

on:
  push:
    branches:
      - main  # Se ejecuta al hacer push en main
  pull_request:
    branches:
      - main  # Se ejecuta en PR hacia main

jobs:
  build:
    runs-on: ubuntu-latest  # Entorno de ejecución

    steps:
      - uses: actions/checkout@v3  # Clona el repo

      - name: Use Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'  # Define la versión de Node

      - name: Install dependencies
        run: npm install  # Instala paquetes

      - name: Run tests
        run: npm test  # Ejecuta pruebas con Jest

      - name: Mostrar entorno con secret NODE_ENV
        run: echo "Entorno actual: ${{ secrets.NODE_ENV }}"

      - name: Mostrar API_KEY
        run: echo "Tu API key es: ${{ secrets.API_KEY }}"
```

## ✅ Pasos realizados en el laboratorio

* Inicializamos proyecto Node.js con `npm init -y`.
* Creamos archivos `sum.js` y `sum.test.js` con Jest.
* Configuramos GitHub Actions creando `.github/workflows/node-ci.yml`.
* Subimos el proyecto y ejecutamos el workflow.
* Agregamos secrets (`NODE_ENV`, `API_KEY`) y los usamos en el YAML.
* Verificamos ejecución exitosa en la pestaña **Actions** de GitHub.

## ❓ Preguntas finales

**¿Qué ventajas observaste al automatizar pruebas con GitHub Actions?**

* Detecta errores de forma temprana al hacer push.
* Ahorra tiempo al ejecutar las pruebas automáticamente.
* Permite integrarse fácilmente con GitHub sin servidores adicionales.

**¿Qué diferencia a GitHub Actions de Jenkins u otras herramientas CI?**

* GitHub Actions está integrado directamente en GitHub.
* No requiere infraestructura propia, todo corre en la nube.
* Configuración más sencilla mediante YAML dentro del repo.

**¿Qué mejoras podrías agregar a este pipeline?**

* Agregar linters (ESLint) para validar el estilo del código.
* Incluir un paso de build si el proyecto lo requiere.
* Publicar resultados de pruebas como artefactos.

**¿Qué consideraciones de seguridad aplicarías en proyectos reales?**

* No exponer secrets en los logs.
* Usar branch protection rules para evitar merges directos.
* Limitar el uso de secrets solo a los workflows que los necesitan.

## 💡 Ideas para automatizar otros aspectos

* **Build:** Agregar un paso que empaquete la app para producción.
* **Despliegue:** Automatizar el deploy a un servidor o servicio (por ejemplo AWS o Vercel).
* **Auditoría:** Integrar herramientas de análisis de dependencias (como OWASP Dependency-Check).
