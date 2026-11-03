# PCB Painter

A simple single-layer PCB layout tool that runs entirely in the browser. There is no schematic: you place components by their footprint and draw copper traces between the pins.

The whole app is one self-contained file, `index.html`. Open it in Chrome, Edge or Firefox. It needs no install, no build step and no internet connection.

## Features

- **Component library** with 96 built-in footprints, sorted into categories (RCL, Diodes, Transistors, ICs, Modules, Connectors, Other) and split into SMD, THT and SM4THT under each category:
  - **ICs:** DIP-8 to DIP-40 (300 and 600 mil), SMD DIP (gull-wing) 8 to 40 pins, SOIC-8/14/16, SOIC-16W/20W/28W, MSOP-8, TSSOP-8/14/16/20, TQFP-32/44/48/64, LQFP-100, QFN-16/20/32, SOT-23-5/6.
  - **Transistors:** TO-92 (2.54 and 1.27 mm), TO-18, TO-126, TO-220 (vertical and lying), TO-247, SOT-23, SOT-323, SOT-143B, SOT-103 (X-package), SOT-89, SOT-223, DPAK and D2PAK.
  - **RCL:** capacitors at 100, 200, 300, 400 and 500 mil pitch; electrolytic capacitors from D4 to D16 mm; axial resistors at 300, 400, 500 and 600 mil; standing resistors at 100 and 200 mil; 0805 and 1206; SM4THT resistors and capacitors at 200, 300, 400 and 500 mil. SM4THT parts are through-hole parts whose leads are bent and soldered onto surface pads, so they have no drill holes.
  - **Diodes:** axial at 300, 400 and 500 mil; standing at 100 and 200 mil; 5 mm LED.
  - **Modules:** Raspberry Pi Pico, Waveshare RP2040-Zero and ESP32-C3 SuperMini, soldered on with pin headers.
  - **Connectors:** pin headers.

  The new package dimensions are typical values. Check them against the datasheet before you make a board.
- **Library window** (L or the Library button): a search box that is focused when the window opens and suggests matches as you type, a category tree below it, and a footprint preview beside the tree. From there you can place, edit, copy or delete a component.
- **Footprint editor**: draw your own parts. Place round, rectangular or oblong pads, with a drill size for THT or no drill for SMD. Set each pin's termination point, where traces attach, and add silkscreen lines and circles.
- **Traces** in three angle modes: any angle, 45° and 90°. The 45° and 90° modes add the corner for you. Trace width comes from a preset list or any value you type in, and traces snap to pins.
- **Copper polygons** (P): filled copper areas drawn with the same angle modes as traces. They have no automatic clearance, so leave gaps around pads yourself.
- **Copper text** (X): bold text on the copper layer, mirrored by default so it reads correctly from the copper side. You can set its height, rotate it and switch mirroring off.
- **Mirrored components** (M): SMD parts are mirrored automatically when you place them, because they sit on the copper side. You can mirror any part while placing it or afterwards, and traces stay attached to its pins.
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
| P | Copper polygon tool |
| X | Copper text tool |
| L | Open the component library |
| M | Mirror the selected component or text (also while placing) |
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
- `components`: placed parts, each with a footprint id, reference, position, rotation and mirror flag.
- `traces`: each trace has a width and a list of points.
- `polys`: copper polygons, each a list of corner points.
- `texts`: copper texts, each with its text, position, height, rotation and mirror flag.
- Each footprint in `library` also has a `category`.

All units are millimetres, and Y points downwards. Older files still open, and the built-in footprints added since they were saved are added to their library. See `examples/example-design.json`.
