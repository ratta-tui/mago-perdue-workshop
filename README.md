Of course. Here is the `README.md` file rewritten for the Purdue University mago3d workshop, with all the necessary instructions.

-----

# 2025 Purdue University mago3d Workshop

Starter code for the 2025 mago3d workshop at Purdue University.

This example repository is designed to get workshop attendees up and running with a base [CesiumJS](https://cesium.com/platform/cesiumjs/) app for visualizing mago3d outputs. It's built using Vite and is based on the [`cesium-vite-example`](https://www.google.com/search?q=%5Bhttps://github.com/CesiumGS/cesium-vite-example%5D\(https://github.com/CesiumGS/cesium-vite-example\)).

## Requirements

- A [Cesium ion account](https://ion.cesium.com/signup)
- [Visual Studio Code](https://code.visualstudio.com/), or another IDE of your choice
- [NodeJS](https://nodejs.org/en), version 20+
- Optional: [Git](https://docs.github.com/en/get-started/git-basics/set-up-git#platform-all) to clone the repository

## Setup

1.  **Download the code:**

   - If you are using Git, **fork this repository** and clone it to your local machine.
   - Otherwise, **download the source code** as a ZIP file and unzip it to your desired location.

2.  In Visual Studio Code, open the project folder by using **File** \> **Open Folder...** and selecting the project directory from the previous step.

3.  Open the `src/main.js` file.

4.  **Create a new Cesium ion access token.** Your token is used to access Cesium ion's base imagery and other assets.

   - In your Cesium ion account, navigate to the [**Access Tokens**](https://ion.cesium.com/tokens) tab.
   - Click the **Create token** button.
   - Give the token a name (e.g., "Purdue Workshop") and leave the default settings. Click **Create**.
   - Copy the generated token string.

    > [Learn more about managing access tokens in Cesium ion.](https://cesium.com/learn/ion/cesium-ion-access-tokens/)

5.  Back in `src/main.js`, find the line `Cesium.Ion.defaultAccessToken = "YOUR_ACCESS_TOKEN";` and paste your new token in place of `YOUR_ACCESS_TOKEN`.

6.  In VS Code, open a new terminal by using **Terminal** \> **New Terminal**.

7.  Run the following commands to install the project dependencies and start the development server:

    ```sh
    # Install project dependencies
    npm install
    ```

    ```sh
    # Build and start the development server
    npm run dev
    ```

8.  In a web browser, navigate to the URL shown in the terminal, which is typically [`http://localhost:5173/`](https://www.google.com/search?q=http://localhost:5173/). You should now see a Cesium globe.

## Data Processing (with Mago3D)
This section contains the Docker commands to process the raw data for Hamilton County into 3D tilesets.

Note: Before running these commands, you must replace YOUR_PROJECT_DIR with the absolute path to your project folder on your machine. For example, on Windows, it might look like D:\my-workshops\cesiumjs-workshop.

Hamilton County

YOUR_PROJECT_DIR(ex C:\mago-perdue-workshop\..\)
1. **Terrain**
```Bash
# run mago-terrainer for window PowerShell
docker run --rm -v "YOUR_PROJECT_DIR\public\perdue:/workspace" `
   gaia3d/mago-3d-terrainer `
   --input /workspace/org/dem/ `
   --output /workspace/output/terrain/ `
   --log /workspace/output/terrain/log.txt `
   -cn --minDepth 0 --maxDepth 17
```
![](/public/images/terrain.png)

2. **Buildings**
```Bash
docker run --rm -v "YOUR_PROJECT_DIR\public\perdue:/workspace" `
  gaia3d/mago-3d-tiler `
  --input /workspace/org/buildings/Building_foot_prints_meter_clip.geojson `
  --output /workspace/output/tileset/buildings/ `
  --inputType geojson `
  --crs 4326 `
  --heightColumn "rel_height_2_meter" `
  --terrain /workspace/org/dem/hamilton_dem_navd88_meters_4326_clip_optimized.tif `
  --log /workspace/output/tileset/buildings/log.txt
```
![](/public/images/building.png)

3. **trees(i3dm)**
```Bash
docker run --rm -v "YOUR_PROJECT_DIR\public\perdue:/workspace" `
  gaia3d/mago-3d-tiler `
  --scaleColumn "rel_height_m" `
  --inputType gpkg `
  --input /workspace/org/forest/forest_meter_clip.gpkg `
  --outputType i3dm `
  --output /workspace/output/tileset/forest `
  --crs 4326 `
  --instance /workspace/org/forest/instance-LOD3.glb `
  --terrain /workspace/org/dem/hamilton_dem_navd88_meters_4326_clip_optimized.tif `
  --log /workspace/output/tileset/forest/log.txt `
  --tilesVersion 1.0
```
![](/public/images/trees.png)

4. **Point Cloud** 
```Bash
docker run --rm -v "YOUR_PROJECT_DIR\public\perdue:/workspace" `
  gaia3d/mago-3d-tiler `
  --input /workspace/org/pointcloud/forest_meter_4326.laz `
  --output /workspace/output/tileset/pointcloud `
  --log /workspace/output/tileset/pointcloud/log.txt `
  --inputType laz `
  --crs 4326 `
  --pointRatio 70 `
  --tilesVersion 1.0
```
![](/public/images/pnts.png)

## Developer Scripts
This project includes a few scripts to help with development. You can run any of them from the terminal.

npm run eslint: Find and fix common JavaScript code issues using ESLint.

npm run prettier: Format all code to a consistent style using Prettier.

npm run dev: Start a development server at http://localhost:5173/ ( or http://localhost:5174/ ) using Vite.

npm run build: Create an optimized build for production, with output in the dist/ directory.

## Developer Scripts

This project includes a few scripts to help with development. You can run any of them from the terminal.

- `npm run eslint`: Find and fix common JavaScript code issues using [ESLint](https://eslint.org/).
- `npm run prettier`: Format all code to a consistent style using [Prettier](https://prettier.io/).
- `npm run dev`: Start a development server at [`http://localhost:5173/`](https://www.google.com/search?q=http://localhost:5173/) using [Vite](https://vite.dev/).
- `npm run build`: Create an optimized build for production, with output in the `dist/` directory.