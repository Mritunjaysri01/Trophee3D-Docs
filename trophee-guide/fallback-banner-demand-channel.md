# Fallback Banner Demand Channel

Trophee 2D UI placements and Sprite Renderer placements can serve image banners from Game Commerce campaigns, the Fallback Banner Demand Channel, or a combination of both.

## Supported components

Fallback banners are supported by `Trophee2DCampaignManager` for Canvas placements and `TropheeSpriteCampaignManager` for placements embedded in the game world. Both use the normal Trophee activation, refresh, visibility, click, and callback lifecycle.

## Select a campaign source

Select the placement GameObject and choose a **Placement Mode** under **Campaign Source**.

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

Use **Banner Size** in the Inspector to select the requested dimensions.

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

For a Canvas placement in `InGameOnly` mode, the SDK previews the selected dimensions on its `RectTransform` and preserves the image aspect ratio. Returning to a Game Commerce mode restores the recorded placeholder size.


## Troubleshooting

### The placement remains empty

* Confirm the component is `Trophee2DCampaignManager` or `TropheeSpriteCampaignManager`.
* For `InGameOnly`, verify SDK initialization supplied a valid endpoint.

### Trackers do not fire in the Editor

This is expected.&#x20;

### The Canvas placeholder changes size

`InGameOnly` uses the selected standard dimensions. Switching back to `GameCommerce` or `Hybrid` restores the recorded Game Commerce size until a fallback banner creative is selected.
