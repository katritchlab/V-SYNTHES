#V-SYNTHES manual 
#(Written by Dr. Arman Sadybekov)

This directory contains scripts required to run V-SYNTHES algorithm (scripts/) and two examples of Enamine REAL Space library reactions for testing purposes.  The V-SYNTHES algorithm is described in Sadybekov et al. 2021, Nature in press, see workflow in Figure 1.  The receptor model is based on CB2 receptor, as described in the paper. The reactions represent one 2-component (s11) and one 3-component (s275592) reactions. These are 2 reactions from the whole Enamine REAL Space chemical library, currently comprising more than 170 well-validated parallel synthesis reactions (for full description, check https://enamine.net/compound-collections/real-compounds/real-space-navigator). 

To run V-SYNTHES scripts and perform docking, you will need ICM-Pro+VLS license (https://www.molsoft.com/products.html). The scripts supplied here were tested with ICM-Pro+VLS version 3.9-2b on Linux, Ubuntu version 18.04.

The first step of the algorithm (preparation of example MEL libraries) has already been performed and the user may access the MEL in subdirectories of two- and three-component project libraries called files/, as well as reaction library and minimal enumeration cap library stored in REACTIONS_SYNTHONS_minimal.icb. 

To run the algorithm using the example provided, follow the instructions below. Items #1-6 correspond to Step 2 of the algorithm (MEL docking), item #7 corresponds to Step 3 (Enumeration with 2nd synthon)), and items 8-10 correspond to Step 4 of the algorithm (docking of enumerated molecules), as described in Figure 1.  Note that the 2_component and the 3_component reaction screenings are executed separately, and the 3-component one requires additional enumeration/docking step. 

To run 2_component set:  
1) copy SYNTHES_example_final_empty/2_component/first_iter to a local directory.
2) (Optional) The receptor models are provided for Cannabinoid CB2 receptor. If you wish to run screening for another receptor, delete all files in run/ subdirectory and put your ICM docking maps files (.map, .dtb etc) there instead.
3) in terminal, cd to the local directory
4) check variable icmhome_1 in the text file input_VSYNTHES.in to be the same as the ICM version used on your machine, update if needed (the scripts were tested with ICM-Pro+VLS Version 3.9-2b)
5) execute the docking launcher script: $ICMHOME/icm64 docking_launcher.icm
Once the docking is completed (about an hour using an 8-core computer for this example), analyze results of MEL:
6) in the local folder above run/, execute ICM script icm_load_hits_enamine_REAL.icm: $ICMHOME/icm64 icm_load_hits_enamine_REAL.icm. This will generate .icb file with all hits: run/processing_files/DOCKINGPROJNAME_first_iter.icb. 
7) run enumeration script icm_enumerate_REAL_frags.icm. Once done, a directory run/processing_files/enumerated_best_frags_RECEPTORNAME_300000/ will appear with the .sdf files of enumerated best fragments
8) create new docking project directory. Put all the scripts from the scripts/ directory of the original distributive inside this directory and create two empty subdirectories: files/ and run/
9) copy the .sdf files from step (8) to files/ folder inside the new docking project. After that, execute indexer.icm script: $ICMHOME/icm64 indexer.icm
10) Repeat steps 2-6 in the new docking project directory. The .icb file obtained at the end of step 6 will contain the top scoring compounds from the example reaction of the Enamine REAL Space library. 

To run 3-component set: 
 1) copy SYNTHES_example_final_empty/3_component/first_iter to a local directory.
Executing the items #2-10 are identical to the 2-component reaction. After finishing #2-10, repeat #7-10 for partially enumerated compounds to fully enumerate them and obtain the final docking results.





