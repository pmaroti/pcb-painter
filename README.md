# PCB Painter

A simple single-layer PCB layout tool that runs entirely in the browser. There is no schematic: you place components by their footprint and draw copper traces between the pins.

The whole app is one self-contained file, `index.html`. Open it in Chrome, Edge or Firefox. It needs no install, no build step and no internet connection.

## Features

- **Component library** with THT and SMD footprints: resistor, diode, capacitors, LED, TO-92, pin headers, DIP-8/14, 0805, 1206, SOT-23 and SOIC-8.
- **Footprint editor**: draw your own parts. Place round, rectangular or oblong pads, with a drill size for THT or no drill for SMD. Set each pin's termination point, where traces attach, and add silkscreen lines and circles.
- **Traces** in three angle modes: any angle, 45° and 90°. The 45° and 90° modes add the corner for you. Trace width comes from a preset list or any value you type in, and traces snap to pins.
- **Grid** with presets in mm and mil, or any custom size. Snap to grid can be turned on and off.
- **Save and open** designs as plain JSON files. You can also import and export the footprint library on its own.
- **PDF export** on A4 at true 1:1 scale (vector output). Options: a mirror for toner transfer, drill-hole dots, a board outline, a 50 mm ruler for checking scale, and a separate silkscreen page.
- **English and Hungarian** user interface.
- Undo/redo, and autosave in the browser.

## Printing

Print the PDF with **Actual size / 100%** scaling, not "Fit to page". Then measure the ruler on the page to confirm it is 50 mm.

## Keyboard shortcuts

| Key | Action |
| --- | --- |
| V | Select / move |
| T | Trace tool |
| A | Cycle the trace angle mode |
| / | Flip the trace corner |
| R | Rotate |
| G | Snap on/off |
| F | Fit to view |
| Del | Delete |
| Enter, double-click, right-click | Finish a trace |
| Ctrl+Z / Ctrl+Y | Undo / redo |
| Ctrl+S | Save |

## File format

A design is a JSON file with these parts:

- `board`: the board size in mm.
- `settings`: grid, snap, trace width and angle mode.
- `library`: the footprints. Each pad has a position, shape, size, drill and termination offset, all in mm.
- `components`: placed parts, each with a footprint id, reference, position and rotation.
- `traces`: each trace has a width and a list of points.

All units are millimetres, and Y points downwards. See `examples/example-design.json`.
