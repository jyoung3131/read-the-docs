===============
BlueField DPUs
===============

.. image:: ../figures/images/nvidia_bf2_card.png
   :alt: BlueField 2 card
   :scale: 10

NVIDIA's BlueField Data Processing Unit has both a high-speed InfiniBand/Ethernet interconnect and on-board DRAM and Arm CPU cores. Notably, this is one of the first SmartNIC devices that can run an on-board operating system in "host" mode. 

Acknowledgments
===============
Dr. Young and Dr. Bryngelson have received several BF2 cards which are hosted in the Rogues Gallery via `NVIDIA's Academic Hardware Grant program <https://nvidia.my.site.com/HardwareGrant/s/Application>`__.

Current Status
==============

BUGS / Feature Requests
-----------------------
- Modules and high-speed interfaces may need some modifications to be fully functional. 

System Specifications
=====================

.. list-table:: 
    :widths: auto
    :header-rows: 1
    :stub-columns: 1

    * - Queues
      - Node Name
      - Hosting Node
      - CPU
      - Memory (GB)
      - Network
      - Notes
    * - rg-nextgen-hpc
      - quorra<1-2>-bf2-1
      - quorra<1-2>
      - 
      - 
      - 
      -
    * - rg-nextgen-hpc
      - kingpin<1-2>-bf2-mgt-<a-b>
      - kingpn<1-2>
      - 
      - 
      - 
      -
    * - rg-nextgen-hpc
      - dash<1-4>-bf3-<1-2>
      - `dash<1-4> <https://gt-crnch-rg.readthedocs.io/en/main/techfee/dash-spr-max-smartnic.html>`__
      - Cortex-A78AE, 16 core
      - 32 GB DDR4, dual channel
      - 
      - 


Software and Tools
===================

.. list-table::
    :widths: auto
    :header-rows: 1
    :stub-columns: 1

    * - Distro
      - Kernel
      - Standard Compilers
      - Other Compilers
      - MPI
      - Miscellaneous
    * - Ubuntu 22.04
      - 5.15.0
      - GCC 11.4
      - OpenMPI 4.1.6, HPC-X 2.17, 2.18
      - 
      - `DOCA 2.7.0 <https://docs.nvidia.com/doca/sdk/nvidia+doca+release+notes/index.html>`__

Networking Configuration
==================

The management ports on the BlueField-3 DPUs are connected to a 1 Gigabit Ethernet switch, while the network ports are connected to our `Cisco 9336 100 Gigabit Ethernet switch <https://www.cisco.com/c/en/us/support/switches/nexus-9336c-fx2-switch/model.html#~tab-specs>`__.


Key Resources to Get Started
============================
- Check out the recent `Supercomputing 2023 tutorial on SmartNICs <https://github.com/gt-crnch-rg/>`__ for an overview of different ways to use BlueFields.
    - See an example of using a `heterogeneous workflow on the host and DPU <https://gt-crnch-rg.readthedocs.io/en/main/networking/bf-heterogeneous-workflow.html>`__
    - Check out recent work by BSC researchers on `using OpenMP offloading with BlueField DPUs <https://gt-crnch-rg.readthedocs.io/en/main/networking/dpu-openmp-offload.html>`__
- See the `DOCA SDK page <https://gt-crnch-rg.readthedocs.io/en/main/networking/nvidia-doca-sdk.html>`__ for information on using DOCA features with the BlueField devices.

How to Access BlueField Cards
=============================

As with most CRNCH resources, you need to either log in via the gateway node, rg-login, or access the system from the campus network via VPN or an on-campus connection.

To request an allocation using slurm, you can run the following for your desired resource:

.. code::

   //Request an allocation of 1 hr, partition rg-nextgen-hpc, and specify the node name for the server with -w
   //If we request dash3 and dash3-bf3
   salloc -t 1:00:00 -p rg-nextgen-hpc -w dash3,dash3-bf3-1
   //Your job would start on dash3, in this instance
   gburdell@dash3:~$

Remember that if you just request the node but don't specify number of cores or tasks that you will receive 1 CPU core per node. To avoid this you can use the `--exclusive` flag to reserve the entire node or the following to reserve a few cores:

.. code::

   salloc -t 1:00:00 -p rg-nextgen-hpc -w dash3,dash3-bf3-1 --ntasks=8 --cpus-per-task=4

Using Software Modules
===========================================

.. code::

   gburdell@dash3-bf3-1:~$ module use /projects/tools/aarch64/ubuntu-22.04/modulefiles/
   gburdell@dash3-bf3-1:~$ module avail

   -------------------- /projects/tools/aarch64/ubuntu-22.04/modulefiles --------------
   hpcx/2.17/hpcx-debug-ompi    hpcx/2.17/hpcx-mt-ompi    hpcx/2.17/hpcx-ompi       
   hpcx/2.17/hpcx-prof-ompi     hpcx/2.17/hpcx-stack      openmpi/4.1.6
   hpcx/2.17/hpcx-debug         hpcx/2.17/hpcx-mt         hpcx/2.17/hpcx-rebuild    
   hpcx/2.17/hpcx-prof          hpcx/2.17/hpcx (D)


Using the High-Speed Interface for MPI jobs
===========================================

TBD

Additional BlueField Resources
------------------------------

- `DPU BF3 User Guide <https://docs.nvidia.com/networking/display/bf3dpuvpi>`__
- `DPU BF2 Ethernet User Guide <https://docs.nvidia.com/networking/display/bluefield2dpuenug>`__
- `DPU Software Guide <https://docs.nvidia.com/networking/display/bluefielddpubspv422/bluefield+software+overview>`__

Related BlueField Publications
---------------------------------------

- `BluesMPI: Efficient MPI Non-blocking Alltoall Offloading Designs on Modern BlueField Smart NICs <https://dl.acm.org/doi/abs/10.1007/978-3-030-78713-4_2>`__
- `Battle of the BlueFields–An In-Depth Comparison of the BlueField-2 and BlueField-3 SmartNICs, HotInterconnects 2023 <https://ieeexplore.ieee.org/document/10287294>`__
- `Characterizing Lossy and Lossless Compression on Emerging BlueField DPU Architectures, HotInterconnects 2023 <https://ieeexplore.ieee.org/document/10287290>`__
- `Hypersparse Traffic Matrix Construction using GraphBLAS on a DPU <https://arxiv.org/abs/2310.18334>`__
