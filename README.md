# Tetris 3D

![Screenshot (30)](https://user-images.githubusercontent.com/45245111/211423574-0422a1ee-5f54-4147-9164-7b69a56215f7.png)

A 3D implementation of the classic Tetris game built from scratch in C++ and OpenGL 3.3 Core Profile. The game features a 10x21 playfield framed by a RGB-gradient 3D cube border, next-piece preview, official Super Rotation System (SRS) wall-kick mechanics, multithreaded gravity and line clearing, FreeType HUD text rendering, and a 360-degree 3D skybox environment with a free-moving camera.

Developed for the Computer Graphics course at Universidade da Beira Interior (2022/2023).

---

## Features

* **3D OpenGL Rendering & Skybox:** All tetrominoes and board boundaries are rendered as textured 3D unit cubes inside a 6-face cubemap skybox with a movable 3D perspective camera.
* **Official SRS Rotation & Wall Kicks:** Implements official Tetris rotation rules around each tetromino center point, complete with Super Rotation System (SRS) wall-kick offset tables (`offsetMatrix` for `J`, `L`, `T`, `S`, `Z` pieces and `offsetMatrixI` for the `I` piece) across 5 collision tests so pieces can kick off walls and adjacent blocks when rotating.
* **Multithreaded Game Architecture:** Runs dedicated worker threads alongside the main OpenGL rendering loop using `std::thread` and `std::mutex` for automatic piece gravity (300 ms tick rate), instant hard drops, and continuous line-clear detection.
* **Point-Grid Collision System:** Represents the 10x21 playfield in a 2D state matrix (`allPiecesInBoard[21][10]`) where `-1` denotes empty space and `0` through `6` store landed block color indices.
* **Next Piece Preview & Persistent High Score:** Displays the upcoming tetromino in 3D space beside the board and renders the current score (`Pontos`) and all-time high score (`Record`, persisted locally in `record.txt`) via FreeType.

---

## Controls

### Tetromino Controls
| Key | Action |
| :--- | :--- |
| **Left / Right / Down Arrows** | Move active piece left, right, or soft-drop down |
| **Z** | Rotate piece counter-clockwise |
| **X** | Rotate piece clockwise |
| **Space** | Hard-drop piece instantly to the bottom |

### 3D Camera & System Controls
| Key / Input | Action |
| :--- | :--- |
| **W / A / S / D** | Move camera forward, left, backward, or right |
| **E / Q** | Move camera upward or downward |
| **Mouse Movement** | Look around in 3D space |
| **Mouse Scroll** | Zoom camera in and out |
| **M** | Print debug board matrix and piece coordinates to console |
| **Esc** | Join worker threads and exit the game |

---

## Tech Stack & Dependencies

* **Language:** C++
* **Graphics API:** OpenGL 3.3 Core Profile
* **Windowing & Input:** GLFW
* **Extension Loader:** GLAD
* **Mathematics:** GLM (OpenGL Mathematics)
* **Font Rendering:** FreeType
* **Texture Loading:** `stb_image.h`
* **IDE / Build System:** Microsoft Visual Studio (`Tetris.sln`)

---

## Project Structure

* `main.cpp` : Core application entry point, OpenGL/GLFW initialization, shader setup, cubemap skybox loading, FreeType text rendering, input handling, and worker threads for gravity and line clearing.
* `piecesCoord.h` : 3D cube vertices, skybox vertices, board frame coordinates and RGB gradient colors, relative tetromino coordinates (`I`, `L`, `J`, `O`, `S`, `Z`, `T`), and SRS wall-kick offset matrices.
* `shaders/` : Vertex and fragment shaders for 3D cubes (`pieces.vs`, `pieces.fs`), 2D HUD text (`text.vs`, `text.fs`), and the cubemap skybox (`skybox.vs`, `skybox.fs`).
* `textures/` : Block texture (`blockBW.png`) and the 6 cubemap skybox faces.
* `fonts/` : TrueType font (`arial.ttf`) used for score and record rendering.
* `dependencies/` : Bundled headers and libraries for GLAD, GLEW, GLFW, GLM, and FreeType.

---

## Authors

* **Afonso Oliveira**
* **Nuno Monteiro**
* **Rúben Abadesso**
* **Margarida Silva**
