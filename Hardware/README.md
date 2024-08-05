
# Hardware 
This directory contains the design files for using and testing the TopmetalSe.

## Test PCB, the UW Caravel Test Board
This board is the primary board used for testing as it contains all of the electronics necessary for running the chip.

A large part of this board is concerned with running the [caravel SOC](https://caravel-harness.readthedocs.io/en/latest/index.html), which is a part of the chip that we ultimatly do not use much. However, it is important to know that we can communicate with it, if necessary. It can also be useful to test I/O connections and make sure the chip is powered on/works as expected. As a result, much of this board is copied over from the [efabless caravel boards](https://github.com/efabless/caravel_board).

The other part of the board is concerned with running the TopmetalSe, which happens in three categories: biasing, clocking and readout. 

The biasing of the chip is handled via the [Texas Instruments DAC 8568](https://www.ti.com/product/DAC8568?utm_source=google&utm_medium=cpc&utm_campaign=asc-null-null-GPN_EN-cpc-pf-google-wwe&utm_content=DAC8568&ds_k=DAC8568&DCM=yes&gclid=EAIaIQobChMIwIbj3O62_wIV-y-tBh3P_wriEAAYASAAEgLwtPD_BwE&gclsrc=aw.ds), which is an 8 Channel Digital to Analog Conveter. That is, we send digital commands and it outputs an analog voltage. The digital communication part is handled by an external FPGA, and the commands are generated via [software bit banging](https://github.com/selena0vbb/TopmetalSe_Sequencer/blob/main/util/DAC_control.py). These analog voltages are used as a bias either to source/sink a current or as a voltage bias on a transistor gate. 

The clocking of the chip is entirely handled by the external FPGAa and its firmware, so please look elsewhere for that. In the PCB design files, there are level shifters on the clocking signals to shift from the FPGA 3.3V signals to what I had assumed to be the caravel's 1.8V logic levels. However, the caravel harness actually expects 3.3V signals, so these level shifters are not soldered on and a jumper wire is used to make these connections.

There are two output signals coming from the TopmetalSe, an output for the large array (LA) and an output for the small array (SA). Both of these signals are readout using an opamp on the PCB. 

## Carrier Boards
To connect to the chip, we use a collection of adapter boards. This allows us to hotswap in any chip we want for testing. Now, the topmetalSe comes in a variety of packages, each of which has its own unique carrier board to accomdate the package. The carrier board is then plugged into the test board via 50 mil pins.

__One design fault is that the carriers can easily be plugged in incorrectly, causing undesired shorts. Please double check the pins and lined up correctly and in the correct orientation, as the header pins are symmetric. This applies to all carrier boards but the M.2 adapter.__

### M.2 Adapter Board
EFabless provided us with many QFN packaged chips. QFN, or quad flat no-leads, is an industry standard package for chips. Inside, chips are wire bonded to the frame and then encapsulated in plastic. This means that the QFN packages provide us with all the electrical capabilities, but none of the charge-sensing aspects of our device. __Please use these QFN packages to test and play around with learning to run the circuit__. Because we have so many and everything is encapsulated, there is very little chance of damaging these devices.

The QFN packages are/can be soldered onto a M.2 breakout board. EFabless provides the (design files)[https://github.com/efabless/caravel_board/tree/main/hardware/breakout/caravel-M.2-card-QFN] for these, so please look there if you need to. If you need more, the QFN packages must be soldered onto more M.2 breakouts.

The M.2 breakout boards can be attached to our test board via the M.2 adapter board.

### Wire Bonded

For charge-sensing, we must use the bare dies. The wire bonded carrier boards are pretty simple, as the bond pads go in the same order as the bond pads on the chip. The one key is that __the wire bonded board must be ENEPIG coated (not ENIG)__. If you order more, please make sure of this.

### Flip Chip


### aSe Flip Chip

## FPGA
For the FPGA, we use an external [BASYS3 Board](https://digilent.com/shop/basys-3-artix-7-fpga-trainer-board-recommended-for-introductory-users/). It is connected to the test board via PMOD connectors. Now, there is a mistake in the PCB design where the PMOD headers are actually flipped, so you must be careful to flip the PMOD connectors. Please see the PCB layout for this as well as the labels on the PCB to make sure things are aligned (ie Pin 1 to Pin 1). The firmware for the FPGA is discussed elsewhere.

## Sapphire Interposer
In flip chip packages, the chip is bonded to a flat piece known as the interposer. It is made with a 200/300 um thick piece of sapphire, which has conductive traces patterned and deposited onto it (usually O(100) nm of Al and Au). The side with traces on it is the bottom side. The top side is used for aSe Deposition and contains a conductive mesh. There is also a window opening where the pixel array is, which we typically laser cut.

## Electronic Equipment

## Mechanical Parts

## TopmetalSe Design Files
The majority of the design files for the TopmetalSe-V1 are contained in a [separate repo](https://github.com/harryxni/TopMetalSe-OpenMPW6). I include some general files in this repo as a reference.
