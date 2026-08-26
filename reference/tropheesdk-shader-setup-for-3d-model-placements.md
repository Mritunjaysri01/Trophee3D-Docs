# TropheeSDK Shader Setup for 3D Model Placements

This guide walks you through configuring shaders for 3D model placements in TropheeSDK, covering both built-in custom shaders and Universal Render Pipeline (URP) shaders. Follow these steps to ensure your models render correctly in both the Editor and your final build.

### 1. Overview

* **Compatibility**\
  TropheeSDK supports two shader modes:
  1. **Custom Shader** (built on Unity’s Built-in Render Pipeline)
  2. **URP Shader** (for projects using the Universal Render Pipeline)
* **Shader Selection**\
  Control which shader is applied per placement via the **Use URP Shader** checkbox on the `Trophee3DCampaignManager` component.
* **Pink Model Fix**\
  If models appear pink after building (a sign that their shaders weren’t included), you must explicitly add the custom shader to Unity’s “Always Include” list.

***

### 2. Prerequisites

1. **Unity Project Setup**
   * For **Built-in**: No extra packages required.
   * For **URP**: Ensure your project has the **Universal RP** package installed and assigned in **Project > Graphics**.
2. **TropheeSDK Installed**\
   Import the latest TropheeSDK package into your project, which provides the `Trophee3DCampaignManager` component and accompanying shaders.

***

### 3. Shader Selection in the Inspector

1. **Locate the Placement**
   * Select your 3D placement GameObject in the Hierarchy.
   * In the Inspector, find the **Trophee 3D Campaign Manager (Script)** component.
2. **Toggle Shader Mode**
   * **Use URP Shader** ▶︎ Checked\
     Applies the URP-compatible GLTF shader shipped with TropheeSDK.
   * **Use URP Shader** ▶︎ Unchecked\
     Applies the custom GLTF shader designed for the Built-in pipeline.

<figure><img src="../.gitbook/assets/Screenshot 2025-05-12 144627 (2).png" alt=""><figcaption></figcaption></figure>

***

### 4. URP-Specific Configuration

If your project uses URP and you encounter pink (magenta) models at runtime or in builds, follow these steps:

1. **Open Project Settings**
   * **Edit > Project Settings > Graphics**
2. **Always Include Shaders**
   * Expand the **Always Included Shaders** list.
   * Click **Size** and increase by one.
   *   Assign your TropheeSDK URP shader in the new element slot, for example:

       ```
       TropheeSDK/URPGLTFShader
       ```
3.  **Save & Rebuild**

    * Save your Graphics asset.
    * Rebuild your project to include the shader in the build.

    <figure><img src="../.gitbook/assets/Screenshot 2025-05-12 152606.png" alt=""><figcaption></figcaption></figure>

***

### 5. Built-in Pipeline (Custom Shader)

For projects **not** using URP:

* No additional Project Settings changes are required in most cases.
* If you experience pink models in builds:
  1. Repeat the “Always Include Shaders” steps above.
  2.  Add the custom shader:

      ```
      Assets/TropheeSDK/Runtime/tropheeShader
      ```

***

### 6. Troubleshooting

| Issue                            | Cause                            | Resolution                                                                                               |
| -------------------------------- | -------------------------------- | -------------------------------------------------------------------------------------------------------- |
| Models appear magenta (pink)     | Shader not included in the build | Add the appropriate TropheeSDK shader to **Always Included Shaders** in Graphics Settings, then rebuild. |
| Shader selector not visible      | Outdated TropheeSDK version      | Update to the latest TropheeSDK package; ensure the `Use URP Shader` field appears on the component.     |
| Errors finding shader at runtime | Shader path mismatch             | Verify the exact shader path in your build:                                                              |

###
