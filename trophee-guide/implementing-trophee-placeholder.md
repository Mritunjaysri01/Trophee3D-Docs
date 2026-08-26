# 👉 Implementing Trophée Placeholder

### &#x20;Trophée Placements:

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

###



<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>
