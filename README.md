# Section-1: Invocation of Open-source EDA, OpenLANE and Sky130 PDK         
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
   
#### SKY130_D3_SK2_L8: Lab introduction to sky130 basic layers layout and LEF using inverter-   
   2. check the layer connectivity and see what layer it is-
      <!--19-->
      <img width="755" alt="19" src="https://github.com/user-attachments/assets/b6de8ae1-5b67-489a-a106-9cf796d803c9">   
      <!--20-->
      <img width="753" alt="20" src="https://github.com/user-attachments/assets/a0257ff5-2a1a-4ee4-a0ba-a324593df7b7">   
      <!--21-->
      <img width="755" alt="21" src="https://github.com/user-attachments/assets/3b76a6f4-bc5f-4972-8b21-60303dae5e58">   

#### SKY130_D3_SK2_L9: Lab steps to create std cell layout and extract spice netlist-
   3. DRC & spice extraction-
      <!--22-->
      <img width="754" alt="22" src="https://github.com/user-attachments/assets/2e4899aa-70d2-499a-b336-9e3b57d7800c">   

      to extract the file to spice, in the tckon prompt type,
      ```tcl
      pwd
      #check the current directory

      extract all
      #this will extract the file in .ext format. then do follwing to extract the parasitics also

      ext2spice cthresh 0 rthresh 0
      #then do the following-

      ext2spice
      #this will convert the .ext to .spice file
      ```
      <!--23-->
      <img width="751" alt="23" src="https://github.com/user-attachments/assets/3ccc4563-71d4-4630-b5a7-3baceb78fc5b">   
      <!--24-->
      <img width="746" alt="24" src="https://github.com/user-attachments/assets/abba8cd7-1a73-4a97-955b-58c5418829b9">    

      looking into the .spice file-
      <!--25-->
      <img width="754" alt="25" src="https://github.com/user-attachments/assets/3d36ba27-7577-4896-a9be-152cf5020784">   

#### SKY130_D3_SK3_L1: Lab steps to create final SPICE deck using sky130 tech-
   4. update the .spice file and proceed to ngspice-
      unit box size in magic-
      <!--26-->
      <img width="755" alt="26" src="https://github.com/user-attachments/assets/f74fe0fe-1bff-4e1a-947f-d14300310727">   

      updated spice file-
      <!--27-->
      <img width="780" alt="27" src="https://github.com/user-attachments/assets/8c32a258-9e08-4fdd-b6a9-813b09d4b984">   
      <!--28-->
      <img width="770" alt="28" src="https://github.com/user-attachments/assets/6e27b4fe-c32f-49fa-9878-ef6771b1f32f">   

#### SKY130_D3_SK3_L2: Lab steps to characterize inverter using sky130 model files-
   5. invoking "ngspice" and characterize a simple inverter-
      ```tcl
      #change directory to
      cd Desktop/work/tools/openlane_work_dir/openlane/vsdstdcelldesign

      #command for ngspice
      ngspice sky130_inv.spice

      #plot the variables
      plot y vs time a
      ```
      <!--29-->
      <img width="637" alt="29" src="https://github.com/user-attachments/assets/f0f8c5d8-175c-479a-a7b3-c11c07291fe9">   
      <!--30-->
      <img width="756" alt="30" src="https://github.com/user-attachments/assets/9826edb9-221f-4354-aa5d-d8b6397b8212">    

   6. Characterization of the cell-   
      This depends on four parameters basically.
      ```
      _Rise time_- the time it takes for a signal to change from a low value to a high value.   
      _Fall time_- the time it takes for a signal to change from a high value to a low value.    
      _Cell rise delay_- Cell rise delay refers to the time it takes for the output of a cell to transition from a low voltage level (logic 0) to a high voltage level (logic 1) after a corresponding change in the input signal.       
      _Cell fall delay_- Cell fall delay is the time it takes for the output of a cell to transition from a high voltage level (logic 1) to a low voltage level (logic 0) after a corresponding change in the input signal.         
      ```
      <!--31-->
      Rise tran time= time taken for output to rise to 80% - time taken for output to rise to 20%
      ```math
      20\%\ of\ output = 660\ mv
      ```
      ```math
      80\%\ of\ output = 2.64\ v
      ```
      <img width="850" alt="31" src="https://github.com/user-attachments/assets/52a503c3-a25c-4816-8082-eb50c3f3e387">    

      ```math
      Rise\ time\ - 2.2467 - 2.1824= 0.0643/ 64.3 ps   
      ```
      Fall tran time= time taken for output to fall to 20% - time taken for output to fall to 80%       
      <!--32-->
      <img width="850" alt="32" src="https://github.com/user-attachments/assets/9be61aa3-ba61-466e-a97a-c03fdeb536ef">    

      ```math
      Fall\ time\ - 2.18 - 2.11= 0.07/ 70ps      
      ```
      Cell rise delay= time taken for output to rise to 50% - time taken for output to fall to 50%
      ```math
      50\%\ of\ 3.3\ v = 1.65\ v
      ```
      <!--33-->
      <img width="850" alt="33" src="https://github.com/user-attachments/assets/0c73e333-d6dc-4be5-8306-4f20eaa4c1ad">   

      ```math
      Cell\ rise\ delay- 2.21 - 2.14= 0.07/ 70ps        
      ```
      <!--34-->
      <img width="850" alt="34" src="https://github.com/user-attachments/assets/486c90af-2707-4429-9b64-3c440c1bb14c">   

      ```math
      Cell\ fall\ delay- 4.07 - 4.05= 0.02/ 20ps       
      ```
#### SKY130_D3_SK3_L4: Lab introduction to sky130 pdk's and steps to download labs-
   7. Tech rule check download-
      ```linux
      #follow the following web for drc rules in pdk
      https://skywater-pdk.readthedocs.io/en/main/rules/periphery.html#rules-periphery--page-root
      
      #download the tech rules from opencircuitdesign
      wget https://opencircuitdeign.com/open_pdks/archive/drc_tests.tgz

      #extract all
      tar xfz drc_tests.tgz

      #invoke magic
      magic -d XR
      ```
#### SKY130_D3_SK3_L6: Lab exercise to fix poly.9 error in sky130 tech-file-
   8. Overriding the poly rules (poly.9)-      
      incorrect poly rule implementation with no drc.    
      <!--35-->
      <img width="942" alt="35" src="https://github.com/user-attachments/assets/4524e290-f423-4ff4-ae8b-86640431a956">    

      updating the tech file for new drc update-
      <!--36-->
      <img width="941" alt="36" src="https://github.com/user-attachments/assets/267bb12a-3a41-432a-9330-698be5f797b9">   
      <!--37-->
      <img width="944" alt="37" src="https://github.com/user-attachments/assets/26c92f7d-4b59-4b31-bae0-d77f095085c1">    
      <!--38-->
      <img width="941" alt="38" src="https://github.com/user-attachments/assets/597790c9-2963-4e7e-9b09-6d2c66fb7d57">    

# Section-4: Pre-layout timing analysis and importance of good clock tree-
#### SKY130_D4_SK1_L1: Timing modelling using delay tables-
   1. Lab steps to convert grid info to track info          
      The cell characterization rules-
      ```
      * The input and output ports must lie in the intersection of the vertical and horizontal tracks.
      * Width of the standard cell should be odd multiples of the horizontal track pitch.
      * Height of the standard cell should be even multiples of the vertical track pitch.
      ```
      Now lets check if the layout is meeting the conditions or not-    
      * first see the track info-
      <!--39-->
      <img width="941" alt="39" src="https://github.com/user-attachments/assets/0ce90a60-322a-4c2b-9b1a-36411e957361">    

      ```tcl
      #change the directory to-
      cd Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/openlane/sky130_fd_sc_hd

      #see the track info
      less tracks.info
      ```
      <!--40-->
      <img width="578" alt="40" src="https://github.com/user-attachments/assets/94807443-64ad-42e3-8358-5eb3aa63ef08">   

      To check the interconnection-      
      <!--41-->
      <img width="946" alt="41" src="https://github.com/user-attachments/assets/0ac710c5-d88c-42a8-bc3d-e5e0a65ea497">    

#### SKY130_D4_SK1_L2: Lab steps to convert magic layout to std cell LEF-    
   2. Extract the LEF-     
      ```tcl
      #lef extraction command
      lef write
      ```
      <!--42-->
      <img width="942" alt="42" src="https://github.com/user-attachments/assets/629464b5-f155-4e0b-ad47-a314862ebbf8">    

   3. Add the custom cell to the picorv32a design-
      ```tcl
      # Copy lef file
      cp sky130_vsdinv.lef ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

      # List and check whether it's copied
      ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

      # Copy lib files
      cp libs/sky130_fd_sc_hd__* ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

      # List and check whether it's copied
      ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/
      ```
      <!--43-->
      <img width="767" alt="43" src="https://github.com/user-attachments/assets/88e22fa1-637c-4646-bd77-7a0506b88f00">   

   4. Edit the config.tcl file-
      ```tcl
      set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"
      set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"
      set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib"
      set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

      set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]
      ```
      <!--44-->
      <img width="555" alt="44" src="https://github.com/user-attachments/assets/1a09f6fa-3d85-4506-85ca-8eeb04914c6f">    

   5. Commands to invoke OpenLANE
      ```tcl
      #alias the following command
      alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
      
      #Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
      docker

      #We can invoke the OpenLANE flow in the Interactive mode using the following command
      ./flow.tcl -interactive

      #Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
      package require openlane 0.9

      #design preparation
      prep -design picorv32a

      # Adiitional commands to include newly added lef to openlane flow
      set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
      add_lefs -src $lefs

      #run the synthesis using the command
      run_synthesis
      ```
      <!--45-->
      <img width="835" alt="45" src="https://github.com/user-attachments/assets/482666ca-a5a4-4f42-99ac-f3e160622a83">   
      <!--46-->
      <img width="835" alt="46" src="https://github.com/user-attachments/assets/a17e24ee-94ee-4062-9b2b-5c5fcc20f629">    
      <!--47-->
      <img width="835" alt="47" src="https://github.com/user-attachments/assets/502dd589-809e-4b56-9755-89605b4f9d4c">    

#### SKY130_D4_SK1_L7: Lab steps to configure settings to fix slack and include vsdinv-
   6. Commands to change parameters to improve timing and run synthesis
      ```tcl
      # Command to display current value of variable SYNTH_STRATEGY
      echo $::env(SYNTH_STRATEGY)

      # Command to set new value for SYNTH_STRATEGY
      set ::env(SYNTH_STRATEGY) "DELAY 3"
      
      # Command to display current value of variable SYNTH_BUFFERING to check whether it's enabled
      echo $::env(SYNTH_BUFFERING)
      
      # Command to display current value of variable SYNTH_SIZING
      echo $::env(SYNTH_SIZING)

      # Command to set new value for SYNTH_SIZING
      set ::env(SYNTH_SIZING) 1
      
      # Command to display current value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not
      echo $::env(SYNTH_DRIVING_CELL)
      
      # Now that the design is prepped and ready, we can run synthesis using following command
      run_synthesis
      ```
      <!--48-->
      <img width="942" alt="48" src="https://github.com/user-attachments/assets/105da08d-4fc3-498b-8bf7-0a86d933b81c"> 
      
      Previous slack values-   
      <!--49-->
      <img width="473" alt="49" src="https://github.com/user-attachments/assets/805a7202-7d60-4f73-90a6-14841841e2f2">   
      
      Afetr running the commands-    
      <!--50-->
      <img width="938" alt="50" src="https://github.com/user-attachments/assets/68571dee-694a-46c1-aabb-42003428bc28">    

   7. Run floorplan
      since now we know that our custom cell has been added in the design and synthesis is successful, we can run floorplan
      ```tcl
      #floorplan command
      run_floorplan
      ```
      custom cell has been added-
      <!--51-->
      <img width="943" alt="51" src="https://github.com/user-attachments/assets/1b5e850b-ac3d-492b-b75e-2077fadf0832">    
      <!--52-->
      <img width="863" alt="52" src="https://github.com/user-attachments/assets/bd3fd23a-7b42-4248-83d9-a0f9f571b4ed">    

      since we are facing an unexcepted error, we need to run the following commands to tackle this-
      ```tcl
      #commands-
      init_floorplan
      place_io
      tap_decap_or
      ```
      screenshots of running the commands-     
      <!--53-->
      <img width="941" alt="53" src="https://github.com/user-attachments/assets/3070321a-bc9f-4ee1-b44b-7aa70973548c">    

      ```tcl
      #running the placement
      run_placement
      ```
      <!--54-->
      <img width="938" alt="54" src="https://github.com/user-attachments/assets/2ec8f260-8c03-4ab4-9b5b-6d709bcba0a7">    

      Load the placement .def file to magic-     
      ```tcl
      # Change directory to path containing generated placement def
      cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/23-09_04-43/results/placement/
      
      # Command to load the placement def in magic tool
      magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
      ```
      <!--55-->
      <img width="941" alt="55" src="https://github.com/user-attachments/assets/5fa3bce5-e6e3-4c19-ac05-d390ab18b73a">    

      ```tcl
      #command for tckon to viewinternal layers of the cell
      expand
      ```
      <!--56-->
      <img width="942" alt="56" src="https://github.com/user-attachments/assets/748f82b9-365a-41e7-8950-aab0009359dc">    
      
#### SKY130_D4_SK2_L3: Timing Analysis with ideal clocks using OpenSTA-
   8. Lab steps to configure OpenSTA for post-synth timing analysis
      create a file name pre_sta.conf in openlane directory
      ```tcl
      #change the directory-
      cd Desktop/work/tools/openlane_working_dir/openlane

      #create a file name pre_sta.conf
      gvim pre_sta.conf

      #add the following there
      set_cmd_units -time ns -capacitance pF -current mA -voltage V -resistance kOhm -distance um

      read_liberty -max /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib
      
      read_liberty -min /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib
      
      read_verilog /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/23-09_04-43/results/synthesis/picorv32a.synthesis.v
      
      link_design picorv32a
      
      read_sdc /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/my_base.sdc
      
      report_checks -path_delay min_max -fields {slew trans net cap input_pin}
      report_tns
      report_wns
      ```
      create a new file name my_base.sdc in picorv32a/src directory based on base.sdc file at openlane/scripts directory
      ```tcl
      #change the directrory to
      cd Desktop/work/tools/openlane_working_dir/openlane/scripts

      #copy the contents of the "base.sdc" file & change the directory to
      cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src

      #create a new file name my_base.sdc and paste the contents copied from base.sdc file
      gvim my_base.sdc

      #add the following content ahead of the file.
      set ::env(CLOCK_PORT) clk
      set ::env(CLOCK_PERIOD) 24.73
      #set ::env(SYNTH_DRIVING_CELL) sky130_vsdinv
      set ::env(SYNTH_DRIVING_CELL) sky130_fd_sc_hd__inv_8
      set ::env(SYNTH_DRIVING_CELL_PIN) Y
      set ::env(SYNTH_CAP_LOAD) 17.653
      set ::env(IO_PCT) 0.2
      set ::env(SYNTH_MAX_FANOUT) 6

      #save the file
      ```
      <!--57-->
      <img width="944" alt="57" src="https://github.com/user-attachments/assets/34ceb02f-bfe9-4ace-8489-02198870c049">   
    
      ```tcl
      #comeback to the directory
      cd Desktop/work/tools/openlane_working_dir/openlane

      #run the timing
      sta pre_sta.conf
      ```
      <!--58-->
      <img width="710" alt="58" src="https://github.com/user-attachments/assets/29c7b1bf-00ef-4c43-a743-6d5b6b110580">  
      <!--59-->
      <img width="393" alt="59" src="https://github.com/user-attachments/assets/743ddfab-5bde-4dd6-927e-ae16915c58d3">   

#### SKY130_D4_SK2_L4: Lab steps to optimize synthesis to reduce setup violations-     
   9. ECO induced for error fixing-    
      ```tcl
      #commands to see the driving strength of any net
      report_net -connections _(net_name)_
      e:g report_net -connections _13316_
      ```
      <!--60-->
      <img width="200" alt="60" src="https://github.com/user-attachments/assets/7353a4d5-472f-4a15-977f-9fe04b79a1d0">    

      in case of timing violation, try to replace the weak drive strength cells with more drive strength cells. that should give a hit on area but the slew should reduce.
      ```tcl
      # Reports all the connections to a net
      report_net -connections _(net_name)_
      
      # Replacing cell
      replace_cell _(net_name)_ (lib_cell)
      
      # Generating custom timing report
      report_checks -fields {net cap slew input_pins} -digits 4
      ```

#### SKY130_D4_SK3_L3: Clock Tree Synthesis TritonCTS and Signal Integrity-    
   10. Lab steps to run CTS using TritonCTS-
       now, we want our tool to take the new netlist post changes-
       ```tcl
       #to overwrite the synthesized netlist with the previous one
       write_verilog /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/23-09_04-43/results/synthesis/picorev32a.synthesis.v

       #now come to the openlane direcotry and run the flow again,
       cd cd Desktop/work/tools/openlane_working_dir/openlane

       # Now once again we have to prep design so as to update variables
       prep -design picorv32a -tag 23-09_04-43 -overwrite
      
       # Addiitional commands to include newly added lef to openlane flow merged.lef
       set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
       add_lefs -src $lefs
         
       # Command to set new value for SYNTH_STRATEGY
       set ::env(SYNTH_STRATEGY) "DELAY 3"
        
       # Command to set new value for SYNTH_SIZING
       set ::env(SYNTH_SIZING) 1
         
       # Now that the design is prepped and ready, we can run synthesis using following command
       run_synthesis
         
       # Follwing commands are alltogather sourced in "run_floorplan" command
       init_floorplan
       place_io
       tap_decap_or
         
       # Now we are ready to run placement
       run_placement
         
       # Incase getting error
       unset ::env(LIB_CTS)
         
       # With placement done we are now ready to run CTS
       run_cts
       ```
       <!--61-->
       <img width="937" alt="61" src="https://github.com/user-attachments/assets/014d4e0a-5f07-4eff-98c0-ad21698ca5d1">     

#### SKY130_D4_SK4_L3: Lab steps to analyze timing with real clocks using OpenSTA-      
   11. Continue with the following command to execute the cts-    
       ```tcl    
       # Command to run OpenROAD tool
       openroad
      
       # Reading lef file
       read_lef /openLANE_flow/designs/picorv32a/runs/24-03_10-03/tmp/merged.lef
      
       # Reading def file
       read_def /openLANE_flow/designs/picorv32a/runs/24-03_10-03/results/cts/picorv32a.cts.def
      
       # Creating an OpenROAD database to work with
       write_db pico_cts1.db
      
       # Loading the created database in OpenROAD
       read_db pico_cts.db
      
       # Read netlist post CTS
       read_verilog /openLANE_flow/designs/picorv32a/runs/24-03_10-03/results/synthesis/picorv32a.synthesis_cts.v
      
       # Read library for design
       read_liberty $::env(LIB_SYNTH_COMPLETE)
      
       # Link design and library
       link_design picorv32a
      
       # Read in the custom sdc we created
       read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc
      
       # Setting all cloks as propagated clocks
       set_propagated_clock [all_clocks]
      
       # Generating custom timing report
       report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4
      
       # Report hold skew
       report_clock_skew -hold
      
       # Report setup skew
       report_clock_skew -setup
      
       # Exit to OpenLANE flow
       exit
       ```
       <!--62-->
       <img width="609" alt="62" src="https://github.com/user-attachments/assets/1e366649-f650-48ae-95fb-cde54e1287a7">   
       <!--63-->
       <img width="523" alt="63" src="https://github.com/user-attachments/assets/b96d211b-8e79-49c5-b8aa-5bd6f7752a21">   

# Section-5: Final steps for RTL to GDS using trinRoute and OpenSTA-         
#### SKY130_D5_SK2_L1: Introduction to Maze Routing Lee's Algorithm-        
   1. Routing and Design rule check (DRC)-     
      ```tcl
      #to check till where you have run the flow
      echo $::env(CURRENT_DEF)

      #create pdn network
      gen_pdn
      ```
      <!--64-->
      <img width="623" alt="64" src="https://github.com/user-attachments/assets/3108d84b-bf1e-4627-bb09-87285bfd640b">  
      <!--65-->
      <img width="359" alt="65" src="https://github.com/user-attachments/assets/1cb6adc0-9d57-44bb-9bd5-6af13a6a5cbd">    

      pdn generated layout
      ```tcl
      # Change directory to path containing generated PDN def
      cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/26-09_11-02/tmp/floorplan/

      # Command to load the PDN def in magic tool
      magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read 14-pdn.def &
      ```
      <!--66-->
      pdn generation      
      <img width="944" alt="66" src="https://github.com/user-attachments/assets/7af91da5-1969-46b8-8a6f-141e86edf749">

#### SKY130_D5_SK2_L3: Basics of global and detail routing and configure TritonRoute-       
   2. Fast/ Global routing is done using FastROUTE & detailed routing is done using TritonROUTE.    
      ```tcl
      #run the placement
      run_placement
      ```
      <!--67-->
      <img width="873" alt="67" src="https://github.com/user-attachments/assets/2e7e0f9d-5c8f-4719-a318-5fd3f9df5521">   
      <!--68-->
      <img width="911" alt="68" src="https://github.com/user-attachments/assets/dccc1e61-210d-4d5d-b0b1-792aa5adb71e">     


      


      


      

      

       






       
       
       
      

      

      

      
      
      
      





      
      


      










      


      



      
      



      

      



      
      


      




      


      



   

      



     
   
      


      

   
     
      
   





   


      









   










     

   






