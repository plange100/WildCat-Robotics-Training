# Wildcat Robotics Software Workstation Setup Guide

Follow this guide in order to configure a laptop for FRC robot programming with Java, WPILib, Git, and Visual Studio Code.

---

## 1. Install WPILib & Tools (Includes Java & VS Code)

> [!IMPORTANT]
> **Do not install standalone Java or standalone VS Code first.**  
> The official **WPILib Installer** bundles a dedicated, sandboxed OpenJDK (JDK 17) and an isolated instance of VS Code configured specifically to avoid breaking system paths or conflicting with other versions.

1. Download the latest release of the **WPILib Installer** from the official WPILib GitHub Releases page: https://github.com/wpilibsuite/allwpilib/releases
   * **Windows:** Download the `.iso` file. Right-click and choose **Mount**, then run `WPILibInstaller.exe`.
   * **macOS:** Download the `.dmg` file and drag the WPILib application to Applications.
   * **Linux:** Download the `.tar.gz`, extract it, and run `WPILibInstaller`.
2. In the installer wizard:
   * Select **Install for this user** (or all users if shared team laptop).
   * Select **Install Everything** (this installs the WPILib-customized VS Code, JDK, RobotBuilder, OutlineViewer, Glass, SysId, and PathWeaver).
3. Once finished, launch **WPILib VS Code** from your desktop/application menu (it has the red/white/blue WPILib hexagonal icon).

---

## 2. Install & Configure Git

If Git was not bundled or you need command-line tools:

### Step 1: Install Git
* **Windows:** Download and install from https://git-scm.com/ . Leave all standard defaults checked (use standard OpenSSH, checkout Windows-style/commit Unix-style line endings).
* **Ubuntu/Linux:**
  `sudo apt update && sudo apt install git -y`
* **macOS:**
  `xcode-select --install`

### Step 2: Global Configuration (Name & Email)
Open your terminal (or press Ctrl + ` in VS Code) and set your Git identity.

> [!WARNING]
> Use the **exact email address associated with your GitHub account**. If your email does not match, GitHub will not link your commits to your profile.

```bash
# 1. Set your display name (e.g., First Last)
git config --global user.name "First Last"

# 2. Set your GitHub email address
git config --global user.email "student@example.com"

# 3. Set the default initial branch name to main
git config --global init.defaultBranch main

# 4. Configure pull behavior to prevent messy merge commits
git config --global pull.rebase false

# 5. (Windows only) Ensure consistent line endings across platforms
git config --global core.autocrlf true

---

## 3. Essential VS Code Extensions for FRC & Java

The WPILib installer pre-packages the base Java language server and WPILib tools. Adding these specific Java and productivity extensions gives students a full-featured IDE experience with auto-completion, unit testing, and code generation.

### A. Java-Specific Extensions (Core Robot Coding)

1. **Extension Pack for Java** (`vscjava.vscode-java-pack`)  
   *Published by Microsoft.* If not already enabled by the WPILib installer, this is the foundation for Java in VS Code. It bundles:
   * **Language Support for Java™ by Red Hat** (`redhat.java`): Code completion (IntelliSense), syntax errors, refactoring, and auto-imports.
   * **Debugger for Java** (`vscjava.vscode-java-debug`): Allows setting breakpoints, stepping through robot loops, and inspecting variables in WPILib simulation.
   * **Test Runner for Java** (`vscjava.vscode-java-test`): Runs JUnit tests directly from the editor for physics simulation and autonomous trajectory verification.
   * **Project Manager for Java** (`vscjava.vscode-java-dependency`): Manages classpath and vendor dependencies cleanly.

2. **Gradle for Java** (`vscjava.vscode-gradle`)  
   *Published by Microsoft.* FRC uses Gradle under the hood (`./gradlew build`). This extension adds a dedicated sidebar icon to view Gradle tasks (e.g., `build`, `deploy`, `simulateJava`) and displays build failure details visually rather than burying them in console text.

3. **Checkstyle for Java** (`shengchen.vscode-checkstyle`)  
   Enforces team formatting rules and coding standards. You can point it directly to a shared team configuration (like WPILib or Google Java style) so students catch missing javadocs or bad naming before pushing to GitHub.

4. **SonarLint** (`SonarSource.sonarlint-vscode`)  
   Acts like a spell-checker for code logic. It highlights common Java bugs on the fly—such as potential `NullPointerException` risks, unused variables, resource leaks, or infinite loops—before you deploy to the roboRIO.

5. **Java Code Generators** (`helixquar.java-code-generators`)  
   Saves time by automatically scaffolding constructors, getters, setters, `equals()`, and `toString()` methods from highlighted class fields with a right-click.

### B. General Productivity & Git Extensions

1. **GitHub Pull Requests and Issues** (`GitHub.vscode-pull-request-github`)  
   View, review, and comment on teammates' GitHub Pull Requests and Issues directly within the VS Code sidebar.
2. **GitLens** (`eamodio.gitlens`)  
   Shows inline commit annotations right next to each line of code, revealing who wrote the logic and what commit message accompanied it.
3. **Error Lens** (`usernamehw.errorlens`)  
   Renders compiler errors and warnings directly inline next to the affected line of code so students immediately see syntax mistakes without hovering over red squiggles.
4. **Markdown All in One** (`yzhang.markdown-all-in-one`)  
   Provides keyboard shortcuts, auto-formatted lists, and fast previewing for `.md` training guides.
5. **Paste Image** (`mushan.paste-image`)  
   Allows pasting clipboard screenshots directly into markdown files, saving the image automatically to your project folder.

### How to Install Any Extension in VS Code:
1. Press `Ctrl + Shift + X` (or `Cmd + Shift + X` on Mac) to open the **Extensions** sidebar.
2. Search for the extension name or copy-paste its ID (e.g., `vscjava.vscode-gradle`).
3. Click **Install**.