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
      <img width="551" alt="1" src="https://github.com/user-attachments/assets/48e2aca3-503a-43dc-b662-190fef43a021">


     
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
      <img width="564" alt="2" src="https://github.com/user-attachments/assets/d7d04aef-4792-4523-b950-cbc92b73e95f">   
      <!--#3-->
      <img width="570" alt="3" src="https://github.com/user-attachments/assets/18eb4f43-2f92-433d-a110-9c43c4d9dbfa">

#### SKY130_D1_SK3_L3: Review files after design prep and run synthesis-
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
   <img width="692" alt="4" src="https://github.com/user-attachments/assets/fd42a2c2-a688-4324-8afb-e4257f9fa964">


              
#### SKY130_D1_SK3_L4: OpenLANE project GIT link description-
   ```bash
   #to go to the project directory provided by the efabless
      https://github.com/efabless/openlane
   ```


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

   <!--#5-->
   <img width="259" alt="5" src="https://github.com/user-attachments/assets/edf3f361-ef20-42a8-8912-3178919c5e8b">    
         check line number 13 for total cell count & line number 37 (highlighted) for total DFF count.
   
percentage of DFFs' is = 10.842968%


# Section-2: Good vs Bad floorplan and inroduction to library cells:
#### SKY130_D2_SK1_L6: Steps to run Floorplan using OpenLANE-
   before moving to the floorplan run, let's have a watch over the config files that works behind completing the flow. also, we can modify the config files according to our requirement. the config fiiles contains various switches which works to make the run work.
   ```tcl
   #the config file can be found in the following directory
      cd Desktop/work/tools/openlane_working_dir/openlane/configuration

   #now have a look at the design specific (i.e. picorv32a in this case) config files. they are located at the following directory.
      cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a
   ```
now, comeback to the run terminal and type the command-
   ```tcl
      run_floorplan
   ```
<!--6-->
   <img width="822" alt="6" src="https://github.com/user-attachments/assets/a5200548-6e02-452c-9334-3cbb876f1f70">

<!--7-->
   <img width="815" alt="7" src="https://github.com/user-attachments/assets/32fa6709-0634-4a77-8885-7f930c46ce02">



