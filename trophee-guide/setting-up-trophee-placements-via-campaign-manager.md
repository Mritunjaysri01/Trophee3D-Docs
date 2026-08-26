# 👉 Setting Up Trophée Placements via Campaign Manager

When you configure Trophée placements using the Campaign Manager, you will initially see a placeholder representing your selected placement type.



<details>

<summary>2D Placement</summary>

1. **Selecting 2D Placement**
   * If you select the **2D Placement** type and click the **Instantiate** button, a `Trophee2DPlacement` GameObject will be created in your active scene.
   * For 2D placement, the `SpriteRenderer` component provides an option to seamlessly integrate Trophee placements within your game.
2. **Canvas Integration**
   * `Trophee2DPlacement` utilizes Unity's **Canvas** component.
   * If an active canvas exists in your scene, the placement will be created within that canvas.
   * If no canvas is present, the SDK will automatically generate one.
3. **Customizing the Placement**
   * By default, the **2D placement** is an **Image** component with a size of `100 x 100` pixels.
   * You can resize and reposition it according to your canvas layout or game requirements.
   * Adjust the **Canvas** placement to position the **2D placement** at the desired location in your game.

</details>

<details>

<summary>3D Placement</summary>

1. **Selecting 3D Placement**
   * If you choose the **3D Placement** type and click the **Instantiate** button, a `Trophee3DPlacement` GameObject will appear in your active scene.
2. **Using the Placement Cube**
   * The `Trophee3DPlacement` GameObject is represented as a **Cube**.
   * This cube helps you define the placement position where the Trophée campaign content will be displayed.
3. **Customizing the Placement**
   * You can **adjust the cube's size and position** to fit your scene and game environment.
   * This allows for precise placement of the Trophée campaign content within your game world.

</details>



### Summary

* **2D Placement**: Uses a **Canvas** and **Image** component for On-Menu screen placements and Sprite Renderer for embedded placements.&#x20;
* **3D Placement**: Uses a **Cube** to define positioning in the game world.
* Both placements are customizable in **size and position** to match your game's layout and design needs.

By following these steps, you can seamlessly integrate Trophée placements into your Unity game environment for immersive in-game commerce experiences.

Note: You need to implement logic to serve both placements. Refer to the Trophée Manager page for details.

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>
