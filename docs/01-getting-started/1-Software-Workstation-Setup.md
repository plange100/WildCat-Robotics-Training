# Wildcat Robotics Software Workstation Setup Guide

Follow this guide in order to configure a laptop for FRC robot programming with Java, WPILib, Git, and Visual Studio Code.

---

## Step 1. Install WPILib & Tools (Includes Java & VS Code)

> [!IMPORTANT]
> **Do not install standalone Java or standalone VS Code first.**  
> The official **WPILib Installer** bundles a dedicated, sandboxed OpenJDK (JDK 17) and an isolated instance of VS Code configured specifically to avoid breaking system paths or conflicting with other versions.

### A. Install WPILib

1. Download the latest release of the **WPILib Installer** from the official WPILib GitHub Releases page: https://github.com/wpilibsuite/allwpilib/releases
   * **Windows:** Download the `.iso` file. Right-click and choose **Mount**, then run `WPILibInstaller.exe`.
   * **macOS:** Download the `.dmg` file and drag the WPILib application to Applications.
   * **Linux:** Download the `.tar.gz`, extract it, and run `WPILibInstaller`.
2. In the installer wizard:
   * Select **Install for this user** (or all users if shared team laptop).
   * Select **Install Everything** (this installs the WPILib-customized VS Code, JDK, RobotBuilder, OutlineViewer, Glass, SysId, and PathWeaver).
3. Once finished, launch **WPILib VS Code** from your desktop/application menu (it has the red/white/blue WPILib hexagonal icon).

---

## Step 2. Install & Configure Git

If Git was not bundled or you need command-line tools:

### A. Install Git
* **Windows:** Download and install from https://git-scm.com/ . Leave all standard defaults checked (use standard OpenSSH, checkout Windows-style/commit Unix-style line endings).
* **Ubuntu/Linux:**
  `sudo apt update && sudo apt install git -y`
* **macOS:**
  `xcode-select --install`

### B. Global Configuration (Name & Email)
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
```

---

## Step 3. Essential VS Code Extensions for FRC & Java

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

---

## Step 4. Install FRC Vendor Libraries (Vendordeps)

Modern FRC robots require third-party libraries for motor controllers, sensors, and gyros. These must be added to each robot project:

### Common Vendor URLs:
* **REVLib (Spark Max, Spark Flex, NEO, Vortex):**  
  `https://software-metadata.revrobotics.com/REVLib-2027.json`
* **CTRE Phoenix 6 (Pigeon 2.0, CANcoder, Kraken, Falcon 500):**  
  `https://maven.ctr-electronics.com/release/com/ctre/phoenix6/latest/Phoenix6-frc2027-latest.json`
* **Kauai Labs (navX):**  
  `https://dev.studica.com/releases/2027/NavX.json`

### How to Add a Vendor Library in VS Code:
1. Open your robot project folder in VS Code.
2. Press `Ctrl + Shift + P` (or click the red **`W`** WPILib logo in the top right).
3. Type and select **`WPILib: Manage Vendor Libraries`**.
4. Select **`Install new library (online)`**.
5. Paste the vendor `.json` URL from above and press **Enter**.
6. VS Code will download the dependencies into the `vendordeps/` folder and rebuild the Gradle project.

---

## Step 5. Setting Your FRC Team Number in VS Code

Setting your team number allows VS Code to automatically locate and deploy code to the roboRIO over USB (`172.22.11.2`) or radio Wi-Fi (`10.TE.AM.2`):

1. Press `Ctrl + Shift + P` to open the Command Palette.
2. Type and select **`WPILib: Set Team Number`**.
3. Enter your team number (e.g., `9086`) and press **Enter**.
4. This saves to `.wpilib/wpilib_preferences.json`.

---

## Step 6. Recommended VS Code Settings for FRC

Add these settings to VS Code to streamline Java robot programming. 

Press `Ctrl + Shift + P` > type `Preferences: Open User Settings (JSON)` > paste the following inside the root `{}`:

```json
{
  "editor.formatOnSave": true,
  "editor.suggestSelection": "first",
  "files.autoSave": "onFocusChange",
  "files.exclude": {
    "**/.git": true,
    "**/.svn": true,
    "**/.hg": true,
    "**/CVS": true,
    "**/.DS_Store": true,
    "**/Thumbs.db": true,
    "**/build": true,
    "**/.gradle": true
  },
  "java.configuration.updateBuildConfiguration": "automatic",
  "git.autofetch": true,
  "git.confirmSync": false
}

* `"editor.formatOnSave": true`: Auto-formats Java code every time a student saves.
* `"files.exclude"`: Hides compiled `build/` and `.gradle/` folders from the file tree to keep the workspace clean.
* `"git.autofetch": true`: Periodically checks GitHub in the background so students know if someone else has pushed new code.
```

---

## Step 7. First Verification Test

1. Open WPILib VS Code.
2. Press `Ctrl + Shift + P` > select `WPILib: Create a new project`.
3. Select `Template` > `Java` > `Command-Based Skeleton`.
4. Pick a folder, enter your team number, and click `Generate Project`.
5. Press `Ctrl + Shift + P` > select `WPILib: Build Robot Code` (or press `F5`).
6. If the output terminal displays `BUILD SUCCESSFUL`, your development workstation is fully operational.