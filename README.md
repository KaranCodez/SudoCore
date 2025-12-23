# ☕ Desktop Sudoku (JavaFX)

![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![JavaFX](https://img.shields.io/badge/UI-JavaFX-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-success?style=for-the-badge)

## 📁 Project Overview
A complete desktop Sudoku application built from scratch using **Java** and **JavaFX**. 

This project intentionally avoids FXML and external build tools (Gradle/Maven) to demonstrate a deep understanding of object-oriented programming, algorithm design, and the Java module system. It implements a custom software architecture that strictly separates the **Problem Domain**, **User Interface**, and **Control Logic**.

---

## 🧠 Architectural Highlights (Deep Dive)

This application goes beyond basic functionality by implementing robust design patterns discussed in the development process:

### 1. ⚡ O(1) UI Rendering with HashMaps
Instead of iterating through a list of 81 TextFields (`O(n)`) to update the board, the UI uses a `HashMap<Coordinates, TextField>` structure.
- **Custom Hashing:** The `Coordinates` class overrides `hashCode()` and `equals()` to serve as a unique key.
- **Performance:** This allows instantaneous retrieval of any specific grid cell to update its state or style without traversing the entire board.

### 2. 🛡️ Immutability & Data Safety
- **State Management:** The `SudokuGame` class (the Model) protects its internal state. 
- **Defensive Copying:** The `SudokuUtilities` class handles array copying to ensure that the game logic operates on new instances of data rather than mutating shared references, preventing side effects.

### 3. 🧩 Decoupled Logic (Separation of Concerns)
- **SudokuBuildLogic:** A dedicated class responsible for "wiring" the application parts together. It separates the *configuration* of objects from their *use*, acting as a manual Dependency Injection container.
- **Interfaces:** The UI and Control Logic communicate strictly through the `IUserInterfaceContract`. This follows the "Design by Contract" principle, making the system modular and testable.

### 4. 🧮 Algorithmic Computation
- **Backtracking Solver:** A custom algorithm in `SudokuSolver` that recursively attempts to fill the grid, validating constraints (Row, Column, 3x3 Grid) at each step.
- **Game Generation:** A "Seed and Dissolve" approach that generates a valid full board first, then strategically removes numbers to create a solvable puzzle.

---

## 📂 Package Structure

The codebase is organized into logical layers rather than technical types:

```text
src/
├── problemdomain/       # The "Soul" of the app (SudokuGame, Coordinates, Constants)
├── userinterface/       # JavaFX View & Event Handling (TextFields, Canvas)
├── computationlogic/    # The "Brain" (Solver, Generator, Validator)
├── buildlogic/          # The "Glue" (Main wiring class)
├── persistence/         # Storage implementation (LocalStorageImpl)
└── SudokuApplication.java  # Entry point
```

---

## 🛠️ How to Run (Command Line)

Since this project avoids Gradle/Maven to maintain simplicity and transparency, you can run it directly using the Java command line tools.

**Prerequisites:** 
- JDK 11+
- JavaFX SDK (downloaded separately)

### 1. Compile
Replace `/path/to/javafx-sdk` with your actual JavaFX library location.

```bash
javac --module-path /path/to/javafx-sdk/lib \
    --add-modules javafx.controls \
    -d out \
    src/**/*.java
```

### 2. Run
```bash
java --module-path /path/to/javafx-sdk/lib \
    --add-modules javafx.controls \
    -cp out \
    SudokuApplication
```

---

## 🎮 Features
- **Interactive UI:** Custom-built JavaFX UI without FXML.
- **Input Validation:** Regex-based filters prevent invalid characters (`[0-9]` only).
- **Auto-Completion Check:** The app listens for board completion and validates the win state.
- **Persistence:** Automatically saves progress to a local `.ser` file using Java Serialization.

---

## 📸 Screenshots

*(Add your screenshots here: `![Board](screenshots/board.png)`)*
