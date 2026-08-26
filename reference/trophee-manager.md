# Trophee Manager

Below is a reference guide to all of TropheeManager’s public callbacks (events), query methods (returning `bool`), and key public methods—complete with signatures, descriptions, and usage examples in C#.

***

### Callbacks (Events)

You can subscribe to these events to react to Trophee lifecycle and user-interaction events:

| Event                            | Signature              | Description                                                                   |
| -------------------------------- | ---------------------- | ----------------------------------------------------------------------------- |
| `OnNoInternet`                   | `event Action`         | Fired when the SDK detects no network connectivity.                           |
| `OnTropheeGCCanvasActivated`     | `event Action`         | Fired when the in-game “TropheeGC” canvas is opened.                          |
| `OnTropheeGCCanvasDeactivated`   | `event Action`         | Fired when the “TropheeGC” canvas is closed.                                  |
| `OnTropheePlacementActivated`    | `event Action<string>` | Fired when a placement becomes active / visible; payload is the placement ID. |
| `OnTropheePlacementDeactivated`  | `event Action<string>` | Fired when a placement is hidden; payload is the placement ID.                |
| `OnTropheeAssetInteractionEvent` | `event Action<string>` | Fired once per placement when the user interacts with the ad asset.           |
| `OnShareEvent`                   | `event Action<string>` | Fired once per placement when the user taps “Share.”                          |
| `OnExploreEvent`                 | `event Action<string>` | Fired once per placement when the user taps “Explore.”                        |
| `OnCopyEvent`                    | `event Action<string>` | Fired once per placement when the user taps “Copy.”                           |

#### Example: Subscribing to Events

```csharp
void Start()
{
    var mgr = TropheeManager.instance;
    mgr.OnNoInternet += HandleNoInternet;
    mgr.OnTropheePlacementActivated += id => Debug.Log($"Placement shown: {id}");
    mgr.OnTropheeAssetInteractionEvent += id => Debug.Log($"Asset interacted: {id}");
}

void HandleNoInternet()
{
    // Show offline UI
    Debug.LogWarning("No internet connection – cannot load Trophee ads.");
}
```

***

### Query Methods (`bool`)

Use these to test SDK state before taking action:

| Method                                 | Signature                       | Description                                                                |
| -------------------------------------- | ------------------------------- | -------------------------------------------------------------------------- |
| `IsAdCached(string placementId)`       | `bool IsAdCached(string)`       | Returns `true` if an ad has already been fetched & cached for that ID.     |
| `IsPlacementReady(string placementId)` | `bool IsPlacementReady(string)` | Returns `true` if the cached ad data, icon sprite, etc., are fully loaded. |

#### Example: Checking Readiness

<pre class="language-csharp"><code class="lang-csharp"><strong>string placementId = "Banner_01";
</strong>if (TropheeManager.instance.IsPlacementReady(placementId))
{
    TropheeManager.instance.InitializeTropheePlacement(placementId);
}
else
{
    Debug.Log("Waiting for ad to finish loading...");
}
</code></pre>

***

### Core Public Methods

#### Initialization & Registration

<pre class="language-csharp"><code class="lang-csharp"><strong>// Ensure a singleton exists in the scene (calls Awake if needed)
</strong>TropheeManager.EnsureTropheeManagerExists();

// If you’re creating placements dynamically:
TropheeManager.instance.RegisterPlacement(myPlacementMonoBehaviour);
</code></pre>

#### Showing / Hiding Placements

<pre class="language-csharp"><code class="lang-csharp"><strong>// Show with optional parameters:
</strong>//   placementID, GratificationText, sound, animate, canvas orientation, onInteract callback
TropheeManager.instance.InitializeTropheePlacement(
    placementID: "Banner_01",
    GratificationText: "You earned 10 points!",
    sound: true,
    animate: false,
    CanvasWindowOrientation: 0,
    onTropheeAssetInteraction: id => Debug.Log($"User tapped {id}")
);

// Hide again when you want to remove it:
TropheeManager.instance.HideTropheePlacement("Banner_01");
</code></pre>

#### Positioning

```csharp
// Move a 2D RectTransform or 3D transform into a new anchored position
Vector3 newPos = new Vector3(100, 200, 0);
TropheeManager.instance.PositionTropheePlacement("Banner_01", newPos);
```

#### Reward Customization

```csharp
// Change the reward sprites & values on demand
TropheeManager.instance.ModifyRewardValues(
    placementID:        "Banner_01",
    shareRewardSprite:  myShareSprite,
    exploreRewardSprite: myExploreSprite,
    copyActionSprite:   myCopySprite,
    shareReward:        5,
    exploreReward:      10,
    copyActionReward:   2
);
```

#### Cache Management

```csharp
// Manually clear a cached ad if you want to force a re-fetch:
TropheeManager.instance.ClearCachedAd("Banner_01");

// Directly access cached data (e.g. to read ad JSON, icon, etc.):
var data = TropheeManager.instance.GetCachedAdData("Banner_01");
```

#### Placement Lookup

```csharp
// Get a reference to the placement component itself:
var bannerMgr = TropheeManager.instance.GetPlacement<Trophee2DPlacementManager>("Banner_01");
bannerMgr.SomePublicProperty = ...;
```

###

***

### Complete Usage Example

```csharp
public class AdController : MonoBehaviour
{
    private const string placementId = "LevelPlacement";

    void Awake()
    {
        TropheeManager.EnsureTropheeManagerExists();
        var mgr = TropheeManager.instance;
        mgr.OnTropheePlacementActivated += id => Debug.Log($"Shown: {id}");
        mgr.OnShareEvent += id => Debug.Log($"Shared: {id}");
        mgr.OnNoInternet += () => Debug.Log("Offline – retry later.");
    }

    void Start()
    {
        TryShowAd();
    }

    async void TryShowAd()
    {
        // wait for the SDK to load initial data...
        while (!TropheeManager.instance.IsPlacementReady(placementId))
        {
            await Task.Delay(100);
        }
        TropheeManager.instance.InitializeTropheePlacement(
            placementId,
            GratificationText: "Thanks for watching!",
            sound: true,
            animate: true,
            CanvasWindowOrientation: 1,
            onTropheeAssetInteraction: id => Debug.Log($"User interacted with {id}")
        );
    }

    public void OnUserClosesAd()
    {
        TropheeManager.instance.HideTropheePlacement(placementId);
    }
}
```

***

Keep this guide handy when integrating TropheeManager in your game—for subscribing to events, checking readiness, showing/hiding placements, and customizing rewards.
