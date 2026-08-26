---
hidden: true
---

# TropheeManager

### Overview

The `TropheeManager` class is a central component of the TropheeSDK, designed to handle the initialization, positioning, and interaction of Trophee 2D /3D campaigns in Unity projects. It supports various configuration options to customize campaigns dynamically.

### Trophee Manager  Setup

The `TropheeManager` follows a singleton pattern to ensure a single instance exists throughout the application lifecycle. Place an Empty GameObject and attach TropheeManager script to it. \
It will ensure that if you call any placement from your Script execution method it would be able to ensure smooth delivery.



The manager defines several events to handle user interactions during a campaign:

* `OnTropheeAssetInteractionEvent` - Triggered when a Trophee asset is interacted with.
* `OnShareEvent` - Triggered when a share action occurs.
* `OnExploreEvent` - Triggered when an explore action occurs.
* `OnCopyEvent` - Triggered when a copy action occurs.

### Campaign Initialization Methods

#### Basic Initialization

```
public async void InitializeTropheePlacement(string gameObjectID, bool sound, bool animate, int CanvasWindowOrientation)
```

#### Initialization with Gratification Text and Interaction Callback

```
public async void InitializeTropheePlacement(string gameObjectID, string GratificationText, bool sound, bool animate, int CanvasWindowOrientation, Action onTropheeAssetInteraction)
```

#### Initialization with Gratification Text

```
public async void InitializeTropheePlacement(string gameObjectID, string GratificationText, bool sound, bool animate, int CanvasWindowOrientation)
```

### Controlling Trophee Placement

Trophee placement can be managed in two ways:

1. **Auto Mode**: The script automatically enables itself when the scene is activated.
2. **Game Logic Mode**: Developers can manually control Trophee placement by enabling the `Allow Script Execution` option and invoking Trophee functions via the `TropheeManager` API.

#### Enabling Manual Control via Game Logic

To enable scripting control, check `Allow Script Execution` in the Trophee component settings and call the desired function programmatically:

```
void Start()
{
    TropheeManager.instance.InitializeTropheePlacement("CampaignUI", "Welcome Reward!", true, true, 0);
}
```

### Hiding and Positioning Campaigns

#### Hide Campaign Placement

```
public void HideTropheePlacement(string gameObjectID)
```

#### Position Campaign Placement

```
public void PositionTropheePlacement(string gameObjectID, Vector3 AnchoredPosition)
```

### Example Use Cases

#### 1. Initializing a Campaign at Runtime

```
void Start()
{
    TropheeManager.instance.InitializeTropheePlacement("CampaignUI", true, true, 0);
}
```

#### 2. Adding a Reward Message

```
void Start()
{
    TropheeManager.instance.InitializeTropheePlacement("CampaignUI", "You've unlocked a reward!", true, true, 0);
}
```

#### 3. Reacting to an Interaction Event

```
void Start()
{
    TropheeManager.instance.InitializeTropheePlacement("CampaignUI", "Congrats!", true, true, 0, OnRewardCollected);
}

void OnRewardCollected()
{
    Debug.Log("Reward Collected!");
}
```

#### 4. Hiding a Campaign Temporarily

```
void HideCampaign()
{
    TropheeManager.instance.HideTropheePlacement("CampaignUI");
}
```

#### 5. Repositioning a Campaign UI

```
void MoveCampaign()
{
    TropheeManager.instance.PositionTropheePlacement("CampaignUI", new Vector3(100, 200, 0));
}
```

#### 6. Triggering a Share Event

```
void ShareItem()
{
    TropheeManager.instance.TriggerOnShare();
}
```

#### 7. Dynamic UI Update Based on Player Progression

```
void UpdateCampaignBasedOnProgress(int level)
{
    string rewardMessage = level > 5 ? "Special Bonus Unlocked!" : "Keep Playing for Rewards!";
    TropheeManager.instance.InitializeTropheePlacement("CampaignUI", rewardMessage, true, true, 0);
}
```

#### 8. Handling Campaigns in Different Orientations

```
void InitializeForLandscape()
{
    TropheeManager.instance.InitializeTropheePlacement("CampaignUI", "Exclusive Offer!", true, true, 0);
}

void InitializeForPortrait()
{
    TropheeManager.instance.InitializeTropheePlacement("CampaignUI", "Limited Time Bonus!", true, true, 1);
}
```

### Troubleshooting

* **GameObject Not Found**: Ensure the GameObject ID matches an existing object.
* **Missing Campaign Component**: Attach `Trophee2DCampaignManager` or `tropheeSpriteRenderer` to the GameObject.
* **Multiple Instances of TropheeManager**: Ensure there’s only one `TropheeManager` in the scene.

### Conclusion

The `TropheeManager` class streamlines the integration of Trophee 2D campaigns, offering an intuitive API for developers. By leveraging reward interactions, dynamic positioning, and event-driven architecture, this system enhances monetization and engagement strategies in Unity games.
