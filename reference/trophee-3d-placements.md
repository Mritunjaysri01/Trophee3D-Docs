---
hidden: true
---

# 🧊 Trophee 3D Placements

#### **Method: `InitializeThreeDAdModel` (Overload 1)**

**Description:**

Initializes a 3D ad campaign model, enabling sound effects and animations, and setting the canvas window orientation.

**Syntax:**

```csharp
public void InitializeThreeDAdModel(int CampaignID, bool sound, bool animate, int CanvasWindowOrientation)
```

**Parameters:**

* **CampaignID** (`int`): The ID of the 3D campaign to be initialized. Must be within the bounds of the `threeDCampaigns` list.
* **sound** (`bool`): Enables or disables sound for the 3D campaign.
* **animate** (`bool`): Enables or disables animation for the 3D campaign.
* **CanvasWindowOrientation** (`int`): The orientation of the ad model in the canvas window (e.g., `0` for landscape, `1` for portrait).

**Example:**

```csharp
TropheeManager.instance.InitializeThreeDAdModel(2, true, true, 0);  // Initializes the 3D ad with sound, animation, and in landscape mode
```

**Remarks:**

* The campaign model is made visible by setting `gameObject.SetActive(true)`.
* The method begins the initialization of the model via a coroutine (`InitializeModel`).
* If the provided `CampaignID` is out of bounds, an error is logged:\
  `"CampaignID is out of bounds"`.

***

#### **Method: `InitializeThreeDAdModel` (Overload 2)**

**Description:**

Initializes a 3D ad campaign model with custom player tag, enabling sound effects and animations.

**Syntax:**

```csharp
public void InitializeThreeDAdModel(int CampaignID, string PlayerTag, bool sound, bool animate)
```

**Parameters:**

* **CampaignID** (`int`): The ID of the 3D campaign to be initialized. Must be within the bounds of the `threeDCampaigns` list.
* **PlayerTag** (`string`): The tag to identify the player or object interacting with the ad.
* **sound** (`bool`): Enables or disables sound for the 3D campaign.
* **animate** (`bool`): Enables or disables animation for the 3D campaign.

**Example:**

```csharp
TropheeManager.instance.InitializeThreeDAdModel(3, "Player1", true, false);  // Initializes the 3D ad with player tag, sound, and no animation
```

**Remarks:**

* The campaign model is made visible by setting `gameObject.SetActive(true)`.
* The method begins the initialization of the model via a coroutine (`InitializeModel`).
* If the provided `CampaignID` is out of bounds, an error is logged:\
  `"CampaignID is out of bounds"`.

***

#### **Method: `InitializeThreeDAdModel` (Overload 3)**

**Description:**

Initializes a 3D ad campaign model with custom gratification text, enabling sound effects and animations.

**Syntax:**

```csharp
public void InitializeThreeDAdModel(int CampaignID, bool sound, bool animate, string GratificationText)
```

**Parameters:**

* **CampaignID** (`int`): The ID of the 3D campaign to be initialized. Must be within the bounds of the `threeDCampaigns` list.
* **sound** (`bool`): Enables or disables sound for the 3D campaign.
* **animate** (`bool`): Enables or disables animation for the 3D campaign.
* **GratificationText** (`string`): The text to be displayed as gratification or reward.

**Example:**

```csharp
TropheeManager.instance.InitializeThreeDAdModel(4, true, true, "Congratulations!");  // Initializes the 3D ad with sound, animation, and gratification text
```

**Remarks:**

* The campaign model is made visible by setting `gameObject.SetActive(true)`.
* The method begins the initialization of the model via a coroutine (`InitializeModel`).
* If the provided `CampaignID` is out of bounds, an error is logged:\
  `"CampaignID is out of bounds"`.

***

#### **Method: `HideThreeDAd`**

**Description:**

Hides a 3D ad campaign model, effectively deactivating its visibility in the scene.

**Syntax:**

```csharp
public void HideThreeDAd(int CampaignID)
```

**Parameters:**

* **CampaignID** (`int`): The ID of the 3D campaign to be hidden. Must be within the bounds of the `threeDCampaigns` list.

**Example:**

```csharp
TropheeManager.instance.HideThreeDAd(1);  // Hides the specified 3D ad model
```

**Remarks:**

* The campaign model is made invisible by setting `gameObject.SetActive(false)`.
* If the provided `CampaignID` is out of bounds, an error is logged:\
  `"CampaignID is out of bounds"`.

***

#### **Method: `PositionThreeDAd`**

**Description:**

Positions a 3D ad campaign model by setting its position to the specified transform.

**Syntax:**

```csharp
public void PositionThreeDAd(int CampaignID, Transform ModelPosition)
```

**Parameters:**

* **CampaignID** (`int`): The ID of the 3D campaign to be positioned. Must be within the bounds of the `threeDCampaigns` list.
* **ModelPosition** (`Transform`): The transform containing the desired position for the 3D model.

**Example:**

```csharp
TropheeManager.instance.PositionThreeDAd(1, someTransform);  // Moves the 3D ad to the specified position
```

**Remarks:**

* If the provided `CampaignID` is out of bounds, an error is logged:\
  `"CampaignID is out of bounds"`.
