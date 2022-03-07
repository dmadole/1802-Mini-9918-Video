# 1802/Mini 9918 Video Assembly Notes

Follow usual assembly practices, which I will not document here. I recommend installing the lowest-height components first (resistors, diodes, right-angle connectors), then the next higher (sockets), and so on.

Please review all jumper settings before trying to operate the board. In particular, a group select jumper must be installed for the board to work, in systems without group I/O capability, this should be on the ALL position.

## Capacitor Values

Note that there are two different values of ceramic capacitor on this board, 33pF and 0.1uF. Please be sure to install the correct value in the correct location. The 33pF are typically marked "33J" and go at C1-3, and the 0.1uF are typically marked "104" and go at C4-10.

## Video Output Connectors

The RCA jacks should be installed flush to the board, with the plastic posts fitting into the notches at the edge of the board. When soldering, the connectors should be pressed firmly down toward the board and inward toward the center of the board. This will ensure the posts are firm against the board to provide maximum physical support of the connectors.

Recommended jack colors are yellow in the Y/COMP position for component video-only boards, and for composite video boards, green at Y/COM, red at R-Y, blue at B-Y, and black at SYNC.

## VDP Type Jumpers

The two jumpers marked 9X2X VDP, should be installed when using a VDP chip with component (Y/R-Y/B-Y) output (9928/9128/9929/9129) and removed when using a VDP chip with composite output (9918/9118).

The two jumpers marked VDP TYPE should be installed on the 99XX side when using 9918/9928/9929 VDP chips, or on the 91XX side when using 9118/9128/9129 VDP chips.

## Interrupts

The serial interface is capable of operating interrupt-driven and two modes are supported. The INTERRUPT jumped can be used to select whether interrupts are generated for all events recognized by the 1854 UART, or for receive character events only. Removing this jumper completely will disable interrupts.

The BIOS drivers do not support interrupt-driven operation. The standard software driver supports interrupts for receive characters only; if using this driver, either jumper setting will work, but the RX setting that only generates receive interrupts will produce less processor overhead and so it is recommended.

## Addressing

The video interface occupies two I/O ports which are set by the address jumpers. The standard configuration is for addresses 1 and 5 which are selected by setting  the two 4-1 jumpers to 1, the 1/4-0 jumper to 1/4, and the 2-0 jumper to 0. Here are all the address options:

| Ports | 4-1 | 1/4-0 | 2-0 |
|:-----:|:---:|:-----:|:---:|
| 1 & 5 |  1  |  1/4  |  0  |
| 2 & 3 |  4  |   0   |  2  |
| 2 & 6 |  1  |   0   |  2  |
| 3 & 7 |  1  |  1/4  |  2  |
| 4 & 5 |  4  |  1/4  |  0  |
| 6 & 7 |  4  |  1/4  |  2  |

Two-level I/O group selection is also supported, if the systemn contains a group expander board, in which case the desired group address should be jumpered on the I/O group jumpers. If no group expander board is installed, then the jumper should be installed on the ALL setting.

## EF Lines

The VDP interrupt signal, gated with the group-select signal, can be connected to any of the EF flag inputs using the EF LINE jumpers. This may be useful for custom polling drivers, or to support faster polling of interrupt-driven devices to determine which needs service. Unless VDP software is being used which monitors an EF line, it is recommended to leave this jumper off.
