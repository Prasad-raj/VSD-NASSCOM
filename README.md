# Section-1: Invoking Opensource EDA, OpenLANE & SKY130 PDK:     
#### SKY130_D1_SK3_L1: OpenLANE directory structure in detail-     
   1. This step shows the directory structure of the lab.
      ```bash
      #change to OpenLANE directory
      cd Desktop/work/tools/openlane_working_dir/openlane
      
      #show the contents
      ls -ltr
      ```
      ![Screenshot (19)](https://github.com/user-attachments/assets/deed21a5-31d6-45ab-ae6b-f3541d786c2f)

     
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
      ![image](https://github.com/user-attachments/assets/186d447f-04a4-4a12-95f2-6e822747fe16)
      ![image](https://github.com/user-attachments/assets/f3f7db29-38b0-4101-a94e-7449b86d8d75)





#### SKY130_D1_SK3_L3: Review files after design prep and run synthesis-


#### SKY130_D1_SK3_L4: OpenLANE project GIT link description-


#### SKY130_D1_SK3_L5: steps to characterize synthesis results-
