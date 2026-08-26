# Prerequisites:

Before using Connectec RV Fallback with GAM rewarded ads, developers should configure app-ads.txt for their app.

app-ads.txt is an industry standard that lets app developers publicly declare which ad systems are authorized to sell their app inventory. For mobile apps, this is required by many demand partners and strongly recommended by Google.

### Why app-ads.txt Matters

Connected RV uses rewarded ads through GAM. For those ads to monetize reliably, buyers need to trust that the ad inventory is coming from the real app publisher.

Adding app-ads.txt helps developers:

* Protect app inventory from spoofing
* Declare Google/GAM as an authorized seller
* Improve buyer trust in the app’s ad inventory
* Reduce the chance of advertiser spend going to fake or misrepresented inventory
* Support healthier fill and monetization through authorized demand
* Avoid app-ads.txt warnings in Google AdMob or Google Ad Manager
* Make the fallback rewarded ad setup production-ready

In simple terms: app-ads.txt helps prove that the developer owns the app inventory and that Google is allowed to sell ads for it.

### Required Setup

To configure app-ads.txt, the developer must have:

* A published app on Google Play or the Apple App Store
* A developer website linked in the store listing
* Access to the website root directory
* A Google publisher ID
* The correct seller line provided by Google AdMob or Google Ad Manager

The developer website must be added to the app store listing because Google crawlers use that website to find the app-ads.txt file.
