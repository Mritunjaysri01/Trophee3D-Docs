# 👉 Setting up Trophée Placement via your game logic

Another way to integrate the Trophée solution is through game logic and scripting.

Follow these steps to load the Trophée solution:



<details>

<summary>Add Placement Objects</summary>



* Add `Trophee2DPlacement` or `Trophee3DPlacement` inside your game and define its position.
* You can also use the method calls available in `TropheeManager` to adjust the **size, scale, and position** of these placements dynamically.

</details>

<details>

<summary><strong>Add Trophée Manager to Your Scene</strong></summary>

Include the `TropheeManager` component in your game scene. Add a Empty GameObject and attach TropheeManager script to it.

</details>

<details>

<summary><strong>Configure the Trophée Manager</strong></summary>

* When script execution is enabled, you can control that specific placement from the Trophy Manager.
* The name of each placement serves as a **campaign ID**, allowing you to reference and control them within your scripts.

</details>

<details>

<summary>Enabling Manual Control via Game Logic</summary>

To enable scripting control, check `Allow Script Execution` in the Trophee component settings and call the desired function programmatically:

```
void Start()
{
    TropheeManager.instance.InitializeTropheePlacement("CampaignUI", "Welcome Reward!", true, true, 0);
}
```

</details>

<details>

<summary>Hiding and Positioning Campaigns</summary>

#### Hide Campaign Placement

```
public void HideTropheePlacement(string gameObjectID)
```

#### Position Campaign Placement

```
public void PositionTropheePlacement(string gameObjectID, Vector3 AnchoredPosition)
```

</details>

<details>

<summary>Example Use Cases</summary>

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

</details>

<details>

<summary>Troubleshooting</summary>

* **GameObject Not Found**: Ensure the GameObject ID matches an existing object.
* **Missing Campaign Component**: Attach `Trophee2DCampaignManager` or `tropheeSpriteRenderer` to the GameObject.
* **Multiple Instances of TropheeManager**: Ensure there’s only one `TropheeManager` in the scene

</details>



By following these steps, you can seamlessly integrate and control Trophée placements through your game's logic, ensuring flexibility and dynamic positioning for in-game commerce experiences.
