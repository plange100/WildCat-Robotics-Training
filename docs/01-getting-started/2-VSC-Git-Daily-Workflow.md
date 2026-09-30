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

## 4. Staging & Committing (Saving Your Work Locally)

> [!NOTE]
>A **commit** is like a permanent save point in a video game.

### Step 1: Review What Changed
In the **Source Control** sidebar (`Ctrl + Shift + G`), look under **Changes**. Clicking any file will open a side-by-side diff showing exactly what lines you added (green) or deleted (red).

### Step 2: Stage Your Changes
* **In VS Code:** Hover over the file name and click the `+` icon next to it (or click the `+` next to the word **Changes** to stage all files at once). The files move up to **Staged Changes**.
* **In Terminal:**
  ```bash
  # Stage a specific file
  git add src/main/java/frc/robot/subsystems/DriveSubsystem.java

  # Or stage all modified files at once
  git add .

### Step 3: Write a Meaningful Commit Message
In the text box above the staged files, write a short summary of what you did.

> [!NOTE]
> Good commit messages make troubleshooting easy. Use present tense and describe the change:
> * ✅ `Add soft limits to elevator motor`
> * ✅ `Invert left drive motors and update deadband`
> * ❌ `fixed stuff`
> * ❌ `code`

### Step 4: Commit
* **In VS Code:** Click the blue checkmark button labeled **Commit** (or press `Ctrl + Enter`).
* **In Terminal:**
  ```bash
  git commit -m "Add soft limits to elevator motor"
---

## 5. Pushing (Uploading to GitHub)

Your commit is currently only saved on your laptop. To share it with your mentors and teammates, you must push it to GitHub.

### Option A: Using the VS Code Interface
1. After committing, a blue button labeled **Sync Changes** or **Push** will appear in the Source Control panel.
2. Click **Sync Changes** (or click the circular arrows icon in the bottom-left blue status bar).

### Option B: Using the Terminal
```bash
git push origin main
```

---

## 6. Reviewing Git History & Logs

When something stops working, you need to see who changed what and when.

### Viewing History in VS Code (Using GitLens)
1. Open the file you want to inspect.
2. Look at the faint text to the right of your cursor line—**GitLens** shows the author and commit message inline.
3. Open the **Source Control** tab and expand the **Commits** or **File History** panel to see the full timeline of changes.

### Viewing History in the Terminal
```bash
# View a compact, one-line summary of recent commits
git log --oneline -n 10

# View a visual branch graph with author names
git log --graph --oneline --decorate --all
```

---

## 7. Undoing Mistakes & Reverting Changes

Everyone makes mistakes. Here is how to safely step backward without panicking:

### Scenario 1: You Made Changes to a File and Want to Erase Them Completely
You typed experimental code that failed and just want to reset the file to the way it was at the last commit:
* **In VS Code:** In the **Source Control** panel, hover over the modified file under **Changes** and click the **Discard Changes** icon (the curved arrow `↶`).
* **In Terminal:**
  ```bash
  # Restore a single file back to the last commit
  git restore src/main/java/frc/robot/Robot.java
  ```

### Scenario 2: You Committed Something Bad, But Have NOT Pushed Yet
You clicked Commit, but realized you left a bug in your code:
* **In VS Code:** Click the `...` menu in Source Control > **Commit** > **Undo Last Commit**. Your changes return to the Staging area so you can fix them.
* **In Terminal:**
  ```bash
  # Undoes the commit, but keeps all your typed code in your editor
  git reset --soft HEAD~1
  ```

### Scenario 3: Bad Code Was Already Pushed to GitHub
Never rewrite history that teammates have already downloaded. Instead, create a new commit that reverses the bad commit:

```bash
# Find the 7-character commit ID using git log --oneline (e.g., a1b2c3d)
git log --oneline -n 5

# Create a safe revert commit
git revert a1b2c3d
git push origin main
```

---

## 8. Resolving Merge Conflicts

A **merge conflict** happens when two people edit the **exact same lines of the same file** and Git doesn't know which version is correct.

> [!CAUTION]
> Conflicts look scary, but they do not break your computer. Git simply stops and asks: *"Which lines do you want to keep?"*

### How to Resolve Conflicts in VS Code:
1. When you run `git pull`, VS Code will alert you that a conflict occurred.
2. In the file explorer, conflicting files will show a red `!` or `C`.
3. Click on the file. VS Code will highlight the conflicting section with four clickable options:
   * **Accept Current Change:** Keeps the code you wrote on your laptop.
   * **Accept Incoming Change:** Keeps the code written by your teammate on GitHub.
   * **Accept Both Changes:** Keeps both blocks of code.
   * **Compare Changes:** Opens a 3-way visual merge editor.
4. Click the option that keeps the correct logic.
5. Save the file (`Ctrl + S`).
6. Build your robot code (`Ctrl + Shift + P` > `WPILib: Build Robot Code`) to verify there are no syntax errors.
7. Stage the resolved file (`+`), commit it with a message like `Resolve merge conflict in DriveSubsystem`, and **Push**.

---

## 9. Quick Git Cheat Sheet

| Task | VS Code Shortcut / UI Action | Terminal Command |
| :--- | :---: | :--- |
| Check status of files | Open Source Control tab (`Ctrl + Shift + G`) | `git status` |
| Pull updates from team | Blue status bar **Sync** button | `git pull` |
| Stage all modified files | Click `+` on the **Changes** header | `git add .` |
| Commit staged files | Type message and click **Commit** (`Ctrl + Enter`) | `git commit -m "Message"` |
| Push commits to GitHub | Click **Sync Changes** button | `git push origin main` |
| Discard local edits | Click curved arrow `↶` on file | `git restore <file>` |
| View commit timeline | Inspect GitLens sidebar | `git log --oneline` |