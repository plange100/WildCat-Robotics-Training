# FRC Software Workstation Setup Guide

Follow this guide in order to configure a laptop for FRC robot programming with Java, WPILib, Git, and Visual Studio Code.

---

## 1. Install WPILib & Tools (Includes Java & VS Code)

> [!IMPORTANT]
> **Do not install standalone Java or standalone VS Code first.**  
> The official **WPILib Installer** bundles a dedicated, sandboxed OpenJDK (JDK 17) and an isolated instance of VS Code configured specifically to avoid breaking system paths or conflicting with other versions.

1. Download the latest release of the **WPILib Installer** from the [official WPILib GitHub Releases page](https://github.com/wpilibsuite/allwpilib/releases).
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
* **Windows:** Download and install from [git-scm.com](https://git-scm.com/). Leave all standard defaults checked (use standard OpenSSH, checkout Windows-style/commit Unix-style line endings).
* **Ubuntu/Linux:**
  ```bash
  sudo apt update
  sudo apt install git -y