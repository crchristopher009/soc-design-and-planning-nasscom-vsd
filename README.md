# Section 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK
## Lab Session 1
Section 1 tasks:-
1. Run 'picorv32a' design synthesis using OpenLANE flow and generate necessary outputs.
2. Calculate the flop ratio.
   
   Flop Ratio = (Number of D Flip-Flops) / (Total Number of Cells)
   
   Percentage of DFFs = Flop Ratio * 100
   
### 1. Run 'picorv32a' design synthesis using OpenLANE flow and generate necessary outputs
Commands to invoke the OpenLANE flow and perform synthesis
   
         # Change directory to openlane flow directory
         cd Desktop/work/tools/openlane_working_dir/openlane
         # alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
         # Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
         docker
   
         # Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
         ./flow.tcl -interactive

         # Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
         package require openlane 0.9

         # Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
         prep -design picorv32a

         # Now that the design is prepped and ready, we can run synthesis using following command
         run_synthesis

         # Exit from OpenLANE flow
         exit

         # Exit from OpenLANE flow docker sub-system
         exit

Screenshots of running each commands
   
![Screenshot 2024-10-08 203821](https://github.com/user-attachments/assets/56af8e5b-3948-47af-b3ca-8e3b5b024a3a)
   
![Screenshot 2024-10-08 203833](https://github.com/user-attachments/assets/851df45e-70c2-45c2-9304-f5e5abf198b9)
   
![Screenshot 2024-10-08 203557](https://github.com/user-attachments/assets/2c15dcc9-07d2-4d09-8bce-1b69156fc55b)

### 2. Calculate the flop ratio
   
Screenshots of synthesis statistics report file with required values highlighted
   
![Screenshot 2024-10-08 204410](https://github.com/user-attachments/assets/569e57ac-d9e5-48fe-bd0e-71414f59064d)
   
Flop Ratio = 1613/14876 = 0.108429685
   
Percentage of DFFs = 0.108429685 * 100 = 10.84296854%

# Section 2 - Good floorplan vs bad floorplan and introduction to library cells
## Lab Session 2
Section 2 tasks:-
1. Run 'picorv32a' design floorplan using OpenLANE flow and generate necessary outputs.
2. Calculate the die area in microns from the values in floorplan def.
3. Load generated floorplan def in magic tool and explore the floorplan.
4. Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.
5. Load generated placement def in magic tool and explore the placement.

      Area of die in microns = Die width in microns * Die height in microns

### 1. Run 'picorv32a' design floorplan using OpenLANE flow and generate necessary outputs.

Commands to invoke the OpenLANE flow and perform floorplan

      # Change directory to openlane flow directory
      cd Desktop/work/tools/openlane_working_dir/openlane
      
      # alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
      # Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
      docker
      # Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
      ./flow.tcl -interactive

      # Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
      package require openlane 0.9

      # Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
      prep -design picorv32a

      # Now that the design is prepped and ready, we can run synthesis using following command
      run_synthesis

      # Now we can run floorplan
      run_floorplan

Screenshots of floorplan run 

![Screenshot 2024-10-08 211739](https://github.com/user-attachments/assets/6478c678-6505-467b-8ca7-9ffae701bb63)

![Screenshot 2024-10-08 211822](https://github.com/user-attachments/assets/294a8827-9b96-4e52-9549-39952e587939)

### 2. Calculate the die area in microns from the values in floorplan def.

Screenshot of contents of floorplan def

![Screenshot 2024-10-08 212402](https://github.com/user-attachments/assets/2c5dc3bf-8330-4d1b-a226-5807cce674f8)

   1000 Unit Distance = 1 Micron 
   
   Die width in unit distance = 660685 − 0 = 660685
   
   Die height in unit distance = 671405 − 0 = 671405
   
   Distance in microns = Value in Unit Distance / 1000
   
   Die width in microns = 660685 / 1000= 660.685 Microns
   
   Die height in microns = 671405 / 1000 = 671.405 Microns
   
   Area of die in microns = 660.685 ∗ 671.405 = 443587.212425 Square Microns 

### 3. Load generated floorplan def in magic tool and explore the floorplan.

Commands to load floorplan def in magic in another terminal

      # Change directory to path containing generated floorplan def
      cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_12-06/results/floorplan/

      # Command to load the floorplan def in magic tool
      magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &

Screenshots of floorplan def in magic

![Screenshot 2024-10-08 214315](https://github.com/user-attachments/assets/7e6d5b2c-71f9-43e5-9cf3-3460a87d2d16)

Equidistant placement of ports

![Screenshot 2024-10-08 214536](https://github.com/user-attachments/assets/0e5f9de6-dc65-435a-83c2-414732952f00)

Decap Cells and Tap Cells

![Screenshot 2024-10-08 214536](https://github.com/user-attachments/assets/9e74b19b-7e6b-426b-94b2-d164de67614e)

Diogonally equidistant Tap cells

![Screenshot 2024-10-08 214827](https://github.com/user-attachments/assets/dca6702f-2516-4fc6-aa60-9273d067723b)

Unplaced standard cells at the origin

![Screenshot 2024-10-08 215015](https://github.com/user-attachments/assets/2f39f95e-0a6f-4a56-a649-8e3471411cc2)

### 4. Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.

Command to run placement

      # Congestion aware placement by default
      run_placement
      
Screenshots of placement run

![Screenshot 2024-10-08 215135](https://github.com/user-attachments/assets/01f89843-d68d-4ce7-b740-ee10ecf7e0fc)

![Screenshot 2024-10-08 215256](https://github.com/user-attachments/assets/c41196f9-cd1c-453b-a244-474a5ff55c5c)

### 5. Load generated placement def in magic tool and explore the placement.

Commands to load placement def in magic in another terminal

      # Change directory to path containing generated placement def
      cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_12-06/results/placement/

      # Command to load the placement def in magic tool
      magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &

Screenshots of floorplan def in magic

![Screenshot 2024-10-08 215349](https://github.com/user-attachments/assets/a7e73441-eac4-4cf3-bdf5-be55af243a39)

Standard cells legally placed

![Screenshot 2024-10-08 215411](https://github.com/user-attachments/assets/3793748a-e056-468d-9bf5-684926a66495)

Commands to exit from current run

      # Exit from OpenLANE flow
      exit

      # Exit from OpenLANE flow docker sub-system
      exit






   
