# Annotated PCB

In the annotated pcb image file, I have added some markers to explain any fixes that need to be made to the current test board. These are either where jumper cables must be soldered onto, or any components which should not be present.

On the left side of the board, the level shifters U12-U26 should not be used/soldered on. Instead, a jumper cable should be soldered between pads 3 and 4.

D4 should not be soldered on simply to remove a strong source of light which could ionize charge in the pixel array. It can useful to know if power is being supplied correctly, so use it in any initial testing phases. But, it should not be present for serious testing.

LA_Row_Clk should always be used and not Ser Tx.

VDDA should be connected to VDDA2 under the carrier board, so there should be a jumper wire there.

R23, R25 and R27 should not be present to prevent current flow along the voltage bias lines.

LDAC bar should always be jumpered.
