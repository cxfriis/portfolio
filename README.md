# Portfolio

Repository for showcasing personal projects.

<!-- TOC start (generated with https://github.com/derlin/bitdowntoc) -->

* [Mobile Game Development](#mobile-game-development)
    + [Demo Videos](#demo-videos)
    + [Technology Stack](#technology-stack)
        - [Programming Languages](#programming-languages)
        - [Game Framework](#game-framework)
        - [Rendering & Graphics](#rendering--graphics)
        - [Game Architecture & Entity Management](#game-architecture--entity-management)
        - [Performance Monitoring & Telemetry](#performance-monitoring--telemetry)
        - [Build System & Dependency Management](#build-system--dependency-management)
        - [Platform Support](#platform-support)
    + [Design Patterns & Justifications](#design-patterns--justifications)
        - [1. Entity Component System (ECS)](#1-entity-component-system-ecs)
        - [2. Event-Driven UI Updates](#2-event-driven-ui-updates)
        - [3. Factory & Repository Pattern for Game Assets](#3-factory--repository-pattern-for-game-assets)
        - [4. Universal Registry for Service Management](#4-universal-registry-for-service-management)
        - [5. Profiling & Performance Optimizations](#5-profiling--performance-optimizations)
    + [Conclusion](#conclusion)

<!-- TOC end -->

## Mobile Game Development

Developing a game and engine on top of LibGDX, using own original artwork, with the intention of submitting to the Google Play Store.

### Demo Videos

* [Gameplay Demo](https://www.canva.com/design/DAGgelagUsk/DnFaHVyq1qRj_Rvzj1qJzQ/watch?utm_content=DAGgelagUsk&utm_campaign=celebratory_first_publish&utm_medium=link2&utm_source=editor_celebratory_first_publish)
* [Metrics Video](https://www.canva.com/design/DAGgfrJDeSU/d-gNBf7jI4RcIsCKAXchjA/watch?utm_content=DAGgfrJDeSU&utm_campaign=designshare&utm_medium=link2&utm_source=uniquelinks&utlId=hbc20bfd6a4)

### Technology Stack

#### Programming Languages

- **Java & Python**: Java is used for the engine, enabling cross-platform compatibility, while Python is leveraged for scripting to create new assets such as level metadata.

#### Game Framework

- **LibGDX**: Chosen for its lightweight nature, strong community support, and cross-platform capabilities. It provides essential game development utilities like rendering, asset management, and input handling.

#### Rendering & Graphics

- **Scene2D**: Used for UI rendering, providing an efficient way to manage hierarchical layouts and event-driven UI interactions.

- **OpenGL Shaders (GLSL)**: Used for custom rendering effects such as brightness adjustments and grayscale transformations.

- **Texture Atlases**: To optimize rendering performance, textures are dynamically packed into atlases to minimize texture switches during rendering.

- **FrameBuffer (FBOs)**: Utilized for off-screen rendering to capture frames for effects like screenshots and post-processing.

#### Game Architecture & Entity Management

- **Ashley ECS (Entity Component System)**: Used to manage game entities efficiently. It promotes separation of concerns by decoupling logic and data, allowing high-performance entity processing.

- **Entity Grouping for Rendering**: Entities are grouped into Background, Midground, and Foreground layers to reduce texture switches and optimize rendering efficiency.

#### Performance Monitoring & Telemetry

- **Micrometer**: Provides instrumentation for game performance metrics.

- **Prometheus & Grafana**: Used to scrape and visualize metrics such as FPS, rendering time, and memory usage in real time.

- **NanoHTTPD**: Lightweight HTTP server used for exposing the metrics endpoint without the overhead of a full web framework.

#### Build System & Dependency Management

- **Gradle**: Used for dependency management and automated builds, ensuring efficient project structure and easy integration of third-party libraries.

#### Platform Support

- **Android, iOS, Desktop**: The game is designed for both mobile and desktop platforms, with platform-specific optimizations to handle rendering, input, and performance constraints.

### Design Patterns & Justifications

#### 1. Entity Component System (ECS)

- **Justification**: Improves modularity and flexibility by separating entity data (components) from behavior (systems). This approach enhances maintainability and performance by processing components in batches.

#### 2. Event-Driven UI Updates

- **Justification**: Instead of allowing game entities to hold UI references, a decoupled event-driven approach is used. This prevents UI elements from persisting across screens and avoids unintended interactions when switching game states.

#### 3. Factory & Repository Pattern for Game Assets

- **Factory Pattern**: Used for creating game objects dynamically, ensuring entities are instantiated consistently.

- **Repository Pattern**: Used for managing shared resources like textures, sounds, and shaders to avoid redundant asset loading.

#### 4. Universal Registry for Service Management

- **Justification**: A central registry holds references to Factories, Repositories, and Services, allowing various game systems to retrieve necessary dependencies without tight coupling.

#### 5. Profiling & Performance Optimizations

- **Batching Render Calls**: To minimize GPU overhead, SpriteBatch is used efficiently by reducing `batch.flush()` calls through texture atlases and render order optimization.

- **Frame Timing Metrics**: FPS and frame render times are tracked using Prometheus to identify and address bottlenecks.

### Conclusion

This game is built with a focus on performance, maintainability, and scalability. By leveraging an Entity Component System, optimized rendering techniques, and a robust monitoring stack, the game achieves high efficiency while remaining adaptable for future expansion.