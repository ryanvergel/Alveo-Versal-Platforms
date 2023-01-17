.. include:: /include/links.txt
.. include:: /include/format.txt

.. # S1 * S2 = S3 - S4

.. _arch overview:

##########################################################################
Platform Overview
##########################################################################

Xilinx® Alveo® Versal® Data Center accelerator cards are PCI Express® compliant cards designed to accelerate compute-intensive applications such as machine learning, data analytics, and video processing in a server or workstation. The Vitis® core development kit provides verified platforms defining all the required hardware and software interfaces (shown in gray in the following figure), allowing you to design custom acceleration applications (shown in white) that are easily integrated into the `Vitis Programming Model`_.

.. figure:: /media/main_system_overview.png
   :align: center

   **Figure: Vitis System Overview**


On the *Alveo device* above, a platform consists of a **static region** and a **dynamic (DFX) region** as shown below.

.. note::
   The following diagram is generic and individual platforms may differ in terms of memory availability, DMA type and acceleration IP present such as `AIE`_. Please see the :ref:`user guides <ug list>` for a platform of interest.

.. figure:: /media/static_and_DFX_regions.png
   :scale: 50 %
   :align: center

   **Figure** Platform Static and DFX Regions


The static region of the platform provides the basic infrastructure for the card to communicate with the host server or workstation and hardware support for running user-defined DFX kernels. It includes the following:

- Hardened PCIe endpoint to enable communication with external PCIe host (`PG346`_)
- Hardened DMA IP (`PG347`_), NOC (`PG313`_) and AXI infrastructure IP (`PG247`_) for bulk Host ↔ Card memory data movement
- Embedded Platform Management running on ARM RPU (`AM011`_, `UG1304`_)
- Enablement of the APU running Petalinux (`AM011`_, `UG1304`_) for PS Kernel deployment
- Clocking and reset for card bring-up and operation.
- Peripherals responsible for board health and diagnostics, debug, and programming.
- UART/I2C communication to external `Satellite Controller`_ (SC), QSFP, sensors and SC firmware updates from the host (over PCIe).

Accelerated RTL, HLS or PS kernels are deployed at runtime to the DFX region. The exact features and resources available for accelerated kernels are :ref:`platform dependent <ug list>`.


----------------------------------

.. include:: /include/license.txt
