---
title: ''
author: Kevin Nel
date: '2023-0x-0x'
---

## Building the Project

## Prerequisites

- `arm-eabi-none-gcc`
- `openocd`
- `make`
- `st-link` (provides `st-flash`)
- [`STM32CubeMX`](https://www.st.com/content/st_com/en/products/development-tools/software-development-tools/stm32-software-development-tools/stm32-configurators-and-code-generators/stm32cubemx.html) (not the same as `STM32CubeIDE`)
- you may need to install [the udev rules](https://calinradoni.github.io/pages/200616-non-root-access-usb.html) or add user to dialout group (check what you might need for your distribution)

## VSCode Extensions

- microsoft c/c++ extension pack
- microsoft makefile tools (optional)
- cortex debug

> **note for windows:** you will need to install all the same things but change all the paths to executables in the `.vscode` folder (some examples have been commented out in `tasks.json`)
> using chocolatey
>
> ```sh
> choco install gcc-arm-embedded
> choco install git
> choco install make
> choco install openocd
> ```
>
> You also need to install `stlink` and **add it to your `PATH` manually**
> make sure the commands are added to your `PATH` (you may need to restart, you can check if the paths were added successfully by trying to run the commands in the command prompt)
> check the `.vscode` folder and it's files to make sure the paths match those required for your system.
> you may need to install the [st-link driver](https://www.st.com/en/development-tools/stsw-link009.html#get-software) to allow the board to flash

## usage

build with: `make -j12` (or however many cores you need)
clean with: `make clean`
flash with: `st-flash --reset write ./build/esp411_pracs.bin 0x8000000`

> start adresss: `0x8000000` (found in `./STM32F429ZITx_FLASH.ld`)

tasks have been setup in `task.json` for building, cleaning and flashing (use `ctrl+shift+b` to access task menu)

for more warnings add the folowing to the makefile

```make
# My CFLAGS
CFLAGS += -Wpedantic -Wimplicit
```

**write all code between the USER CODE BEGIN and USER CODE END comments to avoid code deletion when CubeMX is used to generate code to update peripheral configurations.**
