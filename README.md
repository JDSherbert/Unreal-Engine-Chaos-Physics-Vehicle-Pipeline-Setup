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

To start with, make your vehicle mesh as you normally would, except the following rules must be followed:
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

