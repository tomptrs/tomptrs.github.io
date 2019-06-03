# Dive into my world

# Overview

This demo shows us the possibilities of configuring a 360° story.
What are we going to do:
- Make a 360° video
- Jump into your own 360° world
- Be interactive and jump from reality to virtuallity

# Make a 360° video

## Garmin Virb Camera

![alt text](images/garminvirb.jpg)

## Recording

Take the Garmin Virb camera and record your setting:

![alt text](images/garminvirbInWereld.jpg)

To start recording, you can install the Garmin Virb app on your smartphone or:
 
- Move the recording switch forward to start video recording.
- If the device is switched off, it is now switched on automatically. The device starts making video recordings immediately 
and the red light comes on.
- Set the recording switch to the rear to stop video recording.
- The video is saved on the memory card as an .mp4 file. 

## Watch the video

- Insert the memory card in the PC, and copy the video to the HD
- Open GoPro VR player
- drag & drop your video to the GoPro VR Player and view the video with the HTC VIVE VR Set.


# Enter your own world through the 360 ​​green room

- Make a recording of yourself in the green room
- Insert the memory card in the PC, and copy the video to the HD
- open adobe premiere pro

![alt text](images/workspacePremiereAanduiding.png)

- media browser: your files (videos) are listed here. Drag & drop your video file here.
- source pane: here your files are shown that are being played, and you can select effects
- program pane: Here the sequences of your clips are played
- timeline: Here you collect all your clips

By pressing the play button in the program pane you can play your video in Adobe Premiere Pro.

![alt text](images/VRToggle.png) : Door op de VR toggle knop te klikken kan je de video in 360° bekijken.


Adobe Premiere Pro has some tools available to remove your "green" from your video. Can be found in the effects 
tab (under video effects (media browser pane)). There is both color key and Ultra key. Ultra Key is the one we are 
going to use.

![alt text](images/keying.jpg)

### Step-by-step plan to use the Ultra key:

1. drag & drop the Ultra key on your video file from the timeline
2. Go to the effects control tab (in the source pane)
3. Use the eyedropper tool to select the green (test which gives the best result)
4. Use the setting option to possibly increase your effect
5. Play with the matt Generation effects until you get a solid result.


TIP:

You might get a better result by using only a part of your 360 ° footage. This can be done using a mask, and in that mask that you use ultra key effect. You can even make multiple masks!

How to make a mask:
https://helpx.adobe.com/premiere-pro/using/masking-tracking.html

Or cropping tool => filter > video > transform > cropping . use the left property)


If your green key has been removed from your footage, drag and drop your video of your world into the timeline (your green key video is at the top), and test the video in VR mode

![alt text](images/premiereTimeline.jpg)

Then you export your video and view it in the GoProVR player with the HTC Vive VR set.

![alt text](images/resultaat.PNG)

# Jump from the real world into the virtual world

Unity step-by-step plan:

- Remove the standard camera
- Add SteamVR plugin (via asset store)
- Add steamvr> core> Prefabs> Player to your scene
- Create a new material (right mouse button scene> create material)
    * The settings are:
     - shader: skybox / Panaramic
- Create a new texture (the dimensions are the same as those of your recorded film)
- go back to your material and drag your texture into it
- Create a video player in your scene, and add your video + drag your texture to the video player
- Go to windows> rendering> lighting settings and the skybox material must now be your self-made material.
- Play your unity scene.

## Input control

If you use the controller, you can change the video after e.g. a click. That way you jump from the real world into 
the virtual world :-).

- Add a new empty game object in the scene
- add a new "empty" script
- double click on the script and copy paste the code below:

## Input Script

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Video;
using Valve.VR;
using Valve.VR.InteractionSystem;

public class changeVideo : MonoBehaviour
{
    public SteamVR_Action_Boolean steamVR_Action;
    public VideoPlayer video;

    public Hand hand;

  

    private void OnEnable()
    {
        if (hand == null)
            hand = this.GetComponent<Hand>();

        steamVR_Action.AddOnStateDownListener(Down, hand.handType);
    }

    private void Down(SteamVR_Action_Boolean fromAction, SteamVR_Input_Sources fromSource)
    {
        video.url = "C:\\Users\\eaict\\Desktop\\Secundair\\Test1\\Assets\\Scenes\\2.mp4";
        Debug.Log($"Clicked button");
    }
}


```


Then click on your empty object and set the following settings:

- Steam VR action: \ actions \ default \ in \ GrabPinch
- Video: your video player
- Hand: left hand or right hand of the player


