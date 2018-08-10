# Unity3DRuntimeTransformGizmo
A runtime transform gizmo similar to unitys editor so you can translate (move, rotate, scale) objects at runtime.

Video demonstration - https://www.youtube.com/watch?v=IUQqhS8tsNo

_________
WARNING - There is a bug in unity 5.4 and 5.5 that causes InverseTransformDirection to be affected by scale which will break negative scaling. Not tested, but updating to 5.4.2 should fix it - https://issuetracker.unity3d.com/issues/transformdirection-and-inversetransformdirection-operations-are-affected-by-scale

I have also ran into a unity bug (Unity 2017.2.0f3 (64-bit)) where when rotating a object (it was skewed, not sure if that matters) it will sometimes not have its mesh collider updated or something, causing me to not be able to click it again in certain spots until I disable and reenable the mesh collider in the inspector.
Reenabling the mesh collider also updated where unity saw the center of the object to be.
Maybe related to this bug? https://issuetracker.unity3d.com/issues/colliders-are-not-updating-to-match-attached-gameobject-location
_________

Just place the TransformGizmo on a gameobject with a camera.
Objects must have a collider on them to be selected.

Could use some work with how the moving is being handled. For example, I dont like how if you try to move something towards the camera, you cant get it to move past you to behind.

Added a pivot center mode so you can translate based on the Renderer.bounds.center instead of the normal pivot point.

Good news is that I have the code to replace using temporary parent gameobjects as a pivot with the same accuracy.
Bad news is that it seems using a parent gameobject as a pivot, even when placed at the center of the desired object, does not give the same result as unitys Center mode.
This leaves us wondering what unity is doing differently in Center mode.
Either way, I am going to completely remove the temporary gameobject since its no longer needed, as well as put 2 Scale types that people can switch between.
One scale type called "ScaleFrom" being like using a parent gameobject as a pivot, and one scale type called "ScaleFromOffset" being like unitys Center mode (though a bit inaccurate with skewed objects).

I talk about this more in this thread https://forum.unity.com/threads/scale-from-a-point-other-than-pivot-almost-working-code.544302/#post-3591286


There may also be some differences between unity and how I have things set up currently in regards to Center pivots,
such as unity seems to use colliders first to find how much weight the object has or something to decide how much it effects the center,
but for now we only look at the Renderer.bounds.center, so expect some differences between unity.

