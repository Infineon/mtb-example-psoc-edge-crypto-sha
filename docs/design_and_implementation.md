[Click here](../README.md) to view the README.

## Design and implementation

The design of this application is minimalistic to get started with code examples on PSOC&trade; Edge MCU devices. All PSOC&trade; Edge E84 MCU applications have a dual-CPU three-project structure to develop code for the CM33 and CM55 cores. The CM33 core has two separate projects for the secure processing environment (SPE) and non-secure processing environment (NSPE). A project folder consists of various subfolders, each denoting a specific aspect of the project. The three project folders are as follows:

**Table 1. Application projects**

Project | Description
--------|------------------------
*proj_cm33_s* | Project for CM33 secure processing environment (SPE)
*proj_cm33_ns* | Project for CM33 non-secure processing environment (NSPE)
*proj_cm55* | CM55 project

<br>

In this code example, at device reset, the secure boot process starts from the ROM boot with the secure enclave (SE) as the root of trust (RoT). From the secure enclave, the boot flow is passed on to the system CPU subsystem where the secure CM33 application starts. After all necessary secure configurations, the flow is passed on to the non-secure CM33 application. Resource initialization for this example is performed by this CM33 non-secure project. It configures the system clocks, pins, clock to peripheral connections, and other platform resources. It then enables the CM55 core using the `Cy_SysEnableCM55()` function and the CM55 core is subsequently put to DeepSleep mode.

Secure hash algorithm (SHA) is a function that takes a message of arbitrary length and reduces it to a fixed length residue or message digest, after performing a series of mathematically defined operations that practically guarantee that any change in the message changes the hash value. A hash value is used for message authentication by transmitting a message with a hash value appended to it and recalculating the message hash value using the same algorithm at the recipient’s end. If the hashes differ, it indicates that the message has been corrupted.

In this example, CM33 non-secure project (proj_cm33_ns) reads user input message is from the UART terminal and a 32-byte long hash value is generated using the SHA-256 algorithm. For any arbitrary message, a 32-byte hash value is generated. The 32-byte hash value for the user input message is then displayed on the UART terminal emulator. 

> **Note:** The maximum message size in this example is restricted to 100 characters. To increase the message size, change the `MAX_MESSAGE_SIZE` macro in the *main.c* file to the one you require.

**Figure 2. Firmware flowchart**

![](images/flow-chart.png)

<br>