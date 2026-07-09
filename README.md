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
