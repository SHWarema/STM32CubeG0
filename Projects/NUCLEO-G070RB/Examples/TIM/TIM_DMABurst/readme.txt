/**
  @page TIM_DMABurst TIM_DMABurst example
  
  @verbatim
  ******************************************************************************
  * @file    TIM/TIM_DMABurst/readme.txt 
  * @author  MCD Application Team
  * @brief   Description of the TIM DMA Burst example.
  ******************************************************************************
  *
  * Copyright (c) 2018 STMicroelectronics. All rights reserved.
  *
  * This software component is licensed by ST under BSD 3-Clause license,
  * the "License"; You may not use this file except in compliance with the
  * License. You may obtain a copy of the License at:
  *                       opensource.org/licenses/BSD-3-Clause
  *
  ******************************************************************************
  @endverbatim

@par Example Description 

How to update the TIMER channel 1 period and duty cycle using the TIMER DMA burst feature.

Every update DMA request, the DMA will do 3 transfers of half words into Timer 
registers beginning from ARR register.
On the DMA update request, 0x0FFF will be transferred into ARR, 0x0000 
will be transferred into RCR (if supported), 0x0555 will be transferred into CCR1. 

The TIM3CLK frequency is set to SystemCoreClock, to get TIM3 counter
clock at 8 MHz the Prescaler is computed as following:
- Prescaler = (TIM3CLK / TIM3 counter clock) - 1

SystemCoreClock is set to 56 MHz.

The TIM3 Frequency = TIM3 counter clock/(ARR + 1)
                   = 8 MHz / 4096 = 1.95 KHz

The TIM3 CCR1 register value is equal to 0x555, so the TIM3 Channel 1 generates a 
PWM signal with a frequency equal to 1.95 KHz and a duty cycle equal to 33.33%:
TIM3 Channel1 duty cycle = (TIM3_CCR1/ TIM3_ARR + 1)* 100 = 33.33%

The PWM waveform can be displayed using an oscilloscope.

@note Care must be taken when using HAL_Delay(), this function provides accurate
      delay (in milliseconds) based on variable incremented in SysTick ISR. This
      implies that if HAL_Delay() is called from a peripheral ISR process, then 
      the SysTick interrupt must have higher priority (numerically lower)
      than the peripheral interrupt. Otherwise the caller ISR process will be blocked.
      To change the SysTick interrupt priority you have to use HAL_NVIC_SetPriority() function.
      
@note This example needs to ensure that the SysTick time base is always set to 1 millisecond
      to have correct HAL operation.

@par Keywords

Timer, DMA, Burst mode, Duty Cycle, Waveform, Oscilloscope, Output, Signal, PWM

@par Directory contents

  - TIM/TIM_DMABurst/Inc/stm32g0xx_hal_conf.h    HAL configuration file
  - TIM/TIM_DMABurst/Inc/stm32g0xx_it.h          Interrupt handlers header file
  - TIM/TIM_DMABurst/Inc/main.h                  Header for main.c module  
  - TIM/TIM_DMABurst/Src/stm32g0xx_it.c          Interrupt handlers
  - TIM/TIM_DMABurst/Src/main.c                  Main program
  - TIM/TIM_DMABurst/Src/stm32g0xx_hal_msp.c     HAL MSP file
  - TIM/TIM_DMABurst/Src/system_stm32g0xx.c      STM32G0xx system source file

@par Hardware and Software environment

  - This example runs on STM32G070RBTx devices.
  - In this example, the clock is set to 56 MHz.
    
  - This example has been tested with NUCLEO-G070RB 
    board and can be easily tailored to any other supported device 
    and development board.

  - NUCLEO-G070RB Set-up
    - Connect the TIM3 output channel to an oscilloscope to monitor the different waveforms: 
    - TIM3 CH1 (PA.06 (pin 13 in CN10 connector))

@par How to use it ? 

In order to make the program work, you must do the following :
 - Open your preferred toolchain 
 - Rebuild all files and load your image into target memory
 - Run the example

 * <h3><center>&copy; COPYRIGHT STMicroelectronics</center></h3>
 */
