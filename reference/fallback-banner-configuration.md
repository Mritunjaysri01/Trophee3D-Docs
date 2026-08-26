# Fallback banner configuration reference

Fallback Banner Demand Channel configuration is exposed through `TropheeSDK.Utility.NetworkRequestManager`. Most integrations should use the endpoint delivered during SDK initialization.

{% hint style="info" %}
The current SDK retains `OpenRtb` in the following C# identifiers for backward compatibility.
{% endhint %}

| Member | Type | Purpose |
| --- | --- | --- |
| `OpenRtbEndpoint` | `string` | Current shared fallback banner endpoint. |
| `EnableOpenRtbLogs` | `bool` | Enables fallback banner diagnostics. |
| `EnableOpenRtbTrackersInEditor` | `bool` | Allows live trackers in the Unity Editor. Default: `false`. |
| `OpenRtbRequestAttempts` | `int` | Maximum attempts. Values below one are treated as one. Default: `3`. |
| `IsValidOpenRtbEndpoint(string)` | `bool` | Checks for an absolute HTTP or HTTPS URL with a host. |
| `ConfigureOpenRtbEndpoint(string)` | `bool` | Validates, normalizes, and stores the endpoint. Invalid input clears it. |
| `ClearResponseCache(string)` | `void` | Clears all cached/in-flight responses, or entries for a supplied cache key. |

## Placement helpers

`Trophee2DCampaignManager` and `TropheeSpriteCampaignManager` expose:

| Member | Purpose |
| --- | --- |
| `placementMode` | Selects `GameCommerce`, `Hybrid`, `InGameOnly`, or `RewardedVideoFallback`. |
| `bannerSize` | Selects a standard banner size. |
| `ShouldRequestOpenRtbDirectly()` | Returns `true` for `InGameOnly`. |
| `GetOpenRtbBannerDimensions()` | Returns the selected width and height as `Vector2Int`. |

Canvas placements also expose `ApplyConfiguredBannerSize(bool forceOpenRtbSize = false)`.

```csharp
using TropheeSDK.Campaigns.Manager;

Trophee2DCampaignManager placement = GetComponent<Trophee2DCampaignManager>();
placement.placementMode = Trophee2DCampaignManager.PlacementMode.Hybrid;
placement.bannerSize = Trophee2DCampaignManager.BannerSize.MediumRectangle300x250;
placement.ApplyConfiguredBannerSize();
```

{% hint style="warning" %}
Enabling Editor trackers can send real impression, view, and click events to URLs returned by an ad response.
{% endhint %}
