---
hidden: true
---

# 🖼️ Trophee 2D Placements

### Reward Actions API

The manager defines several events to handle user interactions during a campaign:

* **OnTropheeAssetInteractionEvent:**\
  Triggered when a Trophee asset is interacted with.
* **OnShareEvent:**\
  Triggered when a share action occurs.
* **OnExploreEvent:**\
  Triggered when an explore action occurs.
* **OnCopyEvent:**\
  Triggered when a copy action occurs.

Each event is accompanied by a trigger method. For example:

```csharp
/// <summary>
/// Triggers the OnTropheeAssetInteractionEvent.
/// </summary>
public void TriggerOnTropheeAssetInteraction()
{
    OnTropheeAssetInteractionEvent?.Invoke();
}
```

Similarly, the methods `TriggerOnShare()`, `TriggerOnExplore()`, and `TriggerOnCopy()` invoke their respective events.

***

### Campaign Initialization Methods

The `TropheeManager` provides several overloaded methods to initialize a campaign for a target GameObject. These methods find the target by its ID and check for one of the campaign components: either `Trophee2DCamapaignManager` or `tropheeSpriteRenderer`.

#### Basic Initialization

Initializes the campaign with basic options like sound, animation, and orientation.

```csharp
csharpCopyEdit/// <summary>
/// Initializes the campaign for the GameObject with the given ID.
/// </summary>
/// <param name="gameObjectID">The ID of the GameObject.</param>
/// <param name="sound">Enable or disable sound effects.</param>
/// <param name="animate">Enable or disable animations.</param>
/// <param name="CanvasWindowOrientation">
/// The canvas window orientation (0: Landscape, 1: Portrait).
/// </param>
public async void InitializeTropheePlacement(string gameObjectID, bool sound, bool animate, int CanvasWindowOrientation)
```

#### Initialization with Gratification Text and Interaction Callback

This overload initializes the campaign and sets a gratification message. Additionally, it allows you to assign an action to be executed when the Trophee asset is interacted with.

```csharp
csharpCopyEdit/// <summary>
/// Initializes the campaign for the GameObject with the given ID and sets the gratification text.
/// </summary>
/// <param name="gameObjectID">The ID of the GameObject.</param>
/// <param name="GratificationText">The gratification text.</param>
/// <param name="sound">Enable or disable sound effects.</param>
/// <param name="animate">Enable or disable animations.</param>
/// <param name="CanvasWindowOrientation">
/// The canvas window orientation (0: Landscape, 1: Portrait).
/// </param>
/// <param name="onTropheeAssetInteraction">
/// The action to be triggered on Trophee asset interaction.
/// </param>
public async void InitializeTropheePlacement(string gameObjectID, string GratificationText, bool sound, bool animate, int CanvasWindowOrientation, Action onTropheeAssetInteraction)
```

#### Initialization with Gratification Text

This method is similar to the previous one but without an explicit interaction callback.

```csharp
csharpCopyEdit/// <summary>
/// Initializes the campaign for the GameObject with the given ID and sets the gratification text.
/// </summary>
/// <param name="gameObjectID">The ID of the GameObject.</param>
/// <param name="GratificationText">The gratification text.</param>
/// <param name="sound">Enable or disable sound effects.</param>
/// <param name="animate">Enable or disable animations.</param>
/// <param name="CanvasWindowOrientation">
/// The canvas window orientation (0: Landscape, 1: Portrait).
/// </param>
public async void InitializeTropheePlacement(string gameObjectID, string GratificationText, bool sound, bool animate, int CanvasWindowOrientation)
```

**How It Works:**

1. **Locate the TropheePlaceholder**
2. **Component Check:**\
   Determines if the target has a `Trophee2DCamapaignManager` or `tropheeSpriteRenderer` component.
3. **Configuration:**
   * Activates the target tropheeplaceholder.
   * Configures properties such as sound, animation, and orientation.
   * Optionally sets the gratification text and event callbacks.
   * Allows script execution by setting `allowScriptExecution` to `true`.
4. **Campaign Initialization:**\
   Calls `InitializeCampaign()` asynchronously to begin the campaign.

If the target tropheePlacement or required component is not found, an error message is logged.

***

### Hiding and Positioning Campaigns

#### Hide Campaign Placement

This method deactivates the campaign UI on the target GameObject.

```csharp
csharpCopyEdit/// <summary>
/// Hides the Trophee placement for the GameObject with the given ID.
/// </summary>
/// <param name="gameObjectID">The ID of the GameObject.</param>
public void HideTropheePlacement(string gameObjectID)
```

#### Position Campaign Placement

Adjusts the position of the campaign UI element. For UI components, it sets the `anchoredPosition` of the `RectTransform`, and for sprite-based elements, it sets the `position` of the `Transform`.

```csharp
csharpCopyEdit/// <summary>
/// Positions the Trophee placement for the GameObject with the given ID.
/// </summary>
/// <param name="gameObjectID">The ID of the GameObject.</param>
/// <param name="AnchoredPosition">The new position.</param>
public void PositionTropheePlacement(string gameObjectID, Vector3 AnchoredPosition)
```

***

### Example Usage

Below is a sample script demonstrating how to initialize a campaign with a gratification message and subscribe to an asset interaction event:

```csharp
using TropheeSDK;
using UnityEngine;
using System;

public class CampaignExample : MonoBehaviour
{
    private void Start()
    {
        // Example GameObject ID and configuration parameters
        string gameObjectID = "CampaignUI";
        string gratificationText = "Congratulations! You've unlocked a reward!";
        bool enableSound = true;
        bool enableAnimation = true;
        int orientation = 0; // 0 for Landscape, 1 for Portrait

        // Define the action to perform when the Trophee asset is interacted with
        Action onAssetInteraction = () =>
        {
            Debug.Log("Trophee asset was interacted with!");
        };

        // Initialize the campaign placement with a gratification message and interaction callback
        TropheeManager.instance.InitializeTropheePlacement(
            gameObjectID,
            gratificationText,
            enableSound,
            enableAnimation,
            orientation,
            onAssetInteraction
        );
    }
}
```

> **Note:**\
> Ensure that:
>
> * The `TropheeManager` instance exists in the scene.
> * The target GameObject (in this example, "CampaignUI") has a valid campaign manager component attached (either `Trophee2DCamapaignManager` or `tropheeSpriteRenderer`).

***

### Troubleshooting

* **GameObject Not Found:**\
  Verify that the GameObject ID provided to the initialization methods correctly matches an active GameObject in your scene.
* **Missing Campaign Component:**\
  Ensure the target GameObject has either the `Trophee2DCamapaignManager` or `tropheeSpriteRenderer` component attached.
* **Multiple Instances of TropheeManager:**\
  The singleton pattern prevents multiple instances. If you notice unexpected behavior, check that there is only one `TropheeManager` active in the scene.



