nRF70 BM Driver README
======================

Setup Instructions
==================

This section provides instructions on how to set up and use the nRF70 BM driver with `west` for nRF boards or `git submodule` for customer boards.


Using `west` for nRF Boards
---------------------------

For applications integrating the nRF70 Series BM driver it is recommended to use `west` and the nRF Connect SDK Toolchain,
for building and programming, when testing and evaluating the BM driver using official Nordic development boards.

1. **Toolchain and environment setup:**

    Install the nRF Command Line tools (for programming and debugging applications on Nordic development boards)
    downloading them from https://www.nordicsemi.com/Products/Development-tools/nrf-command-line-tools.

    Follow the instructions on the official nRF Connect SDK documentation on how to install the required toolchain.
    https://docs.nordicsemi.com/bundle/ncs-latest/page/nrf/installation/install_ncs.html


    When using the command line and nRF Util method, `west` and all the required tools will be installed. Alternatively,
    `west` can be installed as described in the following step.

2. **Install West:**

    Follow the instructions on the official Zephyr Project documentation to install `west`:
    https://docs.zephyrproject.org/latest/guides/west/install.html

3. **Clone the Repository:**

    Clone the main repository using `west`:

    ```sh
    west init -m https://github.com/nrfconnect/nrf70-bm
    cd nrf70-bm
    west update
    ```

4. **Build the Project:**

    Use `west` to build the project for your specific board:

    ```sh
    west build -b your_board_name
    ```

5. **Flash the Board:**

    Flash the firmware onto your nRF board:

    ```sh
    west flash
    ```

Using `git submodule` for third-party boards
--------------------------------------------

1. **Clone the Repository:**

    Clone the main repository and its submodules:

    ```sh
    git clone https://github.com/nrfconnect/nrf70-bm --recurse-submodules
    ```

    If you have already cloned the repository without submodules, you can initialize and update the submodules with:

    ```sh
    git submodule update --init --recursive
    ```

2. Build and flashing instructions depend on the third-party board and the build system used.


Source directory Structure
==========================

The source directory structure shall look like this:

.. code-block:: none

    nrf70_bm_lib/         # nRF70 BM driver library
    sdk_nrfxlib/          # nRF Connect SDK nrfxlib
      nrf_wifi/           # nRF70 Wi-Fi OS agnostic driver
    samples/              # Sample applications
      radio_test_bm/      # Radio test sample application
      scan_bm/            # Scan sample application
    nrf70_zephyr_shim/    # Zephyr shim for nRF70, reference for third-party boards


Porting guide
=============

The nRF70 Series BM driver is designed to be portable across different platforms.
The `nrf70_zephyr_shim` directory contains a reference implementation for Zephyr.
This reference implementation can be used as a guide to port the library to other platforms.

Please refer to `nrf70_bm_lib/docs` for more information on the BM driver and the porting guide.

Documentation
=============

The documentation for the nRF70 BM driver is available in the `nrf70_bm_lib/docs` directory.
To build the documentation in a Linux environment, follow the below steps:

> **Note:** Currently, only Linux platforms are supported.

1. **Install python requirements:**

    Install the required python packages using `pip`:

    ```sh
    pip install -r nrf70_bm_lib/docs/requirements.txt
    ```
2. ** Install doxygen:**

    Install doxygen using `apt` package manager (or any other package manager based on your OS):

    ```sh
    sudo apt install doxygen
    ```
3. **Build the Documentation:**

    Build the documentation using the following command:

    ```sh
    ./build_docs.sh
    ```

    The generated HTML files will be available in `nrf70_bm_lib/docs/build/html`.

    Open the `index.html` file in a browser to view the documentation.


Example code
============

The repository includes two sample applications for testing and evaluation of the nRF70 Bare Metal library:

1. `BM radio test` sample to perform basic RF testing of the nRF70 Series device, as well as
    Factory Information Configuration Registers (FICR) programming.

2. `BM scan` sample to test Wi-Fi SSID scanning with the nRF70 Series devices.

Both samples can be found under the ``samples/`` directory. The samples can be built using `west`, as explained above.
