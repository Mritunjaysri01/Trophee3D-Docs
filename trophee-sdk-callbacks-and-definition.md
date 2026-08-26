# Trophee SDK Callbacks and Definition

Below is a deeper dive into each public callback: a clear definition of when and why it fires, plus a concrete use-case illustrating how you might leverage it in your game.

***

#### 1. `OnNoInternet`

**Definition:**\
An event of type `Action` that fires any time the SDK detects there’s no network connectivity when attempting to load or refresh an ad.

**Use Case:**\
You want to gracefully handle offline scenarios—e.g. showing a placeholder UI or queuing a retry—rather than leaving the player staring at a blank spot.

```csharp
// Subscribe (e.g. in Awake)
TropheeManager.instance.OnNoInternet += HandleOffline;

// Handler
void HandleOffline()
{
    // Show a “No Connection” banner in your HUD
    offlinePanel.SetActive(true);
    // Optionally schedule a retry:
    StartCoroutine(RetryLoadAfterDelay(10));
}
```

***

#### 2. `OnTropheeGCCanvasActivated`

**Definition:**\
An `Action` invoked whenever the Trophee Game-Commerce canvas/UI (“TropheeGC”) is opened.

**Use Case:**\
Track time-on-canvas or pause underlying gameplay while the player explores brand or product details.

```csharp
TropheeManager.instance.OnTropheeGCCanvasActivated += () =>
{
    Time.timeScale = 0f;                  // Pause the game
    analytics.LogEvent("CanvasOpened");   // Fire analytics
};
```

***

#### 3. `OnTropheeGCCanvasDeactivated`

**Definition:**\
An `Action` invoked when the TropheeGC canvas closes.

**Use Case:**\
Resume gameplay or advance the player’s progress once they finish interacting with the canvas.

```csharp
TropheeManager.instance.OnTropheeGCCanvasDeactivated += () =>
{
    Time.timeScale = 1f;                  // Resume the game
    StartCoroutine(GrantCanvasReward());  // Give any earned reward
};
```

***

#### 4. `OnTropheePlacementActivated`

**Definition:**\
An `Action<string>` fired when a specific placement (2D or 3D) becomes active/visible in the scene. The string parameter is the placement’s ID.

**Use Case:**\
Begin impression tracking, log that the ad is in view, or trigger a UI animation.

```csharp
TropheeManager.instance.OnTropheePlacementActivated += placementId =>
{
    Debug.Log($"[Impression] Placement shown: {placementId}");
};
```

***

#### 5. `OnTropheePlacementDeactivated`

**Definition:**\
An `Action<string>` fired when a placement is hidden or removed from view. Payload is the placement ID.

**Use Case:**\
Stop impression tracking and log time-in-view, or free up resources tied to that placement.

```csharp
TropheeManager.instance.OnTropheePlacementDeactivated += placementId =>
{
//Call other functions 
    Debug.Log(" Placement is deactivated" );
};
```

***

#### 6. `OnTropheeAssetInteractionEvent`

**Definition:**\
An `Action<string>` invoked when the player actually interacts (e.g. taps/clicks) with the ad asset itself. Parameter is the placement ID.

**Use Case:**\
Reward the player for engagement, or route them to a product page.

```csharp
TropheeManager.instance.OnTropheeAssetInteractionEvent += placementId =>
{
    Debug.Log($"User tapped ad: {placementId}");
    RewardSystem.Grant(placementId, RewardType.Interaction);
};
```

***

#### 7. `OnShareEvent`

**Definition:**\
An `Action<string>` fired when the player taps the “Share” button within a Trophee canvas or placement. The string is the placement ID.

**Use Case:**\
Open the native share dialog, then grant a social-sharing reward upon completion.

```csharp
TropheeManager.instance.OnShareEvent += placementId =>
{
    Debug.Log($"User tapped ad: {placementId}");    
    RewardSystem.Grant(placementId, RewardType.Share);
};
```

***

#### 8. `OnExploreEvent`

**Definition:**\
An `Action<string>` fired when the player taps the “Explore” button—typically to learn more or visit a brand’s landing page.

**Use Case:**\
Launch an in-game webview or external browser, and track click-through rate (CTR).

```csharp
TropheeManager.instance.OnExploreEvent += placementId =>
{
{
    Debug.Log($"User tapped ad: {placementId}");    
    RewardSystem.Grant(placementId, RewardType.Explore);

};
```

***

#### 9. `OnCopyEvent`

**Definition:**\
An `Action<string>` invoked when the player taps “Copy”—for example, copying a promo code or link to clipboard.

**Use Case:**\
Copy the code to the clipboard and provide a “Copied!” confirmation, plus analytics.

```csharp
TropheeManager.instance.OnCopyEvent += placementId =>
{   
    Debug.Log($"User tapped ad: {placementId}");    
    RewardSystem.Grant(placementId, RewardType.Copy);
};
```

***

## Trophee trigger policy

* Default: each trigger fires once per placement per session (guarded by internal flags).&#x20;
* Allow repeats globally: call `TropheeManager.instance.SetAllowRepeatedTriggers(true);` and triggers will fire every time.
* &#x20;Allow repeat for a specific placement: call `TropheeManager.instance.ResetPlacementEventFlags(placementId);` before triggering again.&#x20;
* Affected events: OnTropheeAssetInteractionEvent, OnShareEvent, OnExploreEvent, OnCopyEvent. Usage

```csharp
// enable repeats for all placements
TropheeManager.instance.SetAllowRepeatedTriggers(true);
// OR just reset one placement’s flags before re-triggering
TropheeManager.instance.ResetPlacementEventFlags("TRO_MainMenu_Banner"); 

```

### Notes :

* When repeats are disabled (default), flags clear when the GC canvas deactivates (TriggerOnTropheeGCCanvasDeactivated) or on scene load via ResetAllEvents.&#x20;
* Keep placement IDs consistent; resets are per placement.&#x20;





**By wiring into these callbacks, you gain full control over how your game responds at every step of the Game-Commerce flow—from network errors through ad impressions to user engagement and rewards.**
