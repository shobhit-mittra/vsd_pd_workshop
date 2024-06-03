## Day-2 : Floor-Planning and Introduction to Library Cells

This segment involves getting started with the physical design flow. `Floorplan` stage marks the beginning of the PD flow and it's also known as design planning, 
although prior to floorplan certain sanity checks are performed in order to validate the quality of constraints and netlist provided by the design team. This analysis is 
termed as `Netlist QA` or netlist quality analysis. The primary motive of Netlist QA is to spot any possible flaws in the netlist and the constraints and report 
them back to the synthesis team for corrections. Flagging any preliminary issues is crucial as debugging them becomes increasingly costly in terms of time and 
effort as they propagate deeper into the flow. Constraint validation can be performed by *Synopsys* tool named <br/> `Galaxy Constraints Analyser` (GCA)<br/>

<a id="chip_fp"></a> 
### Chip Floorplan Considerations :

Post Netlist QA and sanity checks floorplan can be done. This stage can itself be divided into smaller steps that are roughly as follows :

- Defining `Aspect Ratio` (Height and width of core and die area) :
  > Finding the optimal dimmensions of core and die (`Apect Ratio = Height/Width of core`) requires understanding of the area occupied by the cells in the netlist. `Utilisation factor` is an important factor to consider which essentially captures the ratio of total area occupied by the netlist to total core area. Conventionally, the utilisation factor is decided to be close to *50-60%* or *0.5-0.6* so that during placement optimisation stages and routing there is enough room for the additional cells and routes in the floorplan. This decision helps the PD team to arrive at an optimal aspect ratio.
- Locating and deciding the positions of `Pre-placed cells` if any
  > Pre-placed cells typically include analog blocks, hard IP's, memory blocks. Say there exists a combinational cloud, as shown below, that consits of good amount of gate instances (50k-100k instances). These can be divided further by using cuts (cut1 and cut2 in the figure) for simplicity. These cells are generally sensitive to noise or are critical in nature hence they need to be placed before the automated placement of standard cells in the placement stage.
  > ![Pre-Placed Cells example](/images/theory/pre_place_cells1.png) <br/>
  > In case of replicating and re-using the logic, they can be `black-boxxed` and used as modules further in the design.
  > ![Pre-Placed cells example 2](/images/theory/pre_place_cells2.png)
- Covering the pre-placed cells using `de-coupling capacitors`
  >
- Defining power grid for the floorplan : `Power Planning`
- I/O Pad placement
- `Macro` placement
- Defining `logical blockages` in and around i/o pad area


