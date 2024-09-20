# Section-1: Invoking Opensource EDA, OpenLANE & SKY130 PDK:     
#### SKY130_D1_SK3_L1: OpenLANE directory structure in detail-     
   1. This step shows the directory structure of the lab.
      ```bash
      #change to OpenLANE directory
      cd Desktop/work/tools/openlane_working_dir/openlane
      
      #show the contents
      ls -ltr
      ```
      <!--#1-->
      <img width="735" alt="1" src="https://github.com/user-attachments/assets/48e2aca3-503a-43dc-b662-190fef43a021">    
     
#### SKY130_D1_SK3_L2: Design preparation steps-
   2. now alias the docker and invoke the tools.
      ```tcl
      #alias the following command
      alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
      
      #Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
      docker

      #We can invoke the OpenLANE flow in the Interactive mode using the following command
      ./flow.tcl -interactive

      #Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
      package require openlane 0.9

      #Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
      prep -design picorv32a

      ```
      <!--#2-->
      <img width="735" alt="2" src="https://github.com/user-attachments/assets/d7d04aef-4792-4523-b950-cbc92b73e95f">   
      <!--#3-->
      <img width="735" alt="3" src="https://github.com/user-attachments/assets/18eb4f43-2f92-433d-a110-9c43c4d9dbfa">

#### SKY130_D1_SK3_L3: Review files after design prep and run synthesis-
   3. now run the synthesis step.
      ```tcl
      #to run the synthesis
      run_synthesis

      #to exit from openLANE
      exit

      #to exit from the docker
      exit

      #every results, logs will be stored in the following directory
      cd Desktop/work/tools/openlane_woring_dir/openlane/designs/picorv32a/runs
      ```
      <!--4-->
      <img width="692" alt="4" src="https://github.com/user-attachments/assets/2ebdd100-2103-4c7c-8e79-c61ca51bb17c">     
      
#### SKY130_D1_SK3_L5: steps to characterize synthesis results-
   4. familiarizing with post-synth collaterals-
      ```tcl
      #formula for calculating the sequential block ratio in a design-
      (Total number of sequential blocks/ total cell count) * 100
      ```
      In our case,   
         Total number of DFF's=1613   
         Total number of cells=14876   
         Ratio = (1613/14876) * 100 = 10.84296%       
   
      <!--5-->
      <img width="259" alt="5" src="https://github.com/user-attachments/assets/207a27b7-499f-4099-8707-5e7d17d21ee4">     

# Section-2: Good vs Bad floorplan and inroduction to library cells:
#### SKY130_D2_SK1_L6: Steps to run Floorplan using OpenLANE-
   










     

   






