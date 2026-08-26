# Fallback Banner Demand Channel

Trophee 2D UI placements and Sprite Renderer placements can serve image banners from Game Commerce campaigns, the Fallback Banner Demand Channel, or a combination of both.

## Supported components

Fallback banners are supported by `Trophee2DCampaignManager` for Canvas placements and `TropheeSpriteCampaignManager` for placements embedded in the game world. Both use the normal Trophee activation, refresh, visibility, click, and callback lifecycle.

## Set up through the Unity Inspector

No code is required for the normal setup. Configure each placement from the Unity Editor:

1. Open the scene containing your Trophee placement.
2. In the **Hierarchy**, select the placement GameObject.
3. In the **Inspector**, locate the `Trophee2DCampaignManager` or `TropheeSpriteCampaignManager` component.
4. Under **Campaign Source**, open **Placement Mode**.
5. Select the mode you want from the table below.
6. When you select **Hybrid** or **In Game Only**, the **Banner Size** field appears automatically.
7. Select the required banner size.
8. Save the scene.

The fallback banner endpoint is loaded automatically from `DataNexus` at runtime. You do not need to paste an endpoint into the Inspector or configure it in a script.

{% hint style="success" %}
For the usual setup, the only required choices are **Placement Mode** and, when displayed, **Banner Size**.
{% endhint %}

## Choose the Placement Mode

| Mode | Behavior |
| --- | --- |
| `GameCommerce` | Requests only the configured Trophee Game Commerce campaign. |
| `Hybrid` | Requests Game Commerce first, then the fallback banner channel when the response is empty, is an error/no-ad result, or selects fallback banner demand. |
| `InGameOnly` | Requests the fallback banner channel directly. A valid endpoint must be available. |
| `RewardedVideoFallback` | Uses the rewarded mediation fallback flow instead of the banner demand channel. |

{% hint style="info" %}
Use `Hybrid` when a placement should prefer a Trophee campaign but remain eligible for fallback banner demand.
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

For a `Trophee2DCampaignManager`:

* **In Game Only** immediately previews the selected dimensions on the `RectTransform` in the Scene view.
* **Hybrid** keeps the Game Commerce placeholder size in the Scene view. The selected banner dimensions are applied only when a fallback banner creative is displayed.
* Returning to **Game Commerce** restores the recorded placeholder size.

### Sprite placement behavior

For a `TropheeSpriteCampaignManager`, the selected dimensions are sent with the banner request. The rendered sprite preserves its aspect ratio and fits within the configured sprite texture bounds. Use the component's existing sprite sizing and collider fields to control its world-space presentation and interaction area.

## What the SDK handles automatically

After the Inspector setup is saved, the SDK automatically:

* Loads the fallback banner endpoint from `DataNexus`.
* Requests the appropriate demand source for the selected mode.
* Applies the response refresh interval when provided.
* Renders the returned image in the UI `Image` or `SpriteRenderer`.
* Tracks viewable impressions and clicks.
* Opens the creative destination URL when the player interacts with the banner.


## Troubleshooting

### The placement remains empty

* Confirm the component is `Trophee2DCampaignManager` or `TropheeSpriteCampaignManager`.
* Confirm **Placement Mode** is set correctly in the Inspector.
* For **Hybrid** or **In Game Only**, confirm a **Banner Size** is selected.
* For **In Game Only**, verify SDK initialization completed so `DataNexus` could supply the endpoint.

### Trackers do not fire in the Editor

This is expected.&#x20;

### The Canvas placeholder changes size

**In Game Only** intentionally previews the selected standard dimensions. **Hybrid** and **Game Commerce** preserve the Game Commerce placeholder size until a fallback banner creative is displayed.
