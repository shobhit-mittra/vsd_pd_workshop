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
  > 
- Covering the pre-placed cells using `de-coupling capacitors`
- Defining power grid for the floorplan : `Power Planning`
- I/O Pad placement
- `Macro` placement
- Defining `logical blockages` in and around i/o pad area


