# Running UPHI in Visual Studio Code

This guide provides step-by-step instructions on how to open, run, and debug the **UPHI (Unified Patient Health Insight)** project using **Visual Studio Code (VS Code)**.

---

## 📋 Prerequisites
Ensure you have the following installed on your system:
1. **Node.js (LTS)**
2. **Java 17 JDK or higher** (e.g., Eclipse Temurin or OpenJDK)
3. **MongoDB** (Running locally on the standard port `27017` or via Docker)
4. **Git**

---

## 🔌 Recommended Extensions
To get the best experience (including syntax highlighting, code completion, and direct debugging), we have configured workspace recommendations. When you open the project folder in VS Code, click **"Install"** on the recommended extensions popup, or search for these in the Extensions tab (`Ctrl+Shift+X`):
* **Extension Pack for Java** (`vscjava.vscode-java-pack`) — *For compiling & debugging Java*
* **Spring Boot Extension Pack** (`vmware.vscode-boot-dev-pack`) — *For running Spring Boot apps*
* **MongoDB for VS Code** (`mongodb.mongodb-vscode`) — *To inspect the database*
* **ESLint** (`dbaeumer.vscode-eslint`) & **Prettier** (`esbenp.prettier-vscode`) — *For frontend code formatting*
* **Expo Tools** (`expo.vscode-expo-tools`) — *For the React Native Expo app*

---

## 🏃 Running the Project in VS Code

We have created several pre-configured **VS Code Tasks** to automate starting all parts of the application.

### Step 1: Open the Workspace
1. Launch **VS Code**.
2. Click **File > Open Folder...** and select the root directory: `c:\code\uphi`.

### Step 2: Install Node Dependencies
Before running the frontend or mobile app for the first time, install their node dependencies. You can do this directly via VS Code Tasks:
1. Press `Ctrl+Shift+P` (or `Cmd+Shift+P` on Mac) to open the Command Palette.
2. Select **Tasks: Run Task**.
3. Choose **`Install Frontend Deps`**.
4. Repeat the same step and choose **`Install Mobile Deps`**.

---

### Step 3: Run the Services

You can run each component using the integrated terminal or using VS Code Tasks.

#### Option A: Running via VS Code Tasks (Recommended)
1. Open the Command Palette (`Ctrl+Shift+P`).
2. Select **Tasks: Run Task**.
3. Select the task you want to run:
   * **`Run Backend (Spring Boot)`** — Starts the backend server on `http://localhost:8080`
   * **`Run Frontend (Vite)`** — Starts the React web app on `http://localhost:5173`
   * **`Run Mobile (Expo)`** — Starts the Metro Bundler for Expo React Native app
   * **`Docker Compose Up`** — Launches everything (DB + Backend + Web) in Docker containers

*Tip: You can open multiple terminal panels in VS Code to see them running side-by-side!*

#### Option B: Debugging via the Run & Debug View
We have configured launch targets in `.vscode/launch.json`:
1. Click on the **Run & Debug** icon on the VS Code Activity Bar (`Ctrl+Shift+D`).
2. Select a configuration from the dropdown at the top:
   * **`Debug Backend (Spring Boot)`** — Compiles, launches, and attaches the Java debugger to the backend. You can set breakpoints inside Java classes.
   * **`Launch Frontend in Chrome`** — Opens a debug-attached Google Chrome browser pointing to `http://localhost:5173`.
   * **`Debug Full Stack (Java + Frontend)`** — Launches both in debug mode simultaneously!
3. Click the green play/start button (or press `F5`).

---

## 🧪 Testing the Applications

Once the services are running:

### 1. Web Portal
* Open [http://localhost:5173](http://localhost:5173) in your browser.
* Use the pre-seeded demo accounts to log in:
  * **Doctor view**: Username: `doctor`, Password: `doctor123`
  * **Receptionist view**: Username: `receptionist`, Password: `recep123`
  * **Admin view**: Username: `admin`, Password: `admin123`

### 2. Expo Mobile App
* Once you start the `Run Mobile (Expo)` task, a QR code will display in the VS Code terminal.
* Install the **Expo Go** application on your Android or iOS device.
* Scan the QR code using Expo Go.
* *Note: Ensure your phone and PC are connected to the same Wi-Fi network.*

---

## 🔧 Database Configuration
By default, the backend expects MongoDB to be running at `mongodb://localhost:27017/uphidb`.
* If you use Docker, run `docker-compose up` or the **`Docker Compose Up`** task which handles setting up a containerized MongoDB instance automatically.
* If you want to connect to a different database instance, modify the `SPRING_DATA_MONGODB_URI` environment variable inside your `.env` file in the project root.
