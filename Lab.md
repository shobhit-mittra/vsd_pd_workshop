# Lab-Work : 
This file archieves all the lab-work undertaken during the 5-Day workshop. I'm in the process of completing this file.

<br/>

<a id="day1"></a>
## Day-1 : Inception of open-source EDA. OpenLANE and Sky130 PDK :

<a id="sky_pdk"></a>
### SkyWater PDKs

We are dealing with the Skywater PDK files listed under $PDK_ROOT. For the workshop, three subdirectories are required.

![skywater PDK locations](/images/pdk_loc.png)

Evidently, there are three pdks available that can be briefly explained as follows 
- skywater pdk : Contains all the foundry provided PDK related files
- open_pdks : Contains scripts that are used to bridge the gap between closed-source and open-source PDK to EDA tool compatibility
- sky130A : The open-source compatible PDK files
<br/>

<a id="ini_ol"></a>
### Initialising OpenLANE

```
./flow.tcl -interactive 
```
- The flow.tcl is the script which runs the OpenLANE flow.
- OpenLANE can be run interactively or in autonomous mode, the `-interactive` switch allows openlane to run in interactive mode.

![Open Lane Invoking](/images/open_lane.png)
<br/>

<a id="im_pkg"></a>
### Importing Package

To operate OpenLANE, certain software dependencies are required. To add these to the OpenLANE tool, we must execute:

```
package require openlane 0.9
```

![Import Package](/images/im_pkg.png)
<br/>

<a id="des_hier"></a>
### Design Folder Hierarchy

All designs run within OpenLANE are extracted from the `openlane/designs` folder. The design hierarchy in openlane is as follows : 

![Design Hierarchy](/images/des_hier.png)


Each design hierarchy comes with two distinct components:

- Src folder : Contains verilog files and sdc constraint files
- Config.tcl files : Design specific configuration switches used by OpenLANE

An example of config.tcl is given as under :

![config.tcl](/images/config_tcl.png)
<br/>

<a id="prep_des"></a>
### Preparing Design

The command `prep` is used to generate file structure for our design. The entire command is executed as under :

```
prep -design <design_name> 
```
The argument `-design` specifies the name of design folder. In our case, `<design_name>` is `picorv32a`.

![Design Preparation](/images/design_prep.png)

Due to running the prep command, in the `picorv32a/runs` path the results and report files is created.

![Preparation Result](/images/prep_result.png)

> [!IMPORTANT]
> All of the OpenLANE parameters used for this particular run are contained in the `config.tcl` file displayed in this folder.

Additionally, the information from the technology LEF and cell LEF is combined when the design is prepared in OpenLANE. Layer definitions and a set of constrained design guidelines required for PnR flow are contained in the LEF information. To reduce DRC errors during PnR flow, the cell LEF of each standard cell carries obstruction information:

![Merged LEF](/images/merge_lef.png)
<br/>

<a id="run_syn"></a>
### Running Synthesis

Synthesis can be run using the command as under :
```
run_synthesis
```

> Minor Task provided in the lab : 
>> To find out the ratio of *flop-ratio* i.e number of d-flip-flops to number of cells. For the run we have :
>> ![Number of cells](/images/num_cells.png)
>> ###### *In the snippet above, the total number of cells are 14,876*
>> ![Numer of D-Flops](/images/num_dff.png)
>> ###### *In the snippet above, the number of d-flops are 1,613*
>>
>> Hence, the `flop-ratio` comes out to be **0.1084**.
<br/>

<a id="ol_cmd"></a>
### List of vital openLANE tool commands

In openlane it is extremely vital to follow the correct sequence of commands while operating it in `interactive` mode for proper functioning of the flow. The list below shows the command flow in openlane :

1. `prep -design <design> -tag <tag> -config <config> -init_design_config -overwrite` similar to the command line arguments, design is required and the rest is optional
2. `run_synthesis`
3. `run_floorplan`
4. `run_placement`
5. `run_cts`
6. `run_routing`
7. `write_powered_verilog` followed by `set_netlist $::env(routing_logs)/$::env(DESIGN_NAME).powered.v`
8. `run_magic`
9. `run_magic_spice_export`
10. `run_magic_drc`
11. `run_lvs`
12. `run_antenna_check`


The above commands can also be written in a file and passed to `flow.tcl`:

```
./flow.tcl -interactive -file <file>
```
<br/>

<a id="day2"></a>
## Day-2 : Floor-Planning and Introduction to Library Cells :

- In Floorplanning we typically set the:

1. Die Area
2. Core Area
3. Core Utilization
4. Aspect Ratio
5. Place Macros
6. Power distribution network (Normally done here but done later in OpenLANE)
7. Place input and output pins

<a id="fp_pl"></a>
### Viewing Floorplan and Placement Variables :

![Configuration Directory](/images/readme_loc.png)

The Floorplan and Placement variables can be seen below :

![Floor Plan Variables](/images/floorplan_vars.png)

![Placement Variables](/images/placement_vars.png)

The Floorplan defaults are as under :

![Floor Plan Defaults](/images/floorplan_defaults.png)
<br/>

<a id="run_fp"></a>
### Running Floorplan :

Floorplan can be run using the command :
```
run_floorplan
```

![Floor plan run](/images/run_floorplan.png)

We can view the results of floorplan in the directory :

![Floor Plan results](/images/post_fp_results.png)

The generated `floorplan.def` is as under :

![Floor plan.def](/images/fp_def.png)
<br/>

<a id="magic_fp"></a>
### Invoking Magic to view generated Floorplan :

In order to view the floorplan on magic, we need to locate the following components as an input to the `magic` tool :

1. Magic technology file (sky130A.tech)
2. Def file of floorplan
3. Merged LEF file

Use the command :
```
magic -T <path_tech_lef_for_magic> lef read <path_to_merged_lef> def read <floorplan.def>
```
> [!NOTE]
> For reference : In the code above, `<path_tech_lef_for_magic>` is used as `/home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic
` ; `<path_to_merged_lef>` is used as `../../tmp/merged.lef` ; `<floorplan.def>` is used as `picorv32a.floorplan.def`.

![Initializing magic tool](/images/ini_magic.png)

The magic tool shows the following floorplan : 

![Magic Floorplan](/images/magic_fp.png)
<br/>

<a id="magic_pl"></a>
### Running Placement and viewing it on magic :

Placement can be run using the command : 
```
run_placement
```

The results are populated on the `results/placement` directory and the `magic` tool can be used to investigate the result of placement stage, in a fashon similar to floorplan stage. The command used is :
```
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def  
```

The result of placement stage as constructed by the `magic` tool can be seen below :

![Placement Magic](/images/magic_placement.png)

The post placement analytics are as under :

![Design Stats](/images/design_stats_placement.png)

![Placement Analysis](/images/placement_analysis.png)

<br/>

<a id="day3"></a>
## Day-3 : Designing Library Cells using magic and ngspice tools 

<!--Thory here-->


<a id="import_inv"></a>
### Importing CMOS-Inveter Files :

The cmos inverter files are provided in the *git-hub* repositry : https://github.com/nickson-jose/vsdstdcelldesign.

Use the command below, to clone the files present in the repositry into your working machine :
```
git clone https://github.com/nickson-jose/vsdstdcelldesign
```
> [!NOTE]
> It is important that your virtual machine has git installed in it to run the command above. In case it isn't installed please run the following command before running the previous command :
> ``` sudo apt-get install git ```

It is recommended to clone the repositry in the main `openlane` directory. 

![Clonned Files result](/images/vsdstd_cell_file.png)
<br/>

<a id="magic_inv"></a>
### Inspecting CMOS-Inverter layout on magic :

Using the command as under, the magic tool can be invoked and the inverter layout can be examined. 
```
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech sky130_inv.mag
```

![Initialize Magic to examine CMOS-inv layout](/images/ini_magic_vsdcell.png)


The magic layout comes out as under :

![Magic Layout Inv cell](/images/magic_invcell.png)
<br/>

<a id="des_inf"></a>
### Design Inference :

Select the specific layer/device by hovering over the object and pressing, `s`, iteratively, until you traverse the hierarchy to the specified object:

![Inverter Cell](/images/dev_inf.png)
 
Next, on the *tkcon* terminal type `what` to reveal the selected object on the layout.

![Tkcon PMOS](/images/tkcon_pmos.png)

Additionally, **DRC-errors** can also be viewed using the tkcon terminal. 

![DRC error in tkcon](images/drc_error_check.png)
<br/>

<a id="ext_spice"></a>
### Extracting SPICE from layout :

To extract the parasitic spice file for the associated layout one needs to create an extraction file using the command `extract all`:

![Extraction File cmd](/images/tkcon_extract.png)

![Extracted File](/images/inv_extraction_file.png)

After generating the extracted file we need to output the .ext file to a spice file:

![Extract to Spice](/images/tkcon_ext2spice.png)

The created SPICE file can be seen in the `vsdcelldesign` directory 

![Spice Created in Dir](/images/spice_created.png)

![Spice img](/images/inv_spice_file.png)
<br/>

<a id="upd_spice"></a>
### Updating SPICE Deck :

The spice file generated needs some changes for proper sourcing in the ngspice tool, The updates are mentioned in the snippet as follows :

![Updated SPICE](/images/update_spice.png)
<br/>

<a id="ngspice_inv"></a>
### Running Updated SPICE on ngspice :

After updating the spice deck, we are set to source the updated spice file into the ngspice tool. Use the following command to invoke ngpsice :
```
ngspice sky130_inv.spice
```
> [!NOTE]
> In case ngspice is not installed in your machine, please run the command shown to install ngspice :
> ```sudo apt install ngspice```

![ngspice run](/images/ngspice_run.png)

Use the command `plot y vs time a` to plot a graph.

![ngspice sim](/images/ngspice_sim.png)
<br/>

<a id="day4"></a>
## Day-4 : Pre-Layout Timing Analysis

For the purpose of to perform place and routing (PnR), an abstract view of the GDS files produced by Magic is used. Information on metal and pins will be included in the abstract. Along with routing guides produced from the PnR flow, the PnR tool will do interconnect routing using the abstract view information, formally known as LEF information.

<a id="upd_inv"></a>
### Updating the inverter cell :

The tracks.info file is used to check where the routing will happen in the metal layer.

![Tracks.info file](/images/tracks_info.png)

Utilising the TCKON terminal in accordance with the tracks, update the grid in the MAGIC tool.info intel. Also, to update the width of the standard cell. Should be odd multiple of x pitch.

![](/images/grid_chg.png)

Ensure that the grid intersection is present on the input(A) and the output(Y) layout blocks :
![](/images/intersection_check.png)

Save this magic layout file using a custom name `sky130_vsdinv` and see if the changes are saved.

![](/images/updated_name_mag.png)
<br/>

<a id="gen_lef"></a>
### Generate LEF file :

Finally, we use the command `lef write` on the *tkcon* terminal to generate a `lef` file of the inverter layout that will be used in the openlane flow to plug the inverter cell in the current floorplan.

![](/images/lef_write.png)

The lef file is generated in the `vsdcelldesign` directory.

![](/images/lef_generated.png)

Now, copy the generated `sky130_inv.lef` file to the `src` directory in designs `picorv32a` directory.

![](/images/cp_to_src.png)

Additionally, copy the libraries : `sky130_fd_sc_hd__fast.lib`, `sky130_fd_sc_hd__slow.lib`, `sky130_fd_sc_hd__typical.lib` from the `libs` directory in the `vsdcelldesign` directory to `src` directory as well.

![](/images/cp_libs_to_src.png)

Check the `src` directory and make sure that all the required files above are coppied successfully. 

![](/images/cp_libs_to_src_success.png)
<br/>

<a id="prep_ol"></a>
### Preparing and Running OpenLANE flow :

Before running the openlane flow, we need to incorporate some modifications in the `config.tcl` file that is present in the `openlane` directory.

![](/images/update_config_tcl.png)

Now, we are set to invoke the openlane docker and start the flow. The initial steps of starting the flow remain the same.
> [!NOTE]
> Please refer to [Day-1 Labs](#ini_ol) to revisit the initialization steps for OpenLANE

The command `prep -design` will require certain changes. Our goal here is to overwrite the existing files present in the `runs` , from the latest run `13-08_20-12` in my case, that would be generated during the openLANE flow. The altered command used is as under :

```
prep -design picorv32a -tag 13-08_20-12 -overwrite
```

![](/images/overwrite.png)

> [!NOTE]
> If encountered by the above error, try to update the `LIB_MIN` and `LIB_MAX` in the `config.tcl` variables to `LIB_FASTEST` and `LIB_SLOWEST` respectively.
> Re-run the openlane and run the prep -design command.

![](/images/prep_resolved.png)

There is also a necessity of running the commands listed below in order to include the lef files in the openLANE flow.
```
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
```

![](/images/additional_cmds.png)

Finally, wr are all set to run synthesis via `run_synthesis` command.

![](/images/run_synthesis2.png)

Make the modifications in the flow as showm below to select a balanced area-delay synthesis strategy :

![](/images/modif_echo.png)

Now, run floorplan using the command `run_floorplan` followed by placement using `run_placement` which will place the updated inverter cell in the floorplan. Check the `results/placement` directory in the `runs/13-08_20-12` directory for the generated `def` file.

![](/images/updated_def.png)

Invoke the magic tool to view the placement ready layout using the command below :
```
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def  
```

Look thoroughly for the cell `sky130_vsdinv`. After locating the cell, hover your cursor over it and press `s` to select it. Now, type `pwd` in the *tkcon* terminal followed by `expand` command to properly view the placed cell.

![](/images/placed_inv.png)


<a id="pre_sta"></a>
### Pre-Layout STA :

After successful placement of our custom inverter cell in the floorplan layout, we embark on the path to optimize the timing performance of the overall design. This opens the gates to Static Timing Analysis which will be done by the `openSTA` tool.  

<a id="prep_sta"></a>
##### Preparing for STA 

Before proceeding to use `openSTA` for timing analysis, we require to make some modifications in the `base.sdc` file that is present in the <enter-path> directory. Appending the modifications, the `base.sdc` file is renamed as `my_base.sdc` and is copied to the `src` files in the `picorv32a` design directory.
The additional constraints that were appended to `base.sdc` are mentioned below.
```
set ::env(CLOCK_PORT) clk
set ::env(CLOCK_PERIOD) 12.000
set ::env(SYNTH_DRIVING_CELL) sky130_fd_sc_hd__inv_8
set ::env(SYNTH_DRIVING_CELL_PIN) Y
set ::env(SYNTH_CAP_LOAD) 17.65
```

![my_base.sdc image](/images/my_base_sdc.png)


> [!IMPORTANT]
> The environment variables for `synthesis`, `floorplan`, `placement` and more can be found in the `configuration` directory that is present in the `openlane_working_dir/openlane` path in the `README.md` (first mentioned in [Day-2](#fp_pl)). 

![Synthesis Environment variables](/images/readme_synthesis_vars.png)

Additionally, the inverter driving cell `sky130_fd_sc_hd_inv_8` characteristics can be found in the `sky130_fd_sc_hd__*.lib` liberty files that . The load capacitance information in the constraints above was used from the liberty files itself. 

![inv_8 information brief](/images/inv_8_cap.png)

Last but not least, since we have a modified sdc called `my_base.sdc` and have it in the `src` directory of the `picorv32a` design, we need to create a script that would be input to the sta tool and contain the data that will help the sta tool find the required files, such as sdc, liberty, reporting commands, etc. 

![pre_sta.conf script](/pre_sta_config.png)

> [!NOTE]
> The pre_sta.conf file is attached to the `main` branch of this repositry. Please take a look at it for further reference. 

<a id="inv_sta"></a>
##### Invoking OpenSTA 

Finally, use the command as below to invoke the `openSTA` tool. Pass the `pre_sta.conf` script to the tool and observe the timing reports.
```
sta pre_sta.conf
```

![running openSTA](/images/run_sta.png)
