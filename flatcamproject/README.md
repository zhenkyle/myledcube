# FlatCAM Project

Generate cnc jobs for making PCB with my 2418 CNC Router.

## About unit

The default unit in FlatCAM is inch

## Tracking the silkscreen LOGO

```
1 inch = 25.4 mm
```

### Generate geo object

Using this method: http://caram.cl/software/flatcam/tracing-the-silkscreen-with-flatcam/

In FlatCAM Shell:

```
cd ~/Documents/Github/myledcube
open_gerber board.topsilk.gbr -follow 1 -outname GTO_follow
follow GTO_follow -outname silk_geo
```

### Export to SVG

In FlatCAM , click `silk_geo`,choose `File - Export SVG...`, export to  `logo.svg`.

### Edit `logo.svg` in InkScape

Edit with Inkscape, delete everything except logo.

```
inkscape logo.svg
```

Flip it verically

Save it with name `logo-flip-vertical`.

### Import `logo-flip-vertical.svg` to FlatCAM again

Import it again, and using Offset to move it into desired place.

_**Note:** There's may be some bugs in FlatCAM, as export then import the same SVG again, doesn't have the same position._

## Making bottom PCB milling CNC job

Steps are:

### Generate Isolation Routing: `board.bottom.gbr` to `board.bottom.gbr_iso`

With these options:

* Tool dia: 0.020 inch( 0.508 mm)
* Width (# passes): 1 pass
* Pass overlap: 0.15 (15%)

### Create CNC job: `board.bottom.gbr_iso` to `board.bottom.gbr_iso_cnc`

With these options:

* Cut Z: 0.001 ( 0.0254 mm, 0.05 mm seems too much)
* Feed Rate: 3.0 inch/minute (76.2 mm/minute)
* Tool dia: 0.024 inch( 0.6096 mm, because I ma using 0.6 mm dia milling head)

### Export CNC job file

Export CNC job file to `1_board_bottom.gcode`.

## Making LOGO milling CNC job

Normal routing with these options:

### Create CNC job: `logo-flip-vertical.svg` to `logo-flip-vertical.svg_cnc`

With these options:

* Cut Z: 0.001 ( 0.0254 mm, 0.05 mm seems too much)
* Feed Rate: 3.0 inch/minute (76.2 mm/minute)
* Tool dia: 0.024 inch( 0.6096 mm, because I ma using 0.6 mm dia milling head)

### Export CNC job file

Export CNC job file to `2_logo.gcode`.

## Making plated drill CNC job

Normal routing with these options:

### Create plated drill hole CNC job `board.plated-drill.cnc` to `board.plated-drill.cnc_cnc`

With tese options:

* Cut Z: -0.08 inch (2.032 mm)
* Travel Z: 0.1 inch (2.54 mm)
* Feed Rate: 3.0 inch/minute (76.2mm/minute)

_**Note:** I use 0.8mm drill head to drill to these holes_

### Export CNC job file

Export CNC job file to `3_plated_drill.gcode`.

## Making unplated drill CNC job

Normal routing with these options:

### Create unplated drill hole CNC job `board.unplated-drill.cnc` to `board.unplated-drill.cnc_cnc`

With tese options:

* Cut Z: -0.08 inch (2.032 mm)
* Travel Z: 0.1 inch (2.54 mm)
* Feed Rate: 3.0 inch/minute (76.2mm/minute)

_**Note:** I use 3mm drill head to drill these holes_

### Export CNC job file

Export CNC job file to `4_plated_drill.gcode`.

