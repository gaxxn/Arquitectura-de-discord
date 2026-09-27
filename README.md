
# Arquitectura de Discord

![Discord](https://img.shields.io/badge/Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white)
![Electron](https://img.shields.io/badge/Electron-47848F?style=for-the-badge&logo=electron&logoColor=white)
![Elixir](https://img.shields.io/badge/Elixir-4B275F?style=for-the-badge&logo=elixir&logoColor=white)
![Rust](https://img.shields.io/badge/Rust-000000?style=for-the-badge&logo=rust&logoColor=white)
![ScyllaDB](https://img.shields.io/badge/ScyllaDB-4A90E2?style=for-the-badge&logo=scylladb&logoColor=white)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)
![React Native](https://img.shields.io/badge/React_Native-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)

## Discord está construido en electron


<img width="980" height="150" alt="656" src="https://github.com/user-attachments/assets/9778df63-9786-47b6-b726-7c5f89b74725" />



Electron es un framework de código abierto diseñado para empaquetar aplicaciones web dentro de un entorno ejecutable en sistemas operativos de escritorio como Windows, macOS y Linux. Su funcionamiento interno se apoya en dos pilares fundamentales, **Chromium**, que actúa como motor de renderizado para desplegar la interfaz gráfica de usuario, y **Node.js**, que proporciona acceso directo al sistema de archivos y recursos del sistema operativo local.

Para Discord, Electron representa la solución central que permite mantener una única base de código entre la aplicación web y el cliente de escritorio. Esto agiliza de forma drástica el despliegue de nuevas funcionalidades de manera simultánea en todas las plataformas. Sin embargo, en el entorno móvil (iOS y Android), empaquetar una instancia de Chromium resultaría ineficiente debido a las restricciones de batería y memoria RAM. Por esta razón, las aplicaciones móviles de Discord están construidas sobre **React Native**, compartiendo la lógica de negocio basada en TypeScript pero renderizando componentes nativos del sistema operativo.

Tanto en escritorio como en el móvil, las operaciones que requieren ese alto rendimiento —como la codificación de audio en tiempo real con Opus, la cancelación de ruido y el cifrado de datos— se delegan a módulos nativos escritos en C++ y Rust. Estos módulos se vinculan directamente mediante Node-API en el escritorio y a través del Java Native Interface (JNI) o Objective-C Bridge en plataformas móviles, garantizando que el hilo principal donde corre la interfaz no sufra congelamientos durante transmisiones intensivas.

---

### Repositorios

> **Framework Electron**  
> https://github.com/electron/electron  
>
> **Motor React Native**  
> https://github.com/facebook/react-native  
>
> **Librería de Componentes Nativos (Node-API)**  
> https://github.com/nodejs/node-addon-api  

---

<details>
<summary><b>Especificaciones Técnicas del Pipeline de Renderizado</b></summary>

```text
+-------------------------------------------------------------------+
|                        DISCORD CLIENT LAYER                       |
+---------------------------------+---------------------------------+
|        Desktop (Electron)       |         Mobile (React Native)   |
|   Chromium Render + Node.js     |    Native iOS / Android Views   |
+---------------------------------+---------------------------------+
|                      Shared TypeScript Core                       |
+-------------------------------------------------------------------+
|                     Native C++ Audio / Voice Engine               |
+-------------------------------------------------------------------+
