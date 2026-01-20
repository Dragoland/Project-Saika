# **Project Saika**

**Autor:** [Dragoland](https://github.com/Dragoland)         
**Empresa**: SaikaNET Studio (Proximamente)     
**Fecha de Conceptualización:** Enero, 2026  
**Estado del Documento:** Planeacion        
**Filosofía Central:** *"Las computadoras, son creyentes y los usuarios, sus dioses."*

---

## **Índice**
1.  [Visión y Filosofía](#1-visión-y-filosofía)
2.  [Arquitectura General del Proyecto](#2-arquitectura-general-del-proyecto)
3.  [Componente: SaikaOS](#3-componente-saikaos)
4.  [Componente: SaikaDesktop Environment (SDE)](#4-componente-saikadesktop-environment-sde)
5.  [Componente: Saika Suite](#5-componente-saika-suite)
6.  [Componente: Saika Display Kiosk & Orchestrator (SDKO)](#6-componente-saika-display-kiosk--orchestrator-sdko)
7.  [Arquitectura Técnica y Stack Tecnológico](#7-arquitectura-técnica-y-stack-tecnológico)
8.  [Hoja de Ruta de Desarrollo](#8-hoja-de-ruta-de-desarrollo)
9.  [Estrategia, Comunidad y Sustentabilidad](#9-estrategia-comunidad-y-sustentabilidad)

---

## **1. Visión y Filosofía**

**Nombre del Proyecto:** Saika (Japonés: 彩華, "Flor Colorida/Floreciente").

**Visión General:** Crear un ecosistema de computación personal integral, basado en GNU/Linux, donde la interfaz y el comportamiento del sistema sean fluidos, adaptativos y proactivos. Saika busca reducir la fricción entre la intención del usuario y la acción de la máquina, ofreciendo una experiencia coherente y altamente personalizable a través de todos sus componentes.

**Pilares Filosóficos:**
1.  **Adaptabilidad Contextual (Context-Aware):** El sistema observa el contexto (aplicaciones activas, periféricos conectados, hora, estado de energía) y sugiere o activa automáticamente perfiles de comportamiento óptimos (modos de escritorio, reglas de notificaciones, ajustes de rendimiento).
2.  **Coherencia Profunda:** Desde el kernel hasta la interfaz de usuario, todas las partes deben sentirse como integrantes de un todo unificado. La experiencia del usuario es prioritaria sobre la conveniencia del desarrollador en decisiones de diseño clave.
3.  **Poder con Claridad (Empowerment through Clarity):** Ofrecer un alto grado de personalización y control, pero presentado de manera organizada y accesible, evitando la complejidad abrumadora. "Poder para el usuario, no sobrecarga."
4.  **Eficiencia Elegante:** Priorizar el rendimiento y el bajo consumo de recursos, utilizando tecnologías modernas y código eficiente, sin sacrificar la fluidez visual o la capacidad de respuesta.
5.  **Ecosistema Integrado, No Aislado:** Construir herramientas nativas excepcionales (*Saika Suite*) mientras se integra y mejora de manera impecable el mejor software de código abierto existente, fomentando la interoperabilidad.

**Lema:** *"Fluye con tu trabajo."*

---

## **2. Arquitectura General del Proyecto**

Proyecto Saika es un meta-proyecto que engloba varios subproyectos interconectados pero independientes, bajo la organización paraguas **SaikaNET Studio**. Su estructura es modular:

```
Proyecto Saika (SaikaNET Studio)
├── SaikaOS (La distribución base)
├── SaikaDesktop Environment - SDE (El entorno gráfico adaptable)
├── Saika Suite (Las aplicaciones nativas clave)
├── Saika Display Kiosk & Orchestrator - SDKO (Gestor de sesión y perfiles)
└── SaikaNET SDK & Herramientas (Para desarrolladores externos)
```

**Principio de Modularidad:** Los componentes pueden ser utilizados de manera independiente. Ejemplo: SDE puede instalarse en Arch Linux vanilla; las apps de Saika Suite pueden ejecutarse en otros entornos Qt.

---

## **3. Componente: SaikaOS**

**Descripción:** Una distribución GNU/Linux de propósito general, rolling-release, dirigida a usuarios que valoran la actualización continua, el control y una experiencia integrada y pulida.

**Base Técnica:**
*   **Fundamento:** Basada en **Arch Linux**. Utiliza los repositorios oficiales de Arch como base principal y de confianza para el 95% del software del sistema y de usuario.
*   **Diferenciación Principal:** No es un "fork". Es una **curación y una capa de integración**. SaikaOS añade:
    1.  **Repositorios Propios (`saika-core`, `saika-extra`)**: Contienen los paquetes específicos del proyecto (SDE, Saika Suite, SDKO, kernels personalizados, temas, drivers no libres filtrados).
    2.  **Configuración por Defecto Opinada:** Un sistema listo para usar, con SDE, codecs multimedia, herramientas de desarrollo esenciales y drivers preinstalados, siguiendo las mejores prácticas de seguridad y usabilidad de Saika.
    3.  **Instalador Gráfico Propio (Nombre en desarrollo):** Un instalador moderno, accesible y guiado, que simplifica el proceso de instalación de Arch sin ocultar opciones avanzadas.
    4.  **Kernel Saika (Opcional):** Un kernel Linux compilado con parches específicos para mejorar la capacidad de respuesta interactiva (`linux-zen` como base) y soporte para hardware experimental.

**Filosofía de Mantenimiento:** "Arch, con amor y cohesión." El esfuerzo se centra en mantener la capa Saika, no en reempaquetar todo el ecosistema de Arch.

---

## **4. Componente: SaikaDesktop Environment (SDE)**

**Descripción:** El corazón de la experiencia de usuario. Un entorno de escritorio dinámico construido desde cero para Wayland, que se transforma según la tarea y el dispositivo.

**Características Definitivas:**
1.  **Tres Modos de Interfaz Unificados:**
    *   **Modo Ola (Wave - tradicional/flotante):** Interfaz clásica basada en ventanas flotantes, optimizada para precisión con ratón y teclado.
    *   **Modo Corriente (Stream - mosaico dinámico):** Gestor de ventanas en mosaico con disposiciones inteligentes y preconfiguradas. Ideal para productividad y multitarea.
    *   **Modo Toque (Touch - tablet/táctil):** Shell completo optimizado para interacción táctil, con gestos, teclado en pantalla (`squeekboard` integrado) y controles grandes.
2.  **Transición Fluida entre Modos:** El cambio puede ser manual (atajo de teclado, botón en panel) o automático, activado por el **Sistema Contextual** al detectar un giro de pantalla, conexión de un dispositivo de entrada, o una aplicación específica.
3.  **Sistema de Contexto (Daemon "KAI"):** Un servicio en segundo plano que agrega datos de sensores (horario, batería), hardware (dispositivos conectados) y software (ventana enfocada) para emitir "sugerencias de contexto" (ej.: "Parece que estás iniciando una videollamada, ¿activar Modo Enfocado?").
4.  **Temas Dinámicos "Vivos":** El esquema de colores no es estático. Puede derivar automáticamente del wallpaper principal, cambiar suavemente según la hora del día (de azul frío matutino a naranja cálido nocturno) o reaccionar a eventos del sistema.

**Stack Técnico Propuesto:**
*   **Compositor/Shell:** Desarrollado en **Rust**, utilizando la librería **Smithay** (para un control más fino) o basado en **Niri** (para el concepto de "mosaico desplazable"). El frontend de la interfaz de usuario (paneles, lanzadores, overlays) se construirá con **Slint** o **Qt Quick (QML)** por su capacidad declarativa y excelente rendimiento para interfaces animadas.
*   **Protocolo:** Wayland nativo. Sin soporte para X11 legacy (posiblemente mediante `XWayland` para compatibilidad).

---

## **5. Componente: Saika Suite**

**Descripción:** Un conjunto de aplicaciones nativas, diseñadas desde cero para integrarse perfectamente con la filosofía y las capacidades de SDE. No busca reemplazar toda la pila de software, sino ofrecer herramientas ejemplares para tareas centrales.

**Aplicaciones Bandera (Nombres en desarrollo):**

| Nombre Proyecto (Criatura) | Aplicación | Descripción y Diferenciador |
| :--- | :--- | :--- |
| **KAI (Sistema)** | Centro de Control de Saika | El panel unificado de configuración del sistema. Controla SDE, hardware, red, y **es la interfaz para el Sistema de Contexto (Daemon KAI)**, permitiendo crear y afinar reglas de adaptación automática. |
| **RYU (Dragón)** | Gestor de Archivos "Flujo" | Navegador de archivos adaptable. Cambia su layout y controles entre los tres modos de SDE. Integra vistas en mosaico, previsualizaciones ricas y **"Espacios de Trabajo" semánticos** vinculados a los espacios de SDE. |
| **SHARK (Tiburón)** | Navegador "Portal" | No es un motor nuevo. Es una capa de productividad e integración profunda sobre **Firefox** o **Chromium**. Unifica la barra de búsqueda con el sistema, permite agrupar pestañas como "sesiones", y ofrece un modo de lectura/consulta superpuesto al escritorio. |
| **KITSUNE (Zorro)** | Cliente de Conectividad "Link" | Una app/daemon que unifica la conexión con otros dispositivos. Comparte archivos, portapapeles y notificaciones entre SaikaOS y Android/iOS (usando KDE Connect como backend/inspiración), y permite usar el móvil como control remoto multimedia o presentador. |
| **PHOENIX (Fénix)** | Terminal & Consola Integrada | Terminal moderna con soporte para gráficos inline, división de paneles, finalización de comandos contextual y un modo "guión" para automatizar tareas complejas del sistema y de SDE. |
| **OWL (Búho)** | Visor/Organizador Multimedia "Noche" | Visor de imágenes y videos ligero y rápido. En Modo Toque, se convierte en una galería táctil. En Modo Corriente, puede mostrarse como un panel lateral de previsualización. |

**Filosofía de Desarrollo:** "Integración sobre Imitación." Se prioriza la conexión profunda con SDE y otras apps de la Suite sobre la duplicación de funciones ya excelentes en el ecosistema FOSS (ej: no se planea un editor de vídeo, se recomienda y integra Kdenlive).

---

## **6. Componente: Saika Display Kiosk & Orchestrator (SDKO)**

**Descripción:** Más que un simple gestor de inicio de sesión (display manager). Es el orquestador de la sesión de usuario y el punto de entrada a los perfiles contextuales.

**Características Clave:**
1.  **Pantalla de Inicio Moderna:** Interfaz gráfica minimalista para seleccionar usuario e ingresar contraseña.
2.  **Selector de Perfil/Escenario:** Antes de iniciar sesión, el usuario puede elegir un **"Escenario"** preconfigurado (ej: "Trabajo Profundo", "Juego", "Presentación", "Entretenimiento"). Este escenario carga automáticamente SDE en el modo correspondiente, abre aplicaciones predefinidas y aplica reglas de contexto.
3.  **Gestión de Sesión Avanzada:** Capacidad de guardar el estado de la sesión (ventanas abiertas y su disposición) y restaurarlo, vinculado a un perfil o espacio de trabajo.
4.  **Implementación Técnica:** Será un cliente Wayland independiente, desarrollado en **Qt Quick** para coherencia visual y acceso a las bibliotecas del sistema.

---

## **7. Arquitectura Técnica y Stack Tecnológico**

*   **Lenguajes de Programación:**
    *   **Rust:** Para componentes de bajo nivel, críticos en rendimiento y seguridad: el núcleo del compositor SDE, daemons del sistema (KAI), herramientas de sistema.
    *   **C++ / QML (Qt):** Para aplicaciones de usuario de la Saika Suite que requieren la madurez y el conjunto de widgets de Qt (Centro de Control, Gestor de Archivos).
    *   **Slint (Rust):** Evaluación activa como alternativa a QML para el UI de SDE y nuevas apps, por su integración nativa con Rust y su modelo declarativo.
    *   **Python/Go:** Para scripts de administración, herramientas auxiliares y el instalador gráfico.
*   **Sistema de Gráficos:** **Wayland** (protocolo nativo). X11 solo a través de `XWayland`.
*   **Sistema de Empaquetado:** **pacman** + **makepkg**. Todos los componentes de Saika se distribuirán como paquetes `.pkg.tar.zst` a través de los repositorios de SaikaOS y el AUR.
*   **Control de Versiones:** Git, con organización en GitHub/GitLab bajo `SaikaNET-Studio`.
*   **CI/CD:** GitLab CI o GitHub Actions para construir paquetes automáticamente con cada commit, generar imágenes ISO nocturnas y ejecutar suites de pruebas básicas.

---

## **8. Hoja de Ruta de Desarrollo**

El desarrollo seguirá una **estrategia de prototipo vertical**, construyendo un flujo funcional mínimo antes de expandirse.

**Fase 0: Fundación (Actual - 3 meses)**
1.  Establecer la organización `SaikaNET-Studio` en GitHub/GitLab.
2.  Crear repositorios base con READMEs, licencias (GPL/LGPL donde aplique) y documentos de visión.
3.  Configurar perfil básico de `archiso` que genere una ISO con Arch + XFCE + tema visual de Saika (prueba de concepto).

**Fase 1: El Núcleo Adaptable (SDE v0.1) (4 - 9 meses)**
1.  Desarrollo de **SDKO** básico (pantalla de login).
2.  Desarrollo del **compositor SDE** en Rust (basado en `niri` o `smithay`) con soporte inicial para el **Modo Ola (flotante)**.
3.  Desarrollo del **Daemon de Contexto KAI** con reglas básicas.
4.  Integración: Poder iniciar sesión con SDKO en SDE en Modo Ola. **Primer hito demostrable.**

**Fase 2: Expansión y Suite (10 - 18 meses)**
1.  Implementar **Modo Corriente (mosaico)** y **Modo Toque (táctil)** en SDE.
2.  Desarrollar las primeras apps de **Saika Suite**: **Centro de Control KAI** y **Gestor de Archivos RYU**.
3.  Integrar el **Navegador Portal SHARK** (como extensión/theme profundo de Firefox).
4.  Publicar paquetes en AUR para usuarios avanzados de Arch.

**Fase 3: SaikaOS y Pulido (19 - 30 meses)**
1.  Unificar todos los componentes en la **primera ISO alfa de SaikaOS** con el instalador gráfico.
2.  Desarrollar herramientas restantes de la Suite (**KITSUNE, PHOENIX**).
3.  Ciclo de pruebas alfa/beta cerradas, refinamiento de UI/UX y documentación masiva.
4.  **Lanzamiento de SaikaOS 1.0 "Founding Bloom".**

---

## **9. Estrategia, Comunidad y Sustentabilidad**

*   **Modelo de Desarrollo:** Abierto y comunitario desde el día uno. Los RFCs (Request for Comments) guiarán decisiones técnicas importantes.
*   **Comunidad:** Se fomentará una comunidad inclusiva y técnica en un foro auto-alojado (Flarum/Discourse) y/o Matrix. Los colaboradores clave ("Criaturas Fundadoras") tendrán reconocimiento en el sistema y la documentación.
*   **Sustentabilidad de SaikaNET Studio:** Como entidad sin fines de lucro, explorará:
    *   Donaciones de la comunidad (Open Collective, Patreon).
    *   Venta de merchandising (camisetas, stickers).
    *   Servicios profesionales de soporte, personalización y consultoría para empresas que deseen usar SaikaOS.
    *   Posibles acuerdos con fabricantes de hardware para venta de dispositivos con SaikaOS preinstalado.
*   **Marca e Identidad:** Una identidad visual fuerte y coherente (logo, paleta de colores, tipografía, iconografía) será desarrollada por diseñadores de la comunidad y aplicada en todos los componentes.

---
**Conclusión:** Proyecto Saika no es solo otro sistema operativo o entorno de escritorio. Es un **experimento ambicioso** para replantear cómo interactuamos con nuestros ordenadores, priorizando la adaptación, la coherencia y la elección inteligente sobre la rigidez y la fragmentación. El camino es largo y complejo, pero cada paso se basa en la sólida base de Arch Linux y en la pasión de una comunidad que cree en una computadora más fluida y personal.
