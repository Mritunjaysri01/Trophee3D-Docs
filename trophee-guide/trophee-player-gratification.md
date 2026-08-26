# 🎁 Trophée Player Gratification

TropheeSDK offers a variety of events you can subscribe to, enhancing in-game interactions and rewarding players. These events enable you to link rewards to specific actions, such as sharing, exploring, copying, and interacting with Trophee assets.<br>

## Event List :&#x20;

Below are the key events available in the **TropheeSDK.TropheeManager**:

#### 1. `OnTropheeAssetInteractionEvent`

Triggered when a player interacts with a Trophee asset.

```
public event Action OnTropheeAssetInteractionEvent;
```

#### 2. `OnShareEvent`

Triggered when a player shares an asset or content.

```
public event  Action<string> OnShareEvent;
```

#### 3. `OnExploreEvent`

Triggered when a player explores a specific area or feature.

```
public event  Action<string> OnExploreEvent;
```

#### 4. `OnCopyEvent`

Triggered when a player copies content.

```
public event  Action<string> OnCopyEvent;
```

### Usage

Developers can subscribe to these events to reward players with in-game items, XP, or currency upon interaction. Below is an example of how to use these events in Unity:

```csharp
TropheeManager.instance.OnCopyEvent +=  (placementId) =>
{
    // Reward the player with XP, coins, or in-game items
};

TropheeManager.instance.OnExploreEvent += (placementId) =>
{
    // Reward the player with XP, coins, or in-game items
};

TropheeManager.instance.OnShareEvent += (placementId) =>
{
    // Reward the player with XP, coins, or in-game items
};

TropheeManager.instance.OnTropheeAssetInteractionEvent += (placementId) =>
{
    // Reward the player with XP, coins, or in-game items
};
```

### Sample Code Implementation :&#x20;

```csharp

public class RewardHandler : MonoBehaviour
{
    private void OnEnable()
    {
        TropheeManager.instance.OnTropheeAssetInteractionEvent += OnTropheeAssetInteraction;
        TropheeManager.instance.OnShareEvent += OnShare;
        TropheeManager.instance.OnExploreEvent += OnExplore;
        TropheeManager.instance.OnCopyEvent += OnCopy;
    }

    private void OnDisable()
    {
        TropheeManager.instance.OnTropheeAssetInteractionEvent -= OnTropheeAssetInteraction;
        TropheeManager.instance.OnShareEvent -= OnShare;
        TropheeManager.instance.OnExploreEvent -= OnExplore;
        TropheeManager.instance.OnCopyEvent -= OnCopy;
    }

    private void OnTropheeAssetInteraction(string placementID)
    {
        Debug.Log("Trophee asset interacted with: " + placementID);
        // Custom behavior for asset interaction
    }

    private void OnShare(string placementID)
    {
        Debug.Log("Share action triggered for: " + placementID);
        // Custom behavior for share action
    }

    private void OnExplore(string placementID)
    {
        Debug.Log("Explore action triggered for: " + placementID);
        // Custom behavior for explore action
    }

    private void OnCopy(string placementID)
    {
        Debug.Log("Copy action triggered for: " + placementID);
        // Custom behavior for copy action
    }
}
```



### Implementation Notes

* Ensure that the reward logic is well-balanced to encourage engagement without excessive exploitation.
* These event handlers should be added during game initialization to ensure all interactions are captured.
* Remove event subscriptions appropriately to avoid memory leaks.

### Summary

By leveraging these events, developers can enhance player engagement and retention through rewards tied to meaningful interactions.&#x20;
