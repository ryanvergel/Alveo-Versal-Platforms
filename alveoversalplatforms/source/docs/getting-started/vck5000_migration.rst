.. include:: /include/links.txt
.. include:: /include/format.txt

.. # S1 * S2 = S3 - S4


.. _VCK5000 Migration Guide:

##########################################################################
VCK5000 Migration Guide
##########################################################################

When first installing any vck5000 shell from ``vck5000_gen4x8_xdma_base_2`` forwards (see :ref:`Alveo Versal Deployment Packages Table`), it is necessary to execute this migration process rather than the standard platform installation. This operation is required to modify the formatting of the on-card OSPI flash for the later platforms.

It may be necessary to setup the XRT environment to use the ``xbmgmt`` utility below. See :ref:`XRT environment setup`.

.. attention::
   Migration only needs to be run once on a card. It is a one-way process. Once migrated it is not possible to revert the card to run pre-2022.1 platforms.

The process needs to be executed for the following two scenarios:

   - A brand new VCK5000 card

   - A VCK5000 card running an earlier platform such as ``vck5000_gen3x16_xdma_base_1``

To determine whether migration is required run the following command. Note: It is assumed that Step 1 from :ref:`Alveo Versal Deployment Package Installation<Alveo Versal Deployment Package Installation Step 1>` has already been completed.

.. code:: bash

   $ xbmgmt examine --report platform --device <Management BDF>
   
To find <Management BDF> see :ref:`Obtaining Card BDF Values`.

If the output from the command above contains the following then migration is needed:

.. packages installed, latest XRT
.. code:: bash

   ------------------------------------
   1/1 [0000:d8:00.0] : xilinx_vck5000
   ------------------------------------
   Warning: Device is not ready - Limited functionality available with XRT tools.
   
   Flash properties
     Type                 : ospi_versal
     Serial Number        : N/A
   
   Device properties
     Type                 : vck5000
     Name                 : N/A
     Config Mode          : 0
     Max Power            : N/A
   
   Flashable partitions running on FPGA
     Platform             : xilinx_vck5000
     SC Version           : INACTIVE
     Platform ID          : 0x0

In particular if the ``Flash properties: Type`` is ``ospi_versal`` then migration is required.

------------------------------

Migration Steps
*************************************************************************

Run the following command to migrate the card

.. code:: bash

   $ sudo /opt/xilinx/firmware/vck5000/gen4x8-xdma/base/migration/migrate.sh <Management BDF>

When complete, cold reboot the host machine as requested.

.. attention::
   Ensure the host machine is **cold** rebooted to ensure the new platform configuration is loaded.

After cold reboot completes, the Satellite Controller on the card also needs to be updated. Issue the following commands

.. code:: bash
   
   $ sudo xbmgmt program --base --device <Management BDF>
   $ timeout 40 watch -n 1 'xbmgmt examine --report vmr --device <Management BDF> --verbose | grep -i "program progress"'


The last command outputs information similar to below

.. code:: bash

   Every 1.0s: xbmgmt examine --report vmr --device d8:00.0 --verbose |...  Tue May  3 10:30:36 2022
   
     Program progress     : 100

``Program progress`` will increment from 0 to 100 to indicate SC upgrade progress. When this completes issue a cold reboot to complete the upgrade.

Return to :ref:`Alveo Versal Deployment Package Installation Step 3` to validate the installation.

----------------------------------

.. include:: /include/license.txt
