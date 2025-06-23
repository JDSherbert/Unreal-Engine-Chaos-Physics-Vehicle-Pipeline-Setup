![image]()

# Unreal Engine Guide: How To Setup Vehicles with Chaos Physics

<!-- Header Start -->
<a href = "https://docs.unrealengine.com/5.3/en-US/"> <img height="40" img width="40" src="https://cdn.simpleicons.org/unrealengine/white"> </a> 
<a href = "https://learn.microsoft.com/en-us/cpp/c-language"> <img height="40" img width="40" src="https://cdn.simpleicons.org/blender"> </a>
<img align="right" alt="Stars Badge" src="https://img.shields.io/github/stars/jdsherbert/JDSherbert-Repo-Template?label=%E2%AD%90"/>
<img align="right" alt="Forks Badge" src="https://img.shields.io/github/forks/jdsherbert/JDSherbert-Repo-Template?label=%F0%9F%8D%B4"/>
<img align="right" alt="Watchers Badge" src="https://img.shields.io/github/watchers/jdsherbert/JDSherbert-Repo-Template?label=%F0%9F%91%81%EF%B8%8F"/>
<img align="right" alt="Issues Badge" src="https://img.shields.io/github/issues/jdsherbert/JDSherbert-Repo-Template?label=%E2%9A%A0%EF%B8%8F"/>
<img align="right" src="https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2FJDSherbert%2FJDSherbert-Repo-Template%2Fhit-counter%2FREADME&count_bg=%2379C83D&title_bg=%23555555&labelColor=0E1128&title=🔍&style=for-the-badge">
<!-- Header End --> 

-----------------------------------------------------------------------

<a href="https://docs.unrealengine.com/5.3/en-US/"> 
  <img align="left" alt="Unreal Engine Guide" src="https://img.shields.io/badge/Unreal%20Engine%20Guide-black?style=for-the-badge&logo=unrealengine&logoColor=white&color=black&labelColor=black"> </a>
<a href="https://docs.unrealengine.com/5.3/en-US/"> 
  <img align="left" alt="Blender Guide" src="https://img.shields.io/badge/Blender%20Guide-black?style=for-the-badge&logo=blender&logoColor=white&color=black&labelColor=orange"> </a>
  
<!-- <a href="https://choosealicense.com/licenses/unlicense/"> 
  <img align="right" alt="License" src="https://img.shields.io/badge/License%20:%20Unlicense-black?style=for-the-badge&logo=unlicense&logoColor=white&color=black&labelColor=black"> </a> -->
  
<br></br>

-----------------------------------------------------------------------
## Overview
Some words about the project here-


-----------------------------------------------------------------------
 ## Using Blender

FTo start with, make sure the units Blender is using are correct for Unreal. If this isn't done correctly, you may encounter scaling issues later.
These are the correct settings for Blender's units.

![image](https://github.com/user-attachments/assets/7bebccfb-ff9e-4793-b8a3-4ac43c628dcb)

Now, make your vehicle mesh as you normally would, except the following rules must be followed:
- +X is always forward (thanks, Unreal)
  
  ![image](https://github.com/user-attachments/assets/1f57ed00-a30f-4a16-bfec-344cf6b03b8b)

- The vehicle mesh body should be inside an empty container, with all position, scale and rotation applied and at 0. You can apply transforms with `Ctrl+A`.
  
![image](https://github.com/user-attachments/assets/26fe3c90-d7b9-4c9c-a82d-edc6df888db1)

- The wheels should be children of the body. If you accidentally modelled the wheels as part of the body, you can select one of the vertices on the wheels, and hit `Ctrl+L` to auto grab the related vertices, and press `P` to seperate the mesh.
  
![image](https://github.com/user-attachments/assets/437df3c7-bd0d-4e37-bf13-c39dd283b7f9)


- Make sure to name the mesh and mesh containers appropriately as these are going to be our only references when importing into unreal. Here is a good example of a good naming convention:
  
![image](https://github.com/user-attachments/assets/09de1184-90b4-4c41-9eaa-6d5ce345774b)

- Note that the wheels should *really* follow the naming convention of FR (Front Right), FL (Front Left), BR (Back Right), BL (Back Left) because it will be important for setting up offsets/sockets.

- Make sure the wheels have the origins in the center of the wheel (the little yellow dot).
  
![image](https://github.com/user-attachments/assets/e3cb4e94-84a4-49e2-885c-1982d594e789)

- If the origin is not centered, you can select the wheel mesh, and hit `Shift+Ctrl+Alt+C` to set the origin to the center of mass (volume) which should work for most cases.
  
![image](https://github.com/user-attachments/assets/59e1d74e-e25f-41db-9999-2eb6fcf86058)

-----------------------------------------------------------------------
 ## Exporting From Blender

 Once you are happy with everything, head to the export (fbx) option.
 
![image](https://github.com/user-attachments/assets/c3fa27a3-d768-41ba-b61f-4dcbdfcf9009)

These are the export options you'll want for the best results in Unreal Engine.

![image](https://github.com/user-attachments/assets/c53099ba-de1d-47ca-b7cb-a3983e15643f)

Make sure you export into a folder in your Unreal Engine project's Content folder.

-----------------------------------------------------------------------
 ## Importing Into Unreal Engine

Once you've exported an .fbx file from Blender into an Unreal Engine Content folder, the engine will detect that there has been a source change and ask you to import via a popup.

![image](https://github.com/user-attachments/assets/8cd1b434-a0ae-4072-9933-4d39a788dfa3)

Choose "Import" here, and scroll down to find the option that says "Force All Mesh As Type" - by default, it will be set to "None" as Unreal can't find a skeleton/armature, so it'll assume you're importing a static mesh.
This couldn't be further from the truth, we've technically set this up by parenting our body mesh to our wheels.
Change this option to force Skeletal Mesh import.

![image](https://github.com/user-attachments/assets/5aceac73-1f1e-4b8c-bf3b-c2f0c6d9f72a)

After it has imported, you'll see a Skeleton, Skeletal Mesh, and Physics Asset, along with any materials and textures you added in Blender in your Content folder.

![image](https://github.com/user-attachments/assets/e8c75310-cb68-4c4d-b496-e71c5ad47e7d)

The first thing to do is head to the physics asset, and the likelihood is that it will be all wrong and everything will be capsules.

![image](https://github.com/user-attachments/assets/1577a20c-2d0c-4fd6-ab1c-bc65201fadd9)

You'll need to manually edit the physics assets here, I'd recommend replacing the capsules on the wheels with spheres, and either a box or single convex hull for the body. Click "Generate" as required.

![image](https://github.com/user-attachments/assets/36a40cf6-b543-4da2-930d-f72dec785a25)

Be aware that particularly strange meshes may require some tinkering with boxes etc to get the right collision setup, and you can have multiple colliders on a single mesh as required, as Unreal fails to recognize what the mesh is.

Next, we want to create an AnimBP for this skeleton. 

![image](https://github.com/user-attachments/assets/b3d485dd-9588-4799-9ad8-9362e1357bfc)

There's a special setup that comes for free by default in the Vehicle Template for the engine, so we'll grab that. Reparent this `AnimationInstance` class to a `VehicleAnimationInstance` class.

![image](https://github.com/user-attachments/assets/a007e694-09fa-4a19-bb90-71b250cbff6d)

This now gives us access to the Wheel Controller node for our Animation Blueprint. This will animate the wheels spinning and steering left/right.
Your setup should look something like this:

![image](https://github.com/user-attachments/assets/8fc06e01-22e0-4f8e-be1a-6602f999ab6d)

Now create a Blueprint and use the template's `Vehicle Pawn` class as the parent. We'll go into this template and make some changes to use our new vehicle.
First off, we'll want to set it to use our new Animation Blueprint.

![image](https://github.com/user-attachments/assets/5af185ef-f018-4b40-aa98-30c96d6df087)

Now, we want to select our skeletal mesh we imported so that we can get our physics.

![image](https://github.com/user-attachments/assets/e9408212-137f-456d-8c1d-f49b7c3f924a)

*Just in case you run into some confusion, the Template actually hides the skeletal mesh from being rendered. It is actually there!*

![image](https://github.com/user-attachments/assets/e1a8b84d-fb48-4e19-9e99-7fae7b17aef5)

Now we want to head to the `Vehicle Movement Component`, and this is where the naming conventions you used in the Blender project are really important.
You'll need to now assign each wheel and make sure it is socketed to the body of the car.
*Don't get confused - the Body is the correct choice, as the other similar option is the container I used to define the Vehicle's root position.*

![image](https://github.com/user-attachments/assets/a45c5758-b44c-4bed-8fea-0ee84d9cb85b)

![image](https://github.com/user-attachments/assets/d00d0301-4e58-40d8-a95a-38c373539231)

Now, with all that done, we need to create a static mesh for the body and wheels. Unfortunately they will all be bundled together if we do it in the Skeleton Asset.
I like to open File Explorer and drag and drop the .fbx we exported from Blender into a different folder. Instead of choosing the Skeletal Mesh option, you can leave it as `None` or choose `Static Mesh`.
*Make sure to import to a different folder than the one the Skeletal Mesh is in, otherwise it will just override it!*

![image](https://github.com/user-attachments/assets/4b5b48c9-aded-4265-93b4-16a04d07f58c)

I like to import all of it into a parent folder, and then `Advanced Copy` it to the child folder so that it overrides the references to the materials and textures nicely.
The Skeletal Mesh and The Static Mesh are considered completely different objects by Unreal, so don't worry about those clashing.

![image](https://github.com/user-attachments/assets/8b721741-99c7-438a-9450-cf2784efe045)

![image](https://github.com/user-attachments/assets/363b13be-b426-4b06-9171-eeaf058fa76b)

Now we need to open the Static Mesh assets so we can handle the collisions. Don't worry this is a lot easier than the Skeletal Mesh one.
Firstly, use the drop down to show the simple collision meshes.

![image](https://github.com/user-attachments/assets/8b9e0509-4d1a-47c2-bb67-7bba513ea335)

Then select it and delete it.

![image](https://github.com/user-attachments/assets/11213a9e-c308-45dc-a395-09252679fcab)

Take a look at the complex collision mesh and make sure it is okay, and if so, you can save that. We'll also need to repeat this process for the wheels.

![image](https://github.com/user-attachments/assets/65097b94-33af-4eb0-9154-56281b7bbae7)

Now you should have the correct Static Mesh assets to finish off the Blueprint.
Again, *make sure everything is socketed to the vehicle Body!*

![image](https://github.com/user-attachments/assets/cfe8f4ea-7288-4f83-b689-baf7fb2e92f1)

That should be it!
