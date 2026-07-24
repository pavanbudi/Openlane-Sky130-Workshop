# Introduction to OPENLANE

You will be inside home directory initially

<img width="723" height="482" alt="Screenshot 2026-07-09 150052" src="https://github.com/user-attachments/assets/f983e51e-37b4-4c14-a351-0b73439d65c6" />

* Now move to `work/tools/` as our required files are in these folder 
* Now enter `ls -ltr` to list all files inside folder

<img width="732" height="495" alt="Screenshot 2026-07-09 150812" src="https://github.com/user-attachments/assets/d7613cec-ee5c-44b0-9598-5c0dbe21e715" />

* Lets find what is in pdk

  <img width="822" height="197" alt="Screenshot 2026-07-09 155445" src="https://github.com/user-attachments/assets/3881be36-6a65-4496-8ea6-7e811d3898ca" />

 * `skywater -pdk` , it is folder which has all `pdk` related files like `timing libraries` , `les files` , `tech lef files`
 * Basically pdk files `skywater files` i.e., any of foundry files. It is made compatible to work with commercial EDA tools not for open source EDA tools.
 * `open_pdks` mitigate that issue and there are certain files that convert foundry pdks to be compatible with open source EDA tools
 * `sky130A` is a pdk that is made compatible to work in opensource environment

 * Let's see what is inside it

      <img width="853" height="642" alt="Screenshot 2026-07-09 160729" src="https://github.com/user-attachments/assets/8cd28dc1-f94b-4d8f-9114-73127055e8e8" />

* `libs.tech` folder contain all technology specific files whereas `libs.ref` folder contain files specific to the tool

* Lets see what is inside `sky130_fd_sc_hd`

  <img width="988" height="268" alt="Screenshot 2026-07-09 161945" src="https://github.com/user-attachments/assets/d8915b4f-5f87-4b5f-ab6d-5f80860a9dd5" />

* It has all technology files like `techlef` contains layer information, if we go into `lib` file

 <img width="990" height="417" alt="Screenshot 2026-07-09 162354" src="https://github.com/user-attachments/assets/adc25064-277b-4395-8e7b-e7cc26ac4f14" />

 * We can see all timing files which are defined for many of PVT corners
 * Lets go to `openlane` directory by invoking it, we will be working in it

 <img width="1042" height="222" alt="Screenshot 2026-07-20 124559" src="https://github.com/user-attachments/assets/0f4b18a4-76e0-469a-a226-214dfe8421bf" />

 * Now enter `docker` as it gives ready-to-use virtual environment with all the complex OpenLANE tools already installed, saving you from installation headaches.
 * Next `pwd` is entered to check present directory(print working directory)

<img width="881" height="416" alt="image" src="https://github.com/user-attachments/assets/21ca1532-baf7-4eb7-9d06-5844baa58552" />

* `flow.tcl`, it says how flow has to go and we do `-interactive` session( complete flow will be executed if we won't use this as openlane is automated flow from RTL to GDS) as we want to know which stage is doing what and comparing results

  <img width="695" height="275" alt="Screenshot 2026-07-20 130502" src="https://github.com/user-attachments/assets/f0193200-21c2-477b-a6b4-e929aadab995" />

  * Now we input all packages that are required to run the flow
  
    <img width="653" height="275" alt="Screenshot 2026-07-20 131755" src="https://github.com/user-attachments/assets/073b766a-cb72-4347-b0f4-c2afaa49d94d" />

  * All designs that are runned by openlane can be extracted from `design` folder(which has more than 100 designs)
 
    <img width="850" height="335" alt="Screenshot 2026-07-20 132030" src="https://github.com/user-attachments/assets/405d77de-552e-4eb5-a236-4d41deed11aa" />

* lets go into picorv32a folder

<img width="1135" height="155" alt="Screenshot 2026-07-20 132143" src="https://github.com/user-attachments/assets/c5fb9fc4-54d5-4bf2-8768-9057d5c2d14e" />

* `src` stands for source file where verilog and sdc files are present and `config` file bypasses any configuration that is done already into openlane (allows us in rewriting default values already present in openlane)

* lets see what is inside `config` file

  <img width="1073" height="242" alt="Screenshot 2026-07-20 133327" src="https://github.com/user-attachments/assets/d87c7079-acf9-4286-8371-62877478345e" />

* order of openlane taking values is:
  1-> default value then 2-> `config` file values then at final `sky130A_sky130..` values

<img width="1270" height="165" alt="Screenshot 2026-07-20 133816" src="https://github.com/user-attachments/assets/3514a80d-d918-4a92-9a27-ff3c28b0c1ba" />

* the values in this file are taken finally

  <img width="562" height="313" alt="Screenshot 2026-07-20 133912" src="https://github.com/user-attachments/assets/cd309383-f555-4b75-8fa8-c6cd6e956972" />


* Now we need to run synthesis but before that a design setup stage is required to prepare file system and data structures as design directory only contains the three base files/folders (src, config.tcl, and the PDK config). The OpenLane flow requires a structured file system where each consecutive step can predictably fetch and store files from specific locations. The preparation stage builds this necessary directory layout.
* It can de done in following way

<img width="890" height="550" alt="Screenshot 2026-07-21 105956" src="https://github.com/user-attachments/assets/9812210e-a3e4-4664-a515-4e4e854a448c" />


* Once the command runs, the first process that occurs is a script called `mergeLef.py.10`
How and Why: This script merges two distinct LEF (Library Exchange Format) files—the cell-level LEF (`macro.lef`) and the technology-level LEF(`tech.lef`)—into a single, unified file.11
The Purpose: Merging them ensures that when OpenLane runs its subsequent steps, it does not have to access two separate files to look up cell-level information and layer-level information simultaneously; it can fetch everything from one place.

* Now lets check any new file is created in design directory

  <img width="970" height="326" alt="Screenshot 2026-07-21 112535" src="https://github.com/user-attachments/assets/52f514d2-f4cd-4693-9c53-75036da1eae9" />

* Next step is synthesis. This runs `yosys`(process input design files and translate the register-transfer level (RTL) code into a gate-level representation) and `ABC` logic synthesis tool(perform logic optimisation and map the generic gates to the specific technology library cells provided by the PDK).

  <img width="840" height="557" alt="Screenshot 2026-07-21 120947" src="https://github.com/user-attachments/assets/a6741d44-e345-42c1-b4ce-013f98e74da8" />

* Now we have to find flop ratio equal to ratio of D-flip flops to cells

  <img width="501" height="615" alt="Screenshot 2026-07-23 140125" src="https://github.com/user-attachments/assets/1cdc9f08-8f1f-4bd6-a449-8d4b8fd07508" />

<img width="612" height="258" alt="Screenshot 2026-07-23 140356" src="https://github.com/user-attachments/assets/ea51009a-04cc-4b16-9d98-285f13db5a64" />

* Now lets check result files are created or not , observe netlist created as shown in image at bottom line, similarly you can also check timing reports also

  <img width="883" height="238" alt="Screenshot 2026-07-23 140536" src="https://github.com/user-attachments/assets/4a047466-744d-4d07-b788-d20c4cb0b2ee" />

# Floorplanning

* Opealane has lot of switches to adjust flow direction. Lets look at them first

  <img width="961" height="291" alt="Screenshot 2026-07-24 150324" src="https://github.com/user-attachments/assets/7e7b55cb-a9e6-4949-ac20-cca3971c21fa" />

* If you open it,you can see variables required for each stage(these are the switches). Now lets see where these are set

  <img width="1100" height="110" alt="Screenshot 2026-07-24 150924" src="https://github.com/user-attachments/assets/e6805a58-8246-451d-8916-9cb79de3a7db" />

* It has default values set for floorplan

  <img width="785" height="703" alt="Screenshot 2026-07-24 151001" src="https://github.com/user-attachments/assets/6658262e-818f-487e-8364-106917e61157" />


* Now lets run floorplan

  <img width="870" height="537" alt="Screenshot 2026-07-24 151502" src="https://github.com/user-attachments/assets/88a7e1f9-9615-4787-8848-f2c77faa915a" />

* Now like synthesis , lets see what are the files created

  <img width="882" height="301" alt="Screenshot 2026-07-24 151914" src="https://github.com/user-attachments/assets/36723fd5-1a85-462b-9b55-bacd56fe9054" />

* Lets open `config.tcl` which tells all configurations that are taken by flow(type SHIFT+g for going to end of page)
