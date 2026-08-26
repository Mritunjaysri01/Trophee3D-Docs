# TropheeConnectedPlayer – Field Reference

#### **1. RequestAndPlayVast()**

**Description:**\
Requests the Connected Play Video (VAST Ad) assigned to the current session and begins playback if available.

**Usage:**\
Call this method when you want to trigger the playback of a VAST-based video ad linked to the player session.

**Behavior:**

* Checks if a valid VAST URL is stored in the `tropheePersistentDataManager.VideoVastUrl`.
* If valid, automatically initializes playback via `PlayVast()`.
* If no VAST URL is assigned, logs a message indicating no video is available.

**Example:**

```csharp
videoPlayerController.RequestAndPlayVast();
```

***

#### **2. StopTropheeVideoPlayback()**

**Description:**\
Stops the current Trophee video playback and hides the video container.

**Usage:**\
Call this method to completely stop playback when the ad is finished or needs to be manually terminated.

**Behavior:**

* Invokes `StopPlayback()` to stop the running video.
* Deactivates the `TropheeVideoContainer` to hide the display surface.

**Example:**

```csharp
videoPlayerController.StopTropheeVideoPlayback();
```

***

#### **3. PauseTropheeVideoPlayback()**

**Description:**\
Pauses the current video playback.

**Usage:**\
Use when you want to temporarily pause playback — for example, when the game is paused or minimized.

**Behavior:**

* Calls the internal `Pause()` method.
* Playback can later be resumed with `ResumeTropheeVideoPlayback()`.

**Example:**

```csharp
videoPlayerController.PauseTropheeVideoPlayback();
```

***

#### **4. ResumeTropheeVideoPlayback()**

**Description:**\
Resumes playback of a paused video.

**Usage:**\
Call this method to continue video playback after a pause event.

**Behavior:**

* Calls the internal `Resume()` method.

**Example:**

```csharp
videoPlayerController.ResumeTropheeVideoPlayback();
```

***

#### **5. ToggleMuteTropheeVideoPlayback()**

**Description:**\
Toggles the mute state of the current video playback.

**Usage:**\
Call this method to switch between muted and unmuted states during playback.

**Behavior:**

* Calls `ToggleMute()` to invert the current audio state.

**Example:**

```csharp
videoPlayerController.ToggleMuteTropheeVideoPlayback();
```

***

#### **6. SkipTropheeVideoPlayback()**

**Description:**\
Skips the current video playback (typically used for skippable ad formats).

**Usage:**\
Invoke this when the player chooses to skip the video or when you want to programmatically skip it after a condition is met.

**Behavior:**

* Calls `Skip()` to terminate the video playback immediately.

**Example:**

```csharp
videoPlayerController.SkipTropheeVideoPlayback();
```

***

#### **7. SetTargetRawImageTropheeVideoPlayback(RawImage targetRawImage)**

**Description:**\
Sets the `RawImage` UI component used as the video rendering target.

**Usage:**\
Use this method to dynamically assign or change the display surface where the video is rendered.

**Parameters:**

* `targetRawImage` _(RawImage)_ — The Unity UI `RawImage` component where the video will be displayed.

**Behavior:**

* Calls `SetTargetRawImage()` internally to apply the render target.

**Example:**

```csharp
videoPlayerController.SetTargetRawImageTropheeVideoPlayback(videoDisplayRawImage);
```
