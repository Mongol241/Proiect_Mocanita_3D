# 🚂 Mocănița 3D – OpenGL Classic Simulation

---

## 🎮 Overview
This project is a desktop application that simulates a traditional Romanian narrow-gauge steam locomotive, known as a **Mocănița**, in a 3D environment. Built in C++ using legacy **OpenGL (GL, GLU, GLAUX)** tech, it provides an interactive viewing experience, geometric rendering, and real-time physics approximations (such as shadow mapping and component animation) based on fundamental computer graphics concepts.

---

## 🧠 About the Project
The project demonstrates:

* 📐 **Procedural 3D Modeling** (building complex objects out of basic geometric primitives)
* 💡 **Lighting & Shading** (configuring light sources and material properties)
* 👤 **Mathematical Shadow Matrix** (calculating planar shadow projections)
* 🔄 **Real-Time Animation** (managing independent movement of sub-components)
* ⌨️ **User Interaction** (keyboard events and an active `Idle` refresh loop)

---

## 🔥 Features

### 🚂 Detailed Modeling
* Proportional main chassis block
* Driver's cabin and smoke stack textured via solid coloring
* Cylindrical boiler featuring a custom front cap (`gluDisk`)
* 6 individual wheels (3 on the left side, 3 on the right side)

### ⚙️ Mechanics & Animation
* **Continuous Rotation:** The train's wheels spin independently and automatically to simulate movement.
* **Adjustable Scene Angle:** The user can rotate the entire environment to admire the locomotive from any perspective.

### 🌑 Realistic Planar Shadows
* Dynamic shadow casting on the ground plane based on the light source position (`lightPos`) and the ground vector (`groundPlane`).
* Temporary disabling of lighting and depth testing (`GL_DEPTH_TEST`) to render perfectly flat, dark mathematical silhouettes.

### 🖥️ Graphical Interface & Control (GLAUX)
* Native window rendering with Double Buffering (`AUX_DOUBLE`) support for smooth, tear-free animations.
* Key Bindings:
  * `X Key` ➔ Rotates the scene by 15 degrees to shift the camera perspective.

---


## ⚙️ How It Works

### 📐 Shadow Projection System (`ShadowMatrix`)
The shadow is not a texture map, but rather a geometric clone of the train flattened onto the floor using linear algebra. The function calculates the following dot product:
$$\text{dot} = \text{plane}[0] \cdot \text{light}[0] + \text{plane}[1] \cdot \text{light}[1] + \text{plane}[2] \cdot \text{light}[2] + \text{plane}[3] \cdot \text{light}[3]$$
This value alters the current modelview matrix (`glMultMatrixf`), flattening and rendering the train's geometry completely black directly onto the ground's $Y$ coordinate.

### 🔄 Application Flow (Game Loop)
1. Display mode initialization (RGB, Depth Buffer, Double Buffer).
2. Ambient and diffuse lighting setup (`GL_LIGHT0`).
3. Execution of the `IdleFunction`: the wheel rotation angle increments by $8^\circ$ every 30 milliseconds.
4. Buffers are cleared, and the scene is redrawn (`display`).

---

## 🧠 Concepts Used

* **Fixed-Function Graphical Pipeline:** Heavy use of the matrix stack (`glPushMatrix`, `glPopMatrix`) for local coordinate transformations.
* **Hierarchical Modeling:** Component animation (the wheels) is strictly dependent on the main parent body's positioning (the chassis).
* **Event/Time-Driven Animation:** Utilizing GLAUX-specific handler callbacks (`auxIdleFunc`, `auxKeyFunc`).

---

## 📌 Notes
* This project was developed for educational purposes to highlight the underlying math of vintage 3D rendering pipelines.
* The GLAUX library is deprecated/legacy software, used here specifically to simplify window setup and handle base 3D primitives.

---

## 👨‍💻 Author
* **Virlan Stefan** – *Student / Developer*

---
