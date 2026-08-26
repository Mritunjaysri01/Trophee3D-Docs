# 🧩 Placement Behavior :

#### 2D UI Placements

For Trophee2DCampaignManager, the SDK displays a fallback sprite inside the placement image.

The fallback sprite is selected in this order:

1. Reward sprite fetched from Trophee master data
2. Local fallback sprite&#x20;

The placement uses its existing Button interaction. When clicked, the SDK triggers the Connected RV ad.

***

#### SpriteRenderer Placements

For TropheeSpriteCampaignManager, the SDK displays the fallback sprite through the placement’s SpriteRenderer.

The placement becomes interactable through:

* Touch or click, when useTouch is enabled
* Player collision, when PlayerInteraction is enabled
* A matching PlayerTag, when collision interaction is used

The SDK also enables the placement’s BoxCollider2D so the fallback asset can receive interaction.

***

#### 3D Placements

For Trophee3DCampaignManager, the SDK does not use the fallback sprite.

Instead, it fetches a fallback reward model.

The SDK automatically configures:

* Collider
* Trigger setup
* Interaction handler
* Kinematic rigidbody
* Optional animation
* Touch or player interaction settings

If the fallback reward model cannot be fetched or instantiated, the placement is hidden and marked as deactivated.<br>
