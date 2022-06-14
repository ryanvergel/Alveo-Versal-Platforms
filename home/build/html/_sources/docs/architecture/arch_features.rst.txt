.. include:: /include/links.txt
.. include:: /include/format.txt

.. # S1 * S2 = S3 - S4

.. _arch features:

##########################################################################
Platform Features
##########################################################################

Different platform releases can include one or more of the following features. See the UG area for details on specific platforms of interest.



.. csv-table:: **Table: Platform Features**
    :header: "Feature", "Description"
    :widths: auto

    "DFX", "| **All Alveo Versal platforms shall be DFX-1RP**
    | Dynamic Function Exchange (DFX) technology allows the card to change functionality on the fly without power-cycling the server. In Alveo Ultrascale+ Platforms there were two variants:
    |   - **DFX-1RP**: The PCIe core and the DMA engine are combined and reside in the static region of the platform. These are also known as one-stage platforms.
    |   - **DFX-2RP**: The PCIe core resides in the static region of the FPGA (also known as the base) while the DMA engine is dynamically loaded into a new reconfiguration region
    |     used by the shell partition. These are also known as two-stage platforms."
    "DMA", "| Static region data mover. For Versal-based platforms the data mover is hardened unlike Ultrascale+-based platforms. Initially one DMA type is supported                              
    |   - `XDMA Subsystem <PG347_>`_                                                                              
    | *Note: XDMA will be replaced by QDMA-MM in the future.*"
    "PLRAM", "| PLRAM are small embedded memories that can be used as the target for DMA transfers."
    "DFX Clocking", "| A platform can provide a number of clocks for use with RTL and HLS kernels in the DFX region. Providing different clocks allows users the option of running their 
    | functions at different frequencies which can help the synthesis process."
    "AIE", "| AI Engine support. AIE support is dependent on the Versal device type. See `AIE Documentation <AIE_>`_ for more detail."
    "GT", "| Some Alveo cards include network interfaces such as QSFP module support. If available, an RTL kernel can be used to connect to the network interface(s)."
    "Host Memory", "| Shorthand for PCIe host memory transfers. The AXI subordinate interface allows User RTL and HLS kernels to directly read and write to host memory, bypassing 
    | the DMA. For more information, see `XRT Host Mem`_."
    "P2P", "| Shorthand for PCIe® peer-to-peer communication. Enables direct DMA transfer of data between two Alveo cards via the PCIe bus without temporarily buffering data within the 
    | host DDR memory. Without this feature the host CPU and memory are used for card-to-card communication. For more information, see `XRT P2P`_."
    
 
----------------------------------

.. include:: /include/license.txt
