Building Xilinx based systems with meta-xilinx
=============================================
This repository provides git submodules to setup the OpenEmbedded build system
with meta-xilinx to build images for Xilinx development boards and some vendor
boards.

Tweaked for the Kula prototype project from: https://github.com/balister/xilinx-minimal

OpenEmbedded allows the creation of custom linux distributions for embedded
systems. It is a collection of git repositories known as *layers* each of
which provides *recipes* to build software packages as well as configuration
information.

Information about the branch names is available at
https://wiki.yoctoproject.org/wiki/Releases.

Getting Started
---------------

1. Clone the git repository:

    $ git clone https://github.com/gratian/kula.git

2. Check out the appropriate branch (default scarthgap based branch is OK for now):

    $ cd kula

3. Update the submodules:

    $ git submodule update --init --recursive

4. Export path to Xilinx tools:

	Currently the setup depends on access to the 'xsct' tool from a Xilinx/Vitis install.
	Add to path with:

	$ export PATH=$PATH:<path_to_Xilinx_Vitis_bin_folder>

	example:

	$ export PATH=$PATH:~/Xilinx/Vitis/2024.2/bin

6. Initialize the build system:

	source kula-setup <path_to_xsa_file>

	This will:

	  - generate a system device tree from the provided .xsa file in ./build/sdt

	  - generate a machine configuration (including device trees) and updated ./build/conf/local.conf

	  - setup the bitbake environment

7. Build an image:

    $ bitbake core-image-minimal

    $ bitbake core-image-full-cmdline

8. Test it in qemu with

   $ MACHINE="versal-vck190-sdt-kula" runqemu core-image-minimal

   $ MACHINE="versal-vck190-sdt-kula" runqemu core-image-full-cmdline

10. Build an sdk:

    $ bitbake -c populate_sdk core-image-minimal
