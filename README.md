# Rearbox

This PCB combines components for the rear side of the vehicle hardware and firmware.

## Features

Communication:

- 2 CAN transceivers
- UART (internal only)
- SPI (internal only)
- I2C (internal only)

Outputs:

- 2 fan drivers
- 2 pump drivers
- ASSI driver
- RTDS driver
- brake light driver

Inputs:

- 12 digital safety inputs
- 2 suspension load cell sensors
- 2 suspension potentiometer sensors
- 2 water pressure sensors
- 2 water temperature sensors
- monocoque temperature sensors


## Hardware

<img width="1116" height="777" alt="rearbox_3D" src="https://github.com/user-attachments/assets/1dca8a6b-c0e8-4828-bbc1-6da1dea14eb6" />
<img width="833" height="537" alt="connector-layer" src="https://github.com/user-attachments/assets/f7b3306e-c65c-4d66-901c-c9ba97e9ff7a" />
<img width="723" height="617" alt="connector" src="https://github.com/user-attachments/assets/7e595106-3718-47bb-96b6-9ad47b7d1b3a" />
<img width="823" height="630" alt="rearbox_layer1_2_Cu" src="https://github.com/user-attachments/assets/c01df8ac-fc16-4f65-b69d-16029ed2286b" />
<img width="838" height="643" alt="rearbox_Front_Cu" src="https://github.com/user-attachments/assets/8c7e2804-226f-43aa-8ecf-7f887df11637" />
<img width="852" height="652" alt="rearbox_BottonCu" src="https://github.com/user-attachments/assets/40271f71-f59a-4932-9937-8149f67643e8" />


## Firmware
> For the CAN library to work correctly, the auto-generated HAL driver file needs to be patched.
>
> Make sure to restore any changes made by the generator to the `firmware/Drivers/STM32G4xx_HAL_Driver/Src/stm32g4xx_hal_fdcan.c` file or the receiving won't work!

Below are the changes that need to be made to the `stm32g4xx_hal_fdcan.c` file:

```diff
2231c2231
<     assert_param(IS_FDCAN_RX_FIFO(RxLocation));
---
>     //assert_param(IS_FDCAN_RX_FIFO(RxLocation));
2235c2235
<         if(RxLocation == FDCAN_RX_FIFO0) /* Rx element is assigned to the Rx FIFO 0 */
---
>         if(RxLocation == 0) /* Rx element is assigned to the Rx FIFO 0 */
2343c2343
<         if(RxLocation == FDCAN_RX_FIFO0) /* Rx element is assigned to the Rx FIFO 0 */
---
>         if(RxLocation == 0) /* Rx element is assigned to the Rx FIFO 0 */
```

