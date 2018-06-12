======================================
== Alamo Object Importer 1.2        ==
==                                  ==
== by Mike Lankamp (a.k.a. Mike.nl) == 
======================================

 Introduction
==============
This importer works under 3d Studio Max 6, 8, 9 and 2013. Note that if an 
imported model has dazzles they will not be imported in 3dsmax6, 8 and 2013,
because Petroglyph's exporter for those version does not support dazzles.
Similarly, proxies will not be imported in 3d Studio Max 2013.

 Respect!
==========
With this importer comes great responsibility. Do NOT rip off other people's
work and try to pass it off as your own. Let's all work towards a friendly
community!

 Installation 
==============
* Make sure any Service Packs for your 3d Studio Max are installed.
* Make sure Petroglyph's exporter (max2alamo.dle) is placed in the "Plugins"
  folder if you want dazzles or proxies.
* Copy alamo2max.ms into the "Scripts" folder of 3d Studio max.
* Copy alamo2max.dlu for your 3dsmax version into the "Plugins" folder of
  3d Studio max.
* If using 3D Studio Max 8 on Vista, move dds.bmi and dxDDS.bmi from
  stdplugs\dxplugins\ to stdplugs\ as described in:
  http://discussion.autodesk.com/thread.jspa?threadID=509350
* After starting 3d Studio Max, open Customize > Preferences and go to the
  MAXScript tab. Set the initial heap allocation to a more comfortable amount,
  say, at least 150 MBytes. Close the preferences window.

 Usage 
=======

 Step 1: Setup
---------------
To import a model, go to the Utilities Panel (with the hamer icon), open the
MAXScript sub-panel, and click "Run Script". Select "alamo2max.ms" from the
Scripts folder. Now select "Alamo Object Importer 1.0" from the Utilities list
(you may need to explicitly click it again). If all went well, the Importer
panel should now be open.

Use the + and - buttons to add/remove texture and shader paths before
importing. The importer will look in these folders for the tga/dds files when
loading textures and fx files when creating DirectX9 materials.

* Empire at War / Forces of Corruption:
  For EaW and FoC it is recommended to extract both Textures.meg into different
  folders and then add those folders to the list (FoC first, since that
  overrides EaW textures). Add a single shader folder, identifying the shader
  sources in Mods\Source\Data\Art\Shaders in the FoC installation folder.

* Universe at War:
  For UaW you should do similarly: extract Textures.meg, add the folder and add
  the shader sources folder.

If the paths are set incorrectly, the importer will complain during import
when it cannot find textures or shaders.

Note: these paths are remembered when 3dsmax is shut down.

With the paths set, you can now import models.

 Step 2: Importing
-------------------
Click the "Import Alamo Object" button and select an ALO file to import. The
importer will also look for all .ALA files that share the same base name in the
same folder and load those as animations.

If there are already objects in the scene, the importer will ask where to
connect the imported model to. Use this to import hardpoints at their correct
spot.

The importer will read the model and animation files, create the various bones,
meshes, lights, proxies and dazzles, set their Alamo properties, connect
everything together, create materials, find textures, skin the meshes, animate
the bones and add the animations to the Alamo Utility.

If all went well, no error will be displayed. Otherwise, common errors include
having an animation which is invalid for the model file, or you did not attempt
to load a model.

The model is imported completely ready for export.

-----------------

Happy importing!


 Troubleshooting
=================

* If you want the viewports to show the models as they are in-game, you need
  to make sure 3d Studio Max runs with the Direct3D driver. Depending on your
  version of 3d Studio Max, this can be done by choosing "Change Graphics 
  Driver" from the Start Menu.

* The standard shaders as they come with Empire at War's official mod tools do
  not work out of the box with all versions of 3d Studio Max. Known issues:

  - The shader doesn't compile with error "No valid techniques found".
    This error can occur if the shader contains a fixed-function technique,
    that is, a technique with a VertexShader and/or PixelShader that is NULL.
    Remove these techniques from the file.

  - My models don't show up in the viewport.
    If, after importing, your model is there (selectable, has a bounding box,
    etc), but is just invisible even though the shader is correctly compiled,
    then the problem is that Petroglyph's shaders rely on the "m_viewProj"
    variable with VIEWPROJECTION semantics; this is not supported by 3d
    Studio Max.
    You'll have to rewrite this code to execute "mul(m_view, m_projection)"
    instead. Since I don't own the copyright on the shader code, I can't
    redistribute a fixed version of them.