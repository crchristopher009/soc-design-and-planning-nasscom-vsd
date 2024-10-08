# Section 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK
## Lab Session 1
Section 1 tasks:-
1. Run 'picorv32a' design synthesis using OpenLANE flow and generate necessary outputs.
2. Calculate the flop ratio.
   
   Flop Ratio = (Number of D Flip-Flops) / (Total Number of Cells)
   
   Percentage of DFFs = Flop Ratio * 100
   
### 1. Run 'picorv32a' design synthesis using OpenLANE flow and generate necessary outputs.
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




   
