---
icon: expand
---

# DIY Trophee Campaign View

### 1. Overview of the TropheeCanvas Prefabs

The Trophee SDK provides two prefab variants for displaying campaign-related content:

* **TropheeCanvasHorizontal** (for landscape-oriented games)
* **TropheeCanvasVertical** (for portrait-oriented games)

Both prefabs contain similar UI elements—background, close button, and other containers. The primary difference is how they are laid out for different screen orientations.

* **Prefab Locations**:
  * `Assets/TropheeSDK/Runtime/Resources/TropheeCanvasHorizontal.prefab`
  * `Assets/TropheeSDK/Runtime/Resources/TropheeCanvasVertical.prefab`

#### When to Use Which Prefab

* **TropheeCanvasHorizontal**: If your game primarily runs in a **landscape** orientation, use this version to ensure the campaign UI fits better horizontally.
* **TropheeCanvasVertical**: If your game primarily runs in a **portrait** orientation, use this version for a taller, more vertical layout.

### 2. Getting Started: Opening and Editing the Prefab

1. In Unity’s **Project** window, navigate to:\
   `Assets/TropheeSDK/Runtime/Resources/`
2. Locate the **TropheeCanvasHorizontal** or **TropheeCanvasVertical** prefab (depending on your game’s orientation).
3. **Double-click** or **right-click → Open** to open the selected prefab in **Prefab Mode**. This will let you see and edit all the child objects in the prefab hierarchy.

***

### 3. Customizing the Background (TropheeCampaignBg)

#### 3.1. Changing the Background Image

1. In the **Hierarchy** (while in Prefab Mode), select **TropheeCampaignBg**.
2. In the **Inspector**:
   * Look for the **Image** component.
   * Find the **Source Image** field.
   * Replace it with your desired texture by clicking the circle icon to the right or by dragging a new sprite/texture into that field.
3. Adjust the **Color** if you want to apply a tint or change alpha (transparency).

#### 3.2. Adjusting the Background Layout

* With **TropheeCampaignBg** selected, you can modify **Rect Transform** properties such as **Anchor**, **Pivot**, **Position**, **Width**, and **Height**.
* In **TropheeCanvasHorizontal**, the background will be more horizontally oriented by default; in **TropheeCanvasVertical**, it will be more vertically oriented. Adjust as needed for your UI.

#### 3.3. Additional Visual Effects

* If you have a 9-sliced sprite, set the **Image Type** to **Sliced** for dynamic resizing.
* Add a **Shadow** or **Outline** component (via **Add Component**) to create depth.
* Use **Canvas Group** or **Image** alpha to fade in/out or create transitions.

***

### 4. Customizing the CloseCanvas Button

#### 4.1. Changing the Button Icon

1. In the **Hierarchy**, locate the **CloseCanvas** button.
2. In the **Inspector**:
   * Select the **Image** component (or the **Button** component if the sprite is set there).
   * Change the **Source Image** to your custom close or exit icon.
3. If you want a hover or pressed state, add sprites to the **Button**’s transition states under the **Button** component in the **Inspector** (Normal, Highlighted, Pressed, Disabled).

#### 4.2. Positioning and Sizing

* In **TropheeCanvasHorizontal**, you might prefer the button in the top-right or top-left corner, depending on the UI layout.
* In **TropheeCanvasVertical**, the top corner might be more centered or aligned differently due to portrait constraints.
* Adjust the **Rect Transform** (Anchor, Pivot, Position, Width, Height) to fit your design.

#### 4.3. Interactivity and Animations

* Attach an **Animator** component or use Unity’s **Button** animations for hover, click, or fade-in effects.
* Add your own script to handle additional logic when the button is clicked (e.g., saving user data before closing the UI).

***

### 5. Adjusting Placement and Alpha of Other Elements

1. **Alpha / Transparency**:
   * Select any UI element (container, text, images) and change the **Color** alpha in the **Inspector**.
2. **Placement**:
   * Use **Rect Transform** tools to reposition elements and set anchor points, ensuring they adapt correctly in either a landscape or portrait layout.
3. **Layout Groups**:
   * If using **Vertical Layout Group** or **Horizontal Layout Group**, adjust spacing and padding to maintain a consistent look.
4. **Text Styling**:
   * Modify fonts, sizes, and colors in the **Text** or **TextMeshPro** component for headings, body text, etc.

***

### 6. Extending Customization

#### 6.1. Theming

* Use a **consistent color palette** and **fonts** across all elements.
* **Semi-transparent overlays** can unify the design and improve readability.

#### 6.2. Animation & Transitions

* **Canvas Group** can fade the entire canvas in/out.
* **Unity’s Animation** window can create slide-ins or scale transitions for different UI elements.

#### 6.3. Audio Feedback

* Add an **Audio Source** to play a click sound when the close button is pressed.
* If desired, add subtle background music or an ambient loop when the campaign is open.

#### 6.4. Additional UI Elements

* **Share Buttons** or **Social Media Icons** to encourage user engagement.
* **Progress Bars** or **Reward Animations** to visualize achievements or reward unlocks.

#### 6.5. Localization Support

* If you have multiple languages, ensure all **Text** components support localization (e.g., via **TextMeshPro** and a localization plugin).
* Keep your text within safe margins to avoid overflow in different languages or orientations.

***

### 7. Implementation Tips

* **Prefab Variants**: If you need multiple styles for different campaigns, consider **Prefab Variants** instead of duplicating the entire prefab.
* **Naming Conventions**: Keep clear names for game objects and components to streamline collaboration.
* **Resolution Testing**: In the Unity **Game** view, switch between different resolutions and aspect ratios to ensure the UI remains consistent.

***

### 8. Final Check & Best Practices

1. **Apply Changes**: After editing in Prefab Mode, click **Apply** so your changes persist.
2. **Play Mode Testing**: Verify that buttons, animations, and transitions work correctly in Play mode.
3. **Version Control**: Use Git or another VCS to track changes, especially when experimenting with UI layouts.
4. **Canvas Sorting**: If you need the Trophee canvas to appear on top of other UI elements, adjust the **Sort Order** in the Canvas component.

***

### Conclusion

Whether you are targeting a **landscape** or **portrait** game, the **TropheeCanvasHorizontal** and **TropheeCanvasVertical** prefabs give you flexibility to match your UI design. By changing images, button icons, positions, and other properties, you can create a cohesive, branded look that aligns with your game’s theme. For more advanced customizations, consider adding animations, sound effects, or localization support.

Following these guidelines will help ensure that the Trophee UI components integrate smoothly into your game, providing a polished experience for your players.

## Some samples are given below for reference :thumbsup:

<figure><img src="../.gitbook/assets/72 copy.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/7 copy.png" alt="" width="368"><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Group 54 (1).png" alt="" width="353"><figcaption></figcaption></figure>
