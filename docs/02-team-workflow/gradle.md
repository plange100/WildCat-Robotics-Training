# Wildcat Robotics Gradle Workflow

For FRC development with WPILib, you rarely need to write low-level Gradle scripts from scratch. However, team members should master two core areas: **the essential terminal/wrapper commands** and **the key sections of `build.gradle` that require occasional modification**.

---

## 1. Core CLI Commands (Gradle Wrapper)

Always execute commands using the project's included Gradle wrapper (`./gradlew` on Linux/macOS or `gradlew.bat` on Windows) rather than a globally installed Gradle binary. Run these commands from the root directory of the repository:

| Command | Purpose | When to Use |
| :--- | :--- | :--- |
| `./gradlew build` | Compiles source code and validates syntax/types | Prior to committing code or connecting to the robot. |
| `./gradlew deploy` | Compiles and transfers binaries to the roboRIO | When connected to the robot (USB, Ethernet, or field Wi-Fi). |
| `./gradlew test` | Executes local unit tests (e.g., JUnit tests) | When verifying math or logic offline without physical hardware. |
| `./gradlew clean` | Wipes cached build artifacts from the `build/` directory | When debugging strange caching issues or phantom build errors. |
| `./gradlew clean build` | Runs a complete wipe followed by a clean rebuild | Recommended after pulling upstream updates from Git. |

> **VS Code Shortcuts:**  
> Press <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd> (or <kbd>Cmd</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd> on macOS) to open the Command Palette, then select:
> * `WPILib: Build Robot Code` (triggers `./gradlew build`)
> * `WPILib: Deploy Robot Code` (triggers `./gradlew deploy`)

---

## 2. Key Sections in `build.gradle`

Students typically interact with three main areas within `build.gradle`:

### A. Managing Vendor Libraries (Vendordeps)
Rather than manually managing raw `.jar` files, WPILib resolves dependencies via JSON configuration files stored in the `vendordeps/` directory (e.g., `REVLib.json` for SPARK MAX/Flex controllers, `navx_frc.json` for the navX2 IMU).

* **Installation:** In VS Code, open the Command Palette (<kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd>) and choose **`WPILib: Manage Vendor Libraries`** > **`Install new library (online)`** (or offline if cached locally).
* During `./gradlew build`, Gradle parses all JSON files inside `vendordeps/` and automatically resolves the necessary motor controller and sensor packages.

### B. JVM Arguments & Garbage Collection Optimization
Inside the `deploy` block of `build.gradle`, you can tune the JVM runtime options executed on the roboRIO:

```groovy
deploy {
    targets {
        roborio(getTargetTypeClass('RoboRIO')) {
            // JVM flags passed to Java on the roboRIO
            jvmArgs.addAll([
                "-XX:+UseG1GC",           // Use the low-pause G1 garbage collector
                "-XX:MaxGCPauseMillis=5"  // Constrain GC pause targets well within the 20ms periodic cycle
            ])
        }
    }
}
```

### C. Main Class Entry Point

If the application entry point shifts or fails to resolve automatically:

```groovy
def ROBOT_MAIN_CLASS = "frc.robot.Main"
```

## 3. Practical Troubleshooting

* **Initial Build Requires Internet Access:**  
  Gradle downloads all toolchains, native binaries, and vendor dependencies during the first execution. Always run `./gradlew build` in the shop or home workspace prior to attending an offline practice field or regional competition pit.

* **Deploy Priority & Fallback Routes:**  
  If deploys time out over the robot radio, attach a direct physical connection:
  * **USB-B direct to roboRIO:** Static IP `172.22.11.2`
  * **Direct Ethernet:** Attached to the network switch or radio aux port

  The `./gradlew deploy` task automatically scans candidate interfaces in order:
  1. `10.TE.AM.2` (mDNS / Team Radio Network)
  2. `172.22.11.2` (Direct USB Tether)
  3. `roboRIO-XXXX-FRC.local` (Local Multicast DNS)

* **Linux / macOS Execution Permissions:**  
  If the terminal returns a `permission denied: ./gradlew` error, grant execution rights to the wrapper:
  
  ```bash
  chmod +x gradlew
  ```