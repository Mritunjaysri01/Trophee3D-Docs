# Fallback Banner Demand Channel

Trophee Canvas placements and in-world Sprite placements can serve image banners from Game Commerce campaigns, the Fallback Banner Demand Channel, or a combination of both.

## Supported placements

Fallback banners are available for both Canvas-based 2D placements and Sprite placements embedded in the game world. Both use the normal Trophee activation, refresh, visibility, and interaction flow.

## Set up through the Unity Inspector

No code is required for the normal setup. Configure each placement from the Unity Editor:

1. Open the scene containing your Trophee placement.
2. In the **Hierarchy**, select the placement GameObject.
3. In the **Inspector**, locate the Trophee placement settings.
4. Under **Campaign Source**, open **Placement Mode**.
5. Select the mode you want from the table below.
6. When you select **Hybrid** or **In Game Only**, the **Banner Size** field appears automatically.
7. Select the required banner size.
8. Save the scene.

The fallback banner connection is supplied automatically by Trophee when the SDK initializes. You do not need to enter an endpoint or add any scripts.

{% hint style="success" %}
For the usual setup, the only required choices are **Placement Mode** and, when displayed, **Banner Size**.
{% endhint %}

## Choose the Placement Mode

| Mode | Behavior |
| --- | --- |
| **Game Commerce** | Requests only the configured Trophee Game Commerce campaign. |
| **Hybrid** | Requests Game Commerce first, then the fallback banner channel when the first source has no available banner. |
| **In Game Only** | Requests the fallback banner channel directly. |
| **Rewarded Video Fallback** | Uses the rewarded mediation fallback flow instead of the banner demand channel. |

{% hint style="info" %}
Use **Hybrid** when a placement should prefer a Trophee campaign but remain eligible for fallback banner demand.
{% endhint %}

## Choose a banner size

The **Banner Size** dropdown is visible only when **Placement Mode** is set to **Hybrid** or **In Game Only**. Select the size that matches the placement reserved in your scene.

| Option              | Dimensions |
| ------------------- | ---------- |
| Banner              | 320 x 50   |
| Medium Rectangle    | 300 x 250  |
| Large Mobile Banner | 320 x 100  |
| Leaderboard         | 728 x 90   |
| Large Leaderboard   | 970 x 90   |
| Wide Skyscraper     | 160 x 600  |
| Half Page           | 300 x 600  |
| Billboard           | 970 x 250  |

### Canvas placement behavior

For a Canvas placement:

* **In Game Only** immediately previews the selected dimensions in the Scene view.
* **Hybrid** keeps the Game Commerce placeholder size in the Scene view. The selected banner dimensions are applied only when a fallback banner creative is displayed.
* Returning to **Game Commerce** restores the recorded placeholder size.

### Sprite placement behavior

For a Sprite placement, the selected dimensions are used for the banner request. The rendered banner preserves its aspect ratio and fits within the sizing configured in the Inspector. Use the visible sizing and interaction fields to control its world-space presentation and clickable area.

## What the SDK handles automatically

After the Inspector setup is saved, the SDK automatically:

* Connects to the configured fallback banner channel.
* Requests the appropriate demand source for the selected mode.
* Applies the response refresh interval when provided.
* Renders the returned image in the selected Canvas or Sprite placement.
* Tracks viewable impressions and clicks.
* Opens the creative destination URL when the player interacts with the banner.


## Troubleshooting

### The placement remains empty

* Confirm the selected GameObject is a Trophee Canvas or Sprite placement.
* Confirm **Placement Mode** is set correctly in the Inspector.
* For **Hybrid** or **In Game Only**, confirm a **Banner Size** is selected.
* For **In Game Only**, enter Play mode and confirm Trophee initialization completes successfully in the Unity Console.

### The Canvas placeholder changes size

**In Game Only** intentionally previews the selected standard dimensions. **Hybrid** and **Game Commerce** preserve the Game Commerce placeholder size until a fallback banner creative is displayed.
