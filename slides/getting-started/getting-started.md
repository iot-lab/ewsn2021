class: center, middle

# Tutorial IoT on Microcontrollers

## Getting started

---

## Your working environment

- The [FIT IoT-LAB](https://www.iot-lab.info) testbed will be used to perform
  the exercises that require hardware.

- We provide temporary accounts, just for this tutorial.

- For the ease of use, all exercises are performed online in Jupyter Notebooks

.center[
    <img src="images/jupyter.png" alt="" style="width:600px;"/>
]

---

## About the Jupyter Notebooks

.center[
Available at **https://labs.iot-lab.info**


<img src="images/iotlab-jupyterhub.png" alt="" style="width:300px;"/>

**Short demo: discover Jupyterlab notebooks!**
<form class=notebook>
    <input class=login id="login_start" type="text" oninput="check_login('login_start', 'launcher_start')" placeholder="Enter your IoT-LAB login">
    <input class=launcher id="launcher_start" type="button" value="Launch notebook" onclick="open_notebook('login_start', 'start.ipynb')">
</form>
]

---

## Structure of a RIOT application

A minimal RIOT application consists in:

- A `Makefile`

```mk
APPLICATION = example

BOARD ?= native

RIOTBASE ?= $(CURDIR)/../../../RIOT

DEVELHELP ?= 1

include $(RIOTBASE)/Makefile.include
```

- A C-file containing the main function

```c
#include <stdio.h>

int main(void)
{
    puts("My first RIOT application");
    return 0;
}
```

---

## Build a RIOT application

- The build system of RIOT is based on **make** build tool

--

- To build an application, **make** can be called in 2 ways:

  - From the application directory:
  ```sh
  $ cd <application_directory>
  $ make
  ```

  - From anywhere, by using the `-C` to specify the application directory:
  ```sh
  $ make -C <application_directory>
  ```

--

- Use the **BOARD** variable to specify the target at build time
```sh
$ make BOARD=<target> -C <application_directory>
```
`BOARD` can be any board supported by RIOT<br>
&#x21d2; see the **RIOT/boards** directory for the complete list

--

- Use the **RIOTBASE** variable to specify the RIOT source base directory

---

## Run a RIOT application

This depends on the target board:

- Running on **native**: the RIOT application executed is a simple Linux process
```sh
$ make BOARD=native -C <application_dir>
$ <application_dir>/bin/native/application.elf
```

- Running on **hardware**: the RIOT application must be *flashed* first on the
  board

--

&#x21d2; use the **flash** and **term** targets with make
  - **flash**: build and write the firmware on the MCU flash memory

  - **term**: opens a terminal client connected to the serial port of the
    target

All this can be done in one command:

```sh
$ make BOARD=<target> -C <application_dir> flash term
```

*Note:* the last command can also be used with **native** target

---

## Exercise: your first RIOT application

Let's build and run our first RIOT application !<br><br>

.center[
<form class=notebook>
    <input class=login id="login_hello" type="text" oninput="check_login('login_hello', 'launcher_hello')" placeholder="Enter your IoT-LAB login">
    <input class=launcher id="launcher_hello" type="button" value="Launch notebook" onclick="open_notebook('login_hello', 'riot/basics/hello-world/hello-world.ipynb')" disabled>
</form>
]

---

## How to extend the application

&#x21d2; by adding modules in the application `Makefile` or from the command line:

- Add extra modules with **USEMODULE**<br>
    &#x21d2; `xtimer`, `fmt`, `shell`, `ps`, etc

- Include external packages with **USEPKG**<br>
    &#x21d2; `lwip`, `semtech-loramac`, etc

- Use MCU peripherals drivers with **FEATURES_REQUIRED**:<br>
    &#x21d2; `periph_gpio`, `periph_uart`, `periph_spi`, `periph_i2c`

--

Example in a `Makefile`:
```mk
USEMODULE += xtimer shell

USEPKG += semtech-loramac

FEATURES_REQUIRED += periph_gpio
```
Example from the command line:
```sh
$ USEMODULE=xtimer make BOARD=b-l072z-lrwan1
```

---

## Exercise: write an application with a shell

.center[
<form class=notebook>
    <input class=login id="login_shell" type="text" oninput="check_login('login_shell', 'launcher_shell')" placeholder="Enter your IoT-LAB login">
    <input class=launcher id="launcher_shell" type="button" value="Launch notebook" onclick="open_notebook('login_shell', 'riot/basics/shell/shell.ipynb')" disabled>
</form>
]

---

## Exercise: read sensor data using the shell



---

## Next steps

Let's continue with 3 more specialized topics to continue this tutorial. You can
choose 1 between the 3:

- [LwM2M](https://iot-lab.github.io/ewsn2021/slides/lwm2m)

- [LoRaWAN](https://iot-lab.github.io/ewsn2021/slides/lorawan)

- [Security](https://iot-lab.github.io/ewsn2021/slides/security)
