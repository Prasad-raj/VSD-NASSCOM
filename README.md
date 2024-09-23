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
      <img width="650" alt="1" src="https://github.com/user-attachments/assets/48e2aca3-503a-43dc-b662-190fef43a021">    
     
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
      <img width="650" alt="2" src="https://github.com/user-attachments/assets/d7d04aef-4792-4523-b950-cbc92b73e95f">   
      <!--#3-->
      <img width="650" alt="3" src="https://github.com/user-attachments/assets/18eb4f43-2f92-433d-a110-9c43c4d9dbfa">

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
      <img width="650" alt="4" src="https://github.com/user-attachments/assets/2ebdd100-2103-4c7c-8e79-c61ca51bb17c">     
      
#### SKY130_D1_SK3_L5: steps to characterize synthesis results-
   4. flop ratio calculation-
      ```tcl
      #formula for calculating the sequential block ratio in a design-
      (Total number of sequential blocks/ total cell count) * 100
      ```
      In our case,   
         Total number of DFF's=1613   
         Total number of cells=14876   
         Ratio = (1613/14876) * 100 = 10.84296%       
   
      <!--5-->
      <img width="350" alt="5" src="https://github.com/user-attachments/assets/207a27b7-499f-4099-8707-5e7d17d21ee4">     

# Section-2: Good vs Bad floorplan and inroduction to library cells:
#### SKY130_D2_SK1_L6: Steps to run Floorplan using OpenLANE-
   1. Floorplan Running (picorv32a)-
      ```tcl
      #after the design preparation, run floorplan-
      run_floorplan
      ```
      <!--6-->
      <img width="650" alt="6" src="https://github.com/user-attachments/assets/a01f8ad5-636a-4da7-844a-f26ef96207ba">  
      
      <!--7-->
      <img width="650" alt="7" src="https://github.com/user-attachments/assets/4379c205-e32d-45d3-bba5-1850bd725403">   

   2. snapshot of .def file from floorplan
      ```tcl
      #change directory to-
      cd Desktop/work/tools/openlane_woring_dir/openlane/designs/picorv32a/runs/19-09_17-49/results/floorplan
      ```
      <!--8-->
      <img width="368" alt="8" src="https://github.com/user-attachments/assets/e5dae2f8-f228-4846-afa0-434d7dd51666">  

   3. visualize the .def file in magic
      ```tcl
      #stay at the directory-
      cd Desktop/work/tools/openlane_woring_dir/openlane/designs/picorv32a/runs/19-09_17-49/results/floorplan

      #invoke magic along with desired def file-
      magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
      ```
      <!--9-->
      <img width="650" alt="9" src="https://github.com/user-attachments/assets/422e1b6d-f78d-4d7b-a40f-4da0aa4f3846">     

      Tap-cells placement-
      <!--10-->
      <img width="650" alt="10" src="https://github.com/user-attachments/assets/36cea24c-707e-47d6-8672-cfab01bed00f">    

      Decap cells placement-
      <!--11-->
      <img width="186" alt="11" src="https://github.com/user-attachments/assets/bcebce3e-eb79-4872-957f-b159416c76f4">    

      Horizontal & Vertical Trace-
      <!--12-->
      <img width="650" alt="12" src="https://github.com/user-attachments/assets/01c277c8-1cf7-4ac6-b0a8-1c1b98dd63c4">    
      <!--13-->
      <img width="650" alt="13" src="https://github.com/user-attachments/assets/157632e7-8f88-440b-a64a-654acca51acb">    

#### SKY130_D2_SK2_L5: congestion aware placement using RePlAce-
   4. Running the placement-
      <!--14-->
      <img width="551" alt="14" src="https://github.com/user-attachments/assets/cba9a8c9-1c6b-4489-b451-f63819c2a048">   

      seeing the placement def using magic-
      <!--15-->
      <img width="755" alt="15" src="https://github.com/user-attachments/assets/8676b04f-66bc-4e7d-a8bb-1fadb7bbf054">   
      <!--16-->
      <img width="755" alt="16" src="https://github.com/user-attachments/assets/5280ba28-6df9-46a0-966b-a025e4a5e197">   

# Section-3: design library cell using Magic layout and ngspice characterization-   
#### SKY130_D3_SK1_L5: Lab steps to git clone vsdstdcelldesign-    
   1. clone the git repo for std cell characterization-
      ```tcl
      #change to the openlane directory
      cd Desktop/work/tools/openlane_work_dir/openlane

      #clone the following repo there
      git clone https://github.com/nickson-jose/vsdstdcelldesign.git
      ```
      <!--17-->
      <img width="749" alt="17" src="https://github.com/user-attachments/assets/11880cf9-c17b-4da8-837f-6c5b5caf99b2">   
      <!--18-->
      <img width="756" alt="18" src="https://github.com/user-attachments/assets/a7538706-9f37-42f2-aeed-c915a562168b">    





   


      









   










     

   






