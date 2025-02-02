# Setup Guide

## Prerequisites
Before setting up the project, ensure you have the following installed:
- **Python 3.x** (for the backend)
- **pip** (Python package manager)
- **MongoDB** (for database storage)
- **Android Studio** (for the Android app)
- **Java 8+** (for the Android app and library)

## Backend Setup
1. Clone the repository:
   ```bash
   git clone https://github.com/GalRadia/Inventory-Management-Backend.git
   ```
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Run the backend server:
   ```bash
   python app.py
   ```
4. The server will start at `http://localhost:5000`.

You can now use the backend API as described in [Backend Documentation](/Docs/Backend.md).

## Android App Setup
1. Clone the repository:
   ```bash
   git clone https://github.com/GalRadia/InventoryManagement.git
    ```
2. Open **Android Studio**.
3. Select **Open an Existing Project** and choose the `android-app` folder.
4. Sync Gradle and build the project.
5. Run the app on an emulator or physical device.

## Android Library Setup
1. Add the dependency to `build.gradle`:
   ```gradle
	        implementation("com.github.GalRadia:InventoryManagement:Tag")
   ```
2. Sync Gradle and rebuild the project.
3. Use the library in your Android app as described in [Android Library Documentation](/Docs/AndroidLibrary.md).
