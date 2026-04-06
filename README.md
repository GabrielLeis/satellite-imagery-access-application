# Satellite Imagery Access Application

![Java](https://img.shields.io/badge/Java-17%2B-orange) ![Orekit](https://img.shields.io/badge/Physics-Orekit-blue) ![License](https://img.shields.io/badge/License-MIT-green)

Command-line interface (CLI) tool developed in Java that bridges the gap between theoretical orbital mechanics and real-world data acquisition. It computes precise satellite visibility windows (Sentinel-2) over a Ground Station or ROI and automates product downloads from the Copernicus Dataspace ecosystem.

## Key Features

* **Orbital Mechanics Computation:** Uses the Orekit library to propagate orbits and detect visibility events ("Rising" and "Setting") in real time, instead of relying on static databases.
* **Efficient Memory Management (I/O):** Implements `java.net.http.HttpClient` with `InputStreams` handling to download large products (+1GB) directly to disk, preventing RAM overflows (`OutOfMemoryError`).
* **Smart Business Logic:** Transforms physical visibility events into compatible OData queries, applying time buffers to account for differences between satellite pass time and product ingestion time.
* **Portability:** Automatic operating system detection and path management relative to the user directory (`user.home`) for compatibility across Windows, macOS, and Linux.

## Tech Stack

* **Language:** Java (JDK 17+)
* **Space Dynamics:** Orekit Library
* **Networking:** `java.net.http.HttpClient` (Native HTTP/2 support)
* **Parsing:** JSON (Jackson/Gson) & OData Protocol
* **Build System:** Maven / Gradle

## Setup (Prerequisite)

This application requires physical data (Earth orientation parameters, UTC-TAI leap seconds, ephemerides) to initialize the Orekit context.

1. **Download data:** Get the latest `orekit-data.zip` file from Orekit.
2. **Install:**
   * Unzip the file.
   * Rename the resulting folder to `orekit-data`.
   * Move the folder to your user root directory:
     * **Windows:** `C:\Users\YourUser\orekit-data`
     * **macOS/Linux:** `/Users/YourUser/orekit-data` or `/home/YourUser/orekit-data`

> **Note:** The application will automatically look for this folder on startup. If it does not exist, execution will stop with an explanatory error.

## Execution

### From the JAR (Recommended)
Download the latest version from the "Releases" section of this repository and run:

```bash
java -jar Satellite-Imagery-Access-Application.jar
