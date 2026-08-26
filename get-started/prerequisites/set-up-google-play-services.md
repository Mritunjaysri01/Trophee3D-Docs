# Set up Google Play services

## Step-by-Step Instructions

1. Open Your Unity Project \
   • Open your Unity project in Unity Editor.<br>
2. Locate or Create the mainTemplate.gradle File\
   &#x20;• Navigate to the Assets/Plugins/Android directory. \
   &#x20;• If you already have a mainTemplate.gradle file, you can skip to step 4. \
   • If you do not have a mainTemplate.gradle file, follow the next steps to create one.<br>
3. Enable Custom Gradle Template • Go to Edit > Project Settings > Player. \
   • Select the Android tab. \
   • Expand the Publishing Settings section. \
   • Check the Custom Main Gradle Template option. This will generate a mainTemplate.gradle file in the Assets/Plugins/Android directory.<br>
4. Edit the mainTemplate.gradle File \
   • Open the mainTemplate.gradle file in a text editor.\
   • Locate the dependencies block in the file. \
   • Add the following line inside the dependencies block:

```
dependencies {
    implementation 'com.google.android.gms:play-services-ads-identifier:18.0.1'
}
```

5. Save the mainTemplate.gradle File \
   • Save the changes to the mainTemplate.gradle file.<br>
6. Resolve Android Dependencies \
   • Go to Assets > External Dependency Manager > Android Resolver > Resolve. \
   • This will download and integrate the required Google Play services libraries into your Unity project.&#x20;

## Summary

To add the Google Play services ads identifier dependency to your Unity project:

* **If you have a `mainTemplate.gradle` file:** Add the dependency within the dependencies block.
* **If you don't have a `mainTemplate.gradle` file:** Enable the custom Gradle template in Unity's Player settings and then add
