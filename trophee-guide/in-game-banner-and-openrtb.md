# In-game banners and OpenRTB

Trophee 2D UI placements and Sprite Renderer placements can serve image banners from Game Commerce campaigns, an OpenRTB source, or a combination of both.

## Supported components

OpenRTB banners are supported by `Trophee2DCampaignManager` for Canvas placements and `TropheeSpriteCampaignManager` for placements embedded in the game world. Both use the normal Trophee activation, refresh, visibility, click, and callback lifecycle.

## Select a campaign source

Select the placement GameObject and choose a **Placement Mode** under **Campaign Source**.

| Mode | Behavior |
| --- | --- |
| `GameCommerce` | Requests only the configured Trophee Game Commerce campaign. |
| `Hybrid` | Requests Game Commerce first, then OpenRTB when the response is empty, is an error/no-ad result, or explicitly selects OpenRTB. |
| `InGameOnly` | Requests OpenRTB directly. A valid endpoint must be available. |
| `RewardedVideoFallback` | Uses the rewarded mediation fallback flow instead of OpenRTB. |

{% hint style="info" %}
Use `Hybrid` when a placement should prefer a Trophee campaign but remain eligible for OpenRTB demand.
{% endhint %}

## Choose a banner size

Use **Banner Size** in the Inspector to select the requested dimensions.

| Option | Dimensions |
| --- | --- |
| Banner | 320 x 50 |
| Medium Rectangle | 300 x 250 |
| Large Mobile Banner | 320 x 100 |
| Leaderboard | 728 x 90 |
| Large Leaderboard | 970 x 90 |
| Wide Skyscraper | 160 x 600 |
| Half Page | 300 x 600 |
| Billboard | 970 x 250 |

For a Canvas placement in `InGameOnly` mode, the SDK previews the selected dimensions on its `RectTransform` and preserves the image aspect ratio. Returning to a Game Commerce mode restores the recorded placeholder size.

## Endpoint configuration

During initialization, `DataNexus` receives the OpenRTB endpoint from the Trophee campaign configuration and stores it in persistent SDK data. It must be an absolute HTTP or HTTPS URL. Normally, developers do not enter an endpoint on each placement.

If the server does not provide a valid endpoint, `GameCommerce` continues normally, while `Hybrid` cannot fall back to OpenRTB and `InGameOnly` cannot request an ad.

```csharp
using TropheeSDK.Utility;

bool configured = NetworkRequestManager.ConfigureOpenRtbEndpoint(
    "https://ads.example.com/openrtb2/auction"
);
```

## Refresh and tracking

When a response supplies a positive refresh interval, the placement applies it to its refresh manager. A viewable impression sends impression and view trackers. Interaction sends click trackers and opens the destination URL when present.

Tracker requests are skipped in the Unity Editor by default. Enable them only during deliberate integration testing:

```csharp
NetworkRequestManager.EnableOpenRtbTrackersInEditor = true;
```

## Diagnostics

```csharp
NetworkRequestManager.EnableOpenRtbLogs = true;
NetworkRequestManager.OpenRtbRequestAttempts = 3;
```

Logs cover placement mode, requested size, attempts, rendering, refresh, impressions, clicks, and endpoint validation. Request bodies may contain device or advertising identifiers, so avoid verbose logs in production.

## Troubleshooting

### The placement remains empty

* Confirm the component is `Trophee2DCampaignManager` or `TropheeSpriteCampaignManager`.
* For `InGameOnly`, verify SDK initialization supplied a valid endpoint.
* Enable OpenRTB logs and check whether all attempts returned no ad.
* Confirm the selected dimensions are supported by the demand source.

### Trackers do not fire in the Editor

This is expected. Set `EnableOpenRtbTrackersInEditor` to `true` only when you intend to send live test events.

### The Canvas placeholder changes size

`InGameOnly` uses the selected standard dimensions. Switching back to `GameCommerce` or `Hybrid` restores the recorded Game Commerce size until an OpenRTB creative is selected.
