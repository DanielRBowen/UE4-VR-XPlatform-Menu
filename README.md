# UE4-VR-XPlatform-Menu
This is a VR template for UE4 that allows gamepad and motion controller input. The game can be set up for non-vr thirdperson games too. Blueprint Virtual Reality Template for Desktop and Playstation VR. The template features a Touchscreen UI, Increment Teleport, Grabbing from a distance, Highlight, and Fist Motion Movement, a 3D Menu with Gamepad/Keyboard Navigation, Gamepad VR support, VR and Third person Modes, and Third Person Mode to First Person camera. The MotionControllerMap lets players get around around using motion controllers with Increment move, Teleport, and Fist Motion Movement.

## UE4 4.25, C++ template, Oculus supported unless modified, can support other headsets if OpenXR plugin works and is enabled

[OpenXR production ready](https://trello.com/c/p0ROFB2t) is a card for future release on the [UE4 Roadmap](https://trello.com/b/TTAVI7Ny/ue4-roadmap)

The template supports UE4 version 4.25. because the [motion controller keys were depreciated](https://docs.unrealengine.com/en-US/Platforms/VR/DevelopVR/MotionControllerKeyDeprecation/index.html) for OpenXR support, I had to convert this into a C++ template in order to access the Oculus Motion controller EKey structs so that the hands can be switched. This only supports Oculus unless you modify it yourself or the OpenXR plugin starts working and emulates the mapping to other headsets.

If you are using the UE4 launcher, put the template into UE4 by putting the FP_3D_Menu folder into: 
C:\Program Files\Epic Games\UE_4.25\Templates

<a href="https://docs.unrealengine.com/en-US/Engine/Basics/Projects/CreatingTemplates" target="_blank">See Creating Templates for help setting up.</a>

When making a new map with VRHands functionality, use the VRPawn as a pawn, place a nav mesh to allow the pawn to move. For the grabbable object highlight, place a post process volume with the Highlight material in the Post Process Materials array under Rendering Features category and make sure you have the correct rendering settings in the project settings (forward shading, vertex fogging for opaque, custom depth-stencil pass set to enabled with stencil). If you want a cursor above the grabbable object then just wire up the cursor in the highlight function of the Grabbable component.

For grabbable objects, create an actor with a Grabbable component and static mesh then set the grab kind for the Grabbable component at event begin play. See the CubeBP for example.

The project uses much of the inital VR template that comes with the Unreal Engine 4.

This uses BP from this <a href="https://youtu.be/lMieSD_7nSg" target="_blank">Arm Swinger Style Movement Tutorial for Unreal 4 video</a>.

It also uses this <a href="https://youtu.be/bWXI91FdMtk" target="_blank">Ue4 Tutorial - Moving an Object along a path using a Spline Track video</a>.

For the dynamic hands, grabbable objects and highlighting is from <a href="https://forums.unrealengine.com/development-discussion/vr-ar-development/1381972-uvrf-handpresence-template-for-rift-vive-free-shooting-range-update-1-3-laser-interactions" target="_blank">UVRF project template</a>.

It also uses this <a href="https://youtu.be/gaSGBsOsFfk" target="_blank">[ue4] - Third/First Person Smooth Camera Toggle [NEW VERSION] video</a>.

Also, this uses <a href="https://useiconic.com/icons/menu/" target="_blank">open iconic</a> for the template graphic.

Touch Screen interaction was figured out from this <a href="https://answers.unrealengine.com/questions/669917/vr-touch-screen-interaction.html" target="_blank">answer by AllJonasNeeds at UnrealEngine.com</a>.

The incremental move (forward, back, strafe right, strafe left, turn right, turn left) by throwing a ball a meter away onto the nav mesh was my work. The 3D menu widget was my work too.

There is a bug that I couldn't fix, it happens when the player does a spline move after a teleport--what happens is any CheckLineCollision function for the spline move will hit a Model Component for unknown reasons and then you would have to just use the trace end which makes it seems pointless but it works as I couldn't spline move across the box brush table.
