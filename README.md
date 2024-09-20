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
   in this stage we shall record the outputs of the synthesis stage. this stage includes synthesized netlist & timing report along with the sequential cell count, ratio.
      ```
      formula for counting the sequential blocks and ratio is,
            (total number of sequntial blocks / total cell count) *$100
      ```
   in our case,    
      the total number of sequential blocks= 1613    
      total cell counts                    = 14876    
      ratio                                = (1613/14876) * 100 = 10.842968%
      <!--5-->
      <img width="259" alt="5" src="https://github.com/user-attachments/assets/207a27b7-499f-4099-8707-5e7d17d21ee4">     

# Section-2: Good vs Bad floorplan and inroduction to library cells:
#### SKY130_D2_SK1_L6: Steps to run Floorplan using OpenLANE-
   before moving to the floorplan run, let's have a watch over the config files that works behind completing the flow. also, we can modify the config files according to our requirement. the config fiiles contains various switches which works to make the run work.  
      ```
      #the config file can be found in the following directory
      cd Desktop/work/tools/openlane_working_dir/openlane/configuration
      #now have a look at the design specific (i.e. picorv32a in this case) config files. they are located at the following directory.
      cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a
      ```
      
now, comeback to the run terminal and type the command-
      ```
      run_floorplan
      ```
      <!--6-->
      <img width="822" alt="6" src="https://github.com/user-attachments/assets/cd8967ae-5d9d-45a1-a761-05d5a6264c60">     
      <!--7-->
      <img width="735" alt="7" src="https://github.com/user-attachments/assets/32fa6709-0634-4a77-8885-7f930c46ce02">

contents of the Floorplan.def file-
      ```
         #change the directory to floorplan.def
         cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_17-49/results/floorplan/
      ```
      <!--8-->
      <img width="735" alt="8" src="https://github.com/user-attachments/assets/9405005e-0d75-4928-8806-7a141836651e">


open "magic" to see the grapical representation of def-
      ```tcl

      #change the directory
      cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_17-49/results/floorplan/
      
      #use the follwing command to launch magic
      magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
      
      

diagonally placed tap cells- 
<!--10-->
<img width="735" alt="10" src="https://github.com/user-attachments/assets/fc900013-49b6-496d-9899-8f36623c271c">   

decap cells placed at the border-
<!--11-->
<img width="186" alt="11" src="https://github.com/user-attachments/assets/058ab73e-20b2-4148-8c36-97f87a07ed17">   

horizontal and vertical routing layers-
<!--12-->
<img width="735" alt="12" src="https://github.com/user-attachments/assets/610cefd3-cf3d-4cb1-8839-06e63749b22f">  
<!--13-->
<img width="735" alt="13" src="https://github.com/user-attachments/assets/e236d9f8-2471-4352-b1a6-7b17f5575a53">   










     

   






