#Section-1: Invoking Opensource EDA, OpenLANE & SKY130 PDK-
##SKY130_D1_SK3_L1: OpenLANE directory structure in detail-
 Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

 alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
 Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker
