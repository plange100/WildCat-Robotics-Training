# Wildcat Robotics Git & VS Code Daily Workflow Guide

This guide walks you through the essential daily Git workflow using Visual Studio Code. Whether you prefer using the VS Code graphical buttons or the terminal, follow these steps to keep our team's code in sync without losing work.

---

## 1. The Git Mental Model (How Git Sees Your Code)

Before running commands, it helps to understand the four places your code lives:

1. **Remote Repository (GitHub):** The shared cloud version the whole team connects to.
2. **Working Directory (Local Files):** The actual `.java` files you edit in VS Code on your laptop.
3. **Staging Area (Index):** The "packing box" where you gather files you are ready to save.
4. **Local Repository (Commit History):** The permanent snapshot saved on your laptop, ready to be sent to GitHub.

---

## 2. The Golden Rule of Team Coding

> [!IMPORTANT]
> **Always pull before you start working, and always pull before you push.**  
> Checking for updates before writing code prevents 95% of merge conflicts.

### The 4-Step Daily Rhythm:
1. **Pull:** Download the newest code from GitHub before making changes.
2. **Code & Test:** Write your logic and verify it builds.
3. **Stage & Commit:** Package your changes locally with a descriptive message.
4. **Push:** Upload your local commits back to GitHub for the team to use.

---

## 3. Pulling & Fetching (Getting Updates)

### What is the Difference?
* **Fetch (`git fetch`):** Asks GitHub, *"Is there anything new?"* It downloads the latest information in the background without touching your open files.
* **Pull (`git pull`):** Downloads the new code **and immediately merges it** into your current local files.

### Option A: Using the VS Code Interface (Recommended for Beginners)
1. Open the **Source Control** tab on the left sidebar (shortcut: `Ctrl + Shift + G`).
2. Click the **`...`** (Views and More Actions) menu at the top of the Source Control panel.
3. Select **Pull** (or click the circular **Sync Changes** button in the blue bottom status bar).

### Option B: Using the Terminal
Press `Ctrl + ` ` to open the built-in terminal, then run:

```bash
# Check if there are updates on GitHub without changing your files
git fetch

# Download and merge the latest team changes into your branch
git pull
```

---