# TropheeConnectedRV – Field Reference

Most developers do not need to call the fallback manager directly. Placement managers trigger fallback automatically.

For custom flows, you can access the manager with:

`var manager = MediationFallbackManager.EnsureInstance();`

To preload a fallback rewarded ad:

`manager.PreloadFallback(placementId);`

To manually trigger fallback:

```csharp
manager.TriggerFallback( 
placementId, 
onComplete: () => 
{ 
Debug.Log("Fallback flow completed"); 
}, 
onRewarded: reward => 
{ 
Debug.Log($"Reward received: {reward.Type} {reward.Amount}"); 
}, 
onFailed: error => 
{ 
Debug.LogWarning($"Fallback failed: {error}"); 
}, 
onShown: () => 
{ 
Debug.Log("Fallback rewarded ad shown"); 
}
);
```

***

### Callback Behavior

onShown

Called when the rewarded ad opens.

onRewarded

Called when GAM reports that the user has earned the reward.

The SDK passes:

```
public struct RewardData { public string Type; public double Amount; }
```

onComplete

Called when the rewarded ad closes, or when the fallback flow exits early.

onFailed

Called when the SDK cannot load or show the fallback ad.

Common failure values include:

```
ad_showing ad_loading adapter_null ad_not_ready mediation_manager_missing
```

GAM load errors are forwarded from the Google Mobile Ads SDK.

***

### Testing Checklist

Before release, verify the following:

* Google Mobile Ads Unity SDK is installed
* TROPHEE\_GAM\_ENABLED is present in scripting defines
* 2D fallback sprite appears correctly
* SpriteRenderer fallback interaction works
* 3D fallback reward model appears correctly
* Clicking, touching, or colliding with the fallback asset opens the rewarded ad
* Reward callbacks are received after ad completion
* Only one fallback ad can show at a time
* Placement hides or deactivates cleanly if mediation has no fill

####

#### GAM Is Not Detected

Confirm that Google Mobile Ads Unity SDK is installed and Unity has recompiled scripts.

Then check that this define exists in Player Settings:

`TROPHEE_GAM_ENABLED`

***

#### Rewarded Ad Does Not Show

Confirm that the configured GAM ad unit is a rewarded ad unit.

Also check the Unity console for the forwarded GAM load error.

***

#### Interaction Does Not Trigger Fallback

For UI placements, confirm the placement object is active and has a Button.

For SpriteRenderer placements, confirm useTouch or PlayerInteraction is enabled.

For 3D placements, confirm the fallback model has a collider and that touch or player interaction is enabled.
