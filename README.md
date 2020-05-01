# How does is work?
> ![](https://i.imgur.com/63S35c6.png)

The plugin uses masked materials and a material function to create a SeeThrough circle with low opacity. 
To achieve this you need to add the MF_SeeThroughFunction Function to your materials. (See [Materials-Functions](https://github.com/rootwinall/SeeThroughSystem/wiki#materials-functions) ).

Then create a masked version of your opaque material, which can also be done automatically using the CanBeMasked Component.
The **SeeThroughSystemManager** component detects the meshes that need to be set to masked, and the **CanBeMasked** component handles the rest.


# How to use :


See Preview Video here :
 
See Tutorial video here : 

Class list : 

## SeeThroughSystemManager
![](https://i.imgur.com/l2oRbL2.png)

_Parent class_ : Actor Component.

> This component must be present in the level. You can add it to the GameState, to your camera's actor, or to the PlayerController.
Only one SeeThroughSystemManager component must be added to the level.

> This component lists the actors that ought to be visible through meshes, and detects the actors that would obscure them.

 | Variable | Documentation | 
 | -------- | ------------- |
 | **Players Must Be Seen** ![](https://i.imgur.com/l4627Wk.png) | Upon activation, looks for PlayerController Pawns and automatically adds them to the list of actors that must be seen through meshes. | 
 | **Auto Activate** ![](https://i.imgur.com/fhrxsjz.png) | The component activates itself after the delay set in  **DelayBeforeAutoActivate** | 
 | **Collision Types** ![](https://i.imgur.com/haHPRkI.png) | Collisions types to detect obstacles with Capsules Traces | 
 | **Use Camera Chanel Collision** ![](https://i.imgur.com/cq7dhmD.png) | /!\ Careful /!\ Will use MultiCapsuleTraceByChannel can cause bug if there are multiple obstacles.|
| **Location Effect Offset** ![](https://i.imgur.com/H5QgqWG.png) | **Advanced**, Option: Offsets the center of the opacity circle. i.e. Center the effect around a character's head. | 
 | **Trace Capsule Radius Add** ![](https://i.imgur.com/TspF4kA.png) | **Advanced**, Option: Increases the Trace Capsules' radius. | 
|**Trace complex**  . . . . . . . ![](https://i.imgur.com/julBxty.png)| Use Complex collision |
 | **Min Alpha when hide** ![](https://i.imgur.com/dSRJIAH.png) | **Advanced**, Option: Minimal opacity limit sent to the material. | 
 | **Use Fade Opacity ?** ![](https://i.imgur.com/5rwlDdN.png) | Smooth opacity transition over time. Disable it to gain performance. | 
 | **Fade out Speed** ![](https://i.imgur.com/syUhrhJ.png) | If UseFadeOpacity? is true, will be use to put opacity to default value. | 
 | **Fade In Speed** ![](https://i.imgur.com/qH8mpuP.png) | If UseFadeOpacity? is true, will be use to put opacity to **MinAlphaWhenHide** value. | 
 | **Delay Before Auto Activate** ![](https://i.imgur.com/ChDe45F.png) | Delay in seconds before the component auto-activates.| 


 | Functions| Documentation | 
 | -------- | ------------- |
 | **Set Camera To Use** . . . ![](https://i.imgur.com/TiWNHWA.png) | Set the camera to use for trace direction. | 
 | **AddActorMustBeSeen** ![](https://i.imgur.com/ZdiugZS.png) | Add actor that must be seen. | 
 | **RemoveActorMustBeSeen** ![](https://i.imgur.com/RpbJzHV.png) | Remove actor that must be seen. | 



## CanBeMasked
![](https://i.imgur.com/yeYOUJT.png)

_Parent class_ : Actor Component.

> Add this component to all actors that are possible obstacle meshes. Manages the materials list and the masked version of that list.

> You can add the component to multiple actors with **Set Selection CanBeMasked Utility** :
![](https://i.imgur.com/egMhp9i.png)

 | Event | Documentation | 
 | -------- | ------------- |
 | **Refresh All Actors with CanBeMasked** ![](https://i.imgur.com/QHsvsa1.png) | **Call in Editor Event** Search all Actors in the level who got the CanBeMasked component and refresh their material list.| 
 | ![](https://i.imgur.com/ybjGjoN.png) | **Call in Editor Event** Refresh material list.| 

 | Variable | Documentation | 
 | -------- | ------------- |
 | **Suffix Masked asset name** ![](https://i.imgur.com/jwbSCxG.png) | Suffix to add to the current path name material to find the masked version.| 
 | **Notify Not Found Materials** ![](https://i.imgur.com/kTc6gPU.png) | Notify with a print message when the masked version of the file is missing. | 
 | **Auto Create Missing Masked Instance** ![](https://i.imgur.com/30YRd7V.png) | Auto-create Masked material asset version if missing. | 
 | **Lists of materials, Default and masked version** ![](https://i.imgur.com/QFyLy0v.png) |Auto generated, but editable after generation| 


 | Functions| Documentation | 
 | -------- | ------------- |
 | **Set Masked Version** . . . ![](https://i.imgur.com/yCK8cnp.png) | Change materials from default to masked or from masked to default. | 

## MPC_SeeThroughSystemParams
![](https://i.imgur.com/11y4uK4.png)

_Parameter collection for materials_

 | Parameters | Documentation | 
 | -------- | ------------- |
 | ![](https://i.imgur.com/7Mez4IT.png) | [ 0,1 : 0,7 ]   Sphere mask on Difference between Pixel direction to camera and center of effect direction to camera | 
 | ![](https://i.imgur.com/YK7WWTf.png) | Masked Dither opacity [ 0 - 2 ] | 

**Masked Dither opacity Example :**
![](https://i.imgur.com/YcHpRkc.png)

## Materials Functions

**MF_SeeThroughFunction**

![](https://i.imgur.com/wHrWxc0.png)

> If you use opacity in the material you can use the Opacity input to add up with the SeeThrough effect.

**MF_SeeThroughWithOpacityMaskFunction**

![](https://i.imgur.com/ufAVqDw.png)

> Same but with Opacity mask option.

**MF_SeeThroughAttributesFunction**

![](https://i.imgur.com/9ivaCEr.png)

> Same with material Attributes.

# If it not working - check list : 

* Check that MF_SeeThroughSystem is in parent material. [See Image](https://i.imgur.com/AYiTDdK.png)

* Check the actor has a CanBeMasked Component.  [See Image](https://i.imgur.com/EVWLInM.png)

* Check the masked material list is not empty or filled of none references. [See Image](https://i.imgur.com/EVWLInM.png)

* Check Mesh Profile Collision and Mesh Collision Shape.
