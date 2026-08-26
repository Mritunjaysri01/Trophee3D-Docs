---
icon: expand
---

# Adjusting Trophee Campaign View

The **Trophée Campaign View** allows players to see campaign content **within the game**, ensuring a seamless experience without redirecting them outside the game environment. This view displays served campaign content or advertiser materials directly inside your game.

### Customizing the Campaign View

Developers can modify the **height, width, or display area** of the campaign view to align with the game's UI and screen requirements.

#### Steps to Adjust Campaign View:

1. **Navigate to the Resources Folder** → Open **Trophée Canvas**.
2. **Select the Appropriate Canvas type**
   * Choose the canvas type you initially selected for your placement (Landscape or Portrait).
3. **Open the Canvas in Unity Editor**
4. **Locate the AdView GameObject**
5. Inside **AdView**, you will find:
   * **AdViewContainer** (The primary campaign content display area)
   * **AdViewCloseButton** (A close button for dismissing the campaign view)
6. **Modify the Rect Transform**
   * Adjust **size, position, and scaling** of the **AdViewContainer** to fit your screen layout.
   * Ensure the **AdViewCloseButton** is placed for easy access by players.

<figure><img src="../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

### Best Practices

* **Maintain UI Consistency**: Align the campaign view with your game’s UI style.
* **Optimize for Different Screen Sizes**: Test across multiple resolutions to ensure the best experience.
* **Ensure Accessibility**: The close button should be easily visible and accessible for users.

By following these steps, developers can seamlessly integrate and adjust the Trophée Campaign View, ensuring an optimized experience.
