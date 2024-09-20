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
   <img width="233" alt="5" src="https://github.com/user-attachments/assets/02c5b9b0-e78f-47ac-a949-31c49c618279">
   
percentage of DFFs' is = 10.842968%

