/**
  @page TIM_OCInactive TIM_OCInactive example
  
  @verbatim
  ******************************************************************************
  * @file    TIM/TIM_OCInactive/readme.txt 
  * @author  MCD Application Team
  * @brief   This example shows how to configure the Timer to generate four 
  *          delayed signals.
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

Configuration of the TIM peripheral in Output Compare Inactive mode 
with the corresponding Interrupt requests for each channel.

  The TIM1 frequency is set to SystemCoreClock, and the objective is
  to get TIM1 counter clock at 10 kHz so the Prescaler is computed as following:
     - Prescaler = (TIM1CLK /TIM1 counter clock) - 1
   
  SystemCoreClock is set to 56 MHz for STM32G0xx Devices.

  The TIM1 CCR1 register value is equal to 10000:
  TIM1_CH1 delay = CCR1_Val/TIM1 counter clock  = 1s
  so the TIM1 Channel 1 generates a signal with a delay equal to 1s.

  The TIM1 CCR2 register value is equal to 5000:
  TIM1_CH2 delay = CCR2_Val/TIM1 counter clock = 500 ms
  so the TIM1 Channel 2 generates a signal with a delay equal to 500 ms.

  The TIM1 CCR3 register value is equal to 2500:
  TIM1_CH3 delay = CCR3_Val/TIM1 counter clock = 250 ms
  so the TIM1 Channel 3 generates a signal with a delay equal to 250 ms.

  The TIM1 CCR4 register value is equal to 1250:
  TIM1_CH4 delay = CCR4_Val/TIM1 counter clock = 125 ms
  so the TIM1 Channel 4 generates a signal with a delay equal to 125 ms.

  While the counter is lower than the Output compare registers values, which 
  determines the Output delay, the PC0, PC1, PC2 and PC3 pin are turned ON. 

  When the counter value reaches the Output compare registers values, the Output 
  Compare interrupts are generated and, in the handler routine, these pins are turned OFF.
  
@note Delay values mentioned above are theoretical (obtained when the system clock frequency 
      is exactly 56 MHz). Since the generated system clock frequency may vary from one board to another observed
      delay might be slightly different.
	  
@note Care must be taken when using HAL_Delay(), this function provides accurate delay (in milliseconds)
      based on variable incremented in SysTick ISR. This implies that if HAL_Delay() is called from
      a peripheral ISR process, then the SysTick interrupt must have higher priority (numerically lower)
      than the peripheral interrupt. Otherwise the caller ISR process will be blocked.
      To change the SysTick interrupt priority you have to use HAL_NVIC_SetPriority() function.
      
@note This example needs to ensure that the SysTick time base is always set to 1 millisecond
      to have correct HAL operation.

@par Keywords

Timer, Output, Compare, InActive, Signals, Delay, Frequency

@par Directory contents

  - TIM/TIM_OCInactive/Inc/stm32g0xx_hal_conf.h    HAL configuration file
  - TIM/TIM_OCInactive/Inc/stm32g0xx_it.h          Interrupt handlers header file
  - TIM/TIM_OCInactive/Inc/main.h                  Header for main.c module  
  - TIM/TIM_OCInactive/Src/stm32g0xx_it.c          Interrupt handlers
  - TIM/TIM_OCInactive/Src/main.c                  Main program
  - TIM/TIM_OCInactive/Src/stm32g0xx_hal_msp.c     HAL MSP file
  - TIM/TIM_OCInactive/Src/system_stm32g0xx.c      STM32G0xx system source file


@par Hardware and Software environment

  - This example runs on STM32G070RBTx devices.
    
  - This example has been tested with NUCLEO-G070RB 
    board and can be easily tailored to any other supported device 
    and development board.      

  - NUCLEO-G070RB Set-up
   Connect the following pins to an oscilloscope to monitor the different waveforms:
      - PC0: wave form of (TIM1_CH1) (pin 18 in CN10 connector)
      - PC1: wave form of (TIM1_CH2) (pin 16 in CN10 connector)
      - PC2: wave form of (TIM1_CH3) (pin 35 in CN7 connector)
      - PC3: wave form of (TIM1_CH4) (pin 37 in CN7 connector)

@par How to use it ? 

In order to make the program work, you must do the following :
 - Open your preferred toolchain
 - Rebuild all files and load your image into target memory
 - Run the example

  PC0
               _____________________________________________________
 _____________|                                                     |________________
              <-----------------------1sec-------------------------->
  PC1
               ___________________________
 _____________|                           |__________________________________________
              <-----------500ms----------->
  PC2
               _________________
 _____________|                 |____________________________________________________
              <------250ms------>
 
  PC3
               ___________
 _____________|           |___________________________________________________________
              <---125ms--->


 * <h3><center>&copy; COPYRIGHT STMicroelectronics</center></h3>
 */
