# MyLEDCube

This is My 8x8x8 LED Cube project.

## Install toolchain

All tools are under Ubuntu 16.04.

### Install gEDA

http://www.geda-project.org/

### Install FlatCAM

http://flatcam.org

### Install Candle

https://github.com/Denvi/Candle

## Workflow

### Edit Schema

Edit mulitiplexer schema with:

```
gschem multiplexer.sch 
```

### Generate PCB file

Run this after make change with schema file:

```
gsch2pcb project.gsch2pcb
```

### Edit PCB file

Edit PCB file with:

```
pcb board.pcb
```

### Output gerber file

Output gerber file after edit PCB file:

_Select `File - Export`, choose `gerber`, click `OK`_

### View gerber file

You can view gerber file with:

```
gerbv *.gbr *.cnc
```