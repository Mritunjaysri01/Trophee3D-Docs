# Trophee Connected  :

Trophee Connected RV allows Trophee placements to continue serving a reward experience when a Trophee campaign is unavailable, returns no ad, or fails to load the required creative asset.

Instead of leaving the placement empty, the SDK displays a fallback reward asset. When the player interacts with that asset, the SDK triggers a rewarded ad through the configured mediation provider.

\
The current built-in mediation fallback provider is Google Ad Manager, using the Google Mobile Ads Unity SDK.<br>

## When Mediation Fallback Is Triggered

The SDK automatically switches a placement into fallback mode when:

* The Trophee campaign response is null
* The response type is error
* The response type is no ads or no\_ads
* A campaign response exists, but the required creative asset cannot be loaded

If a valid Trophee campaign and creative are available, the normal Trophee ad flow is used.<br>

### GAM Adapter Detection

The SDK will detect and activate the available mediation adapter.

If GAM is not available, the SDK logs a warning and disables mediation fallback.
