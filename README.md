```
Name : Karnan k 
Register number : 212222230062
```
# EXPERIMENT--03-SIMULATION-OF-PUSHBUTTON-AND-LED INTERFACE WITH ARM CONTROLLER AND PROTEUS 
## Aim: To Interface a Digital output (LED) and Digital input (Pushbutton) to ARM development board , and simulate it in Proteus 
## Components required: STM32 CUBE IDE, Proteus 8 simulator .
## Theory 
The full form of an ARM is an advanced reduced instruction set computer (RISC) machine, and it is a 32-bit processor architecture expanded by ARM holdings. The applications of an ARM processor include several microcontrollers as well as processors. The architecture of an ARM processor was licensed by many corporations for designing ARM processor-based SoC products and CPUs. This allows the corporations to manufacture their products using ARM architecture. Likewise, all main semiconductor companies will make ARM-based SOCs such as Samsung, Atmel, TI etc.

What is an ARM7 Processor?
ARM7 processor is commonly used in embedded system applications. Also, it is a balance among classic as well as new-Cortex sequence. This processor is tremendous in finding the resources existing on the internet with excellence documentation offered by NXP Semiconductors. It suits completely for an apprentice to obtain in detail hardware & software design implementation.

  STM32F401xB STM32F401xC ARM® Cortex®-M4 32b MCU+FPU, 105 DMIPS, 256KB Flash/64KB RAM, 11 TIMs, 1 ADC, 11 comm.
interfaces Datasheet - production data Features
• Core: ARM® 32-bit Cortex®-M4 CPU with FPU, Adaptive real-time accelerator (ART Accelerator™) allowing 0-wait state execution from Flash memory, frequency up to 84 MHz, memory protection unit, 105 DMIPS/ 1.
25 DMIPS/MHz (Dhrystone 2.
1), and DSP instructions
• Memories – Up to 256 Kbytes of Flash memory – Up to 64 Kbytes of SRAM
 
 

## Procedure:
 1. Creating Proteus project and running the simulation We are now at the last part of step by step guide on how to simulate STM32 project in Proteus.

 2. Create a new Proteus project and place STM32F40xx i.e. the same MCU for which the project was created in STM32Cube IDE.

 3. After creation of the circuit as per requirement as shown below
<img src = "https://github.com/karnankasinathan/EXPERIMENT--03-SIMULATION-OF-PUSHBUTTON-AND-LED-WITH-PROTEUS-/assets/118787064/cd8f90b8-63ac-4407-b740-53b2c37a0817" width=450 height=450>



 4. Double click on the the MCU part to open settings. Next to the Program File option, give full path to the Hex file generated using STM32Cube IDE. Then set the external 
 crystal frequency to 8M (i.e. 8 MHz). Click OK to save the changes.
 <img src = "https://github.com/karnankasinathan/EXPERIMENT--03-SIMULATION-OF-PUSHBUTTON-AND-LED-WITH-PROTEUS-/assets/118787064/656d1cbd-46c2-4963-a799-91ac0d990021" width=450 height=450>

 
 5. click on debug and simulate using simulation as shown below
<img src = "https://github.com/karnankasinathan/EXPERIMENT--03-SIMULATION-OF-PUSHBUTTON-AND-LED-WITH-PROTEUS-/assets/118787064/3f5b0073-e46c-4a3b-ad10-9eb1b862188d" width=450 height=450>




## STM 32 CUBE PROGRAM :
```
#include "main.h"
#include <stdbool.h>
bool bstat;

void SystemClock_Config(void);
static void MX_GPIO_Init(void);
void push_button();
int main(void)
{

  HAL_Init();

  SystemClock_Config();

  MX_GPIO_Init();

  while (1)
  {
	  push_button();
  }
}
void push_button()
{
	bstat=HAL_GPIO_ReadPin(GPIOA,GPIO_PIN_0);
	if(bstat==1)
		HAL_GPIO_WritePin(GPIOA,GPIO_PIN_5,GPIO_PIN_RESET);
	else
		HAL_GPIO_WritePin(GPIOA,GPIO_PIN_5,GPIO_PIN_SET);
}

void SystemClock_Config(void)
{
  RCC_OscInitTypeDef RCC_OscInitStruct = {0};
  RCC_ClkInitTypeDef RCC_ClkInitStruct = {0};


  __HAL_RCC_PWR_CLK_ENABLE();
  __HAL_PWR_VOLTAGESCALING_CONFIG(PWR_REGULATOR_VOLTAGE_SCALE2);

  RCC_OscInitStruct.OscillatorType = RCC_OSCILLATORTYPE_HSI;
  RCC_OscInitStruct.HSIState = RCC_HSI_ON;
  RCC_OscInitStruct.HSICalibrationValue = RCC_HSICALIBRATION_DEFAULT;
  RCC_OscInitStruct.PLL.PLLState = RCC_PLL_NONE;
  if (HAL_RCC_OscConfig(&RCC_OscInitStruct) != HAL_OK)
  {
    Error_Handler();
  }

  RCC_ClkInitStruct.ClockType = RCC_CLOCKTYPE_HCLK|RCC_CLOCKTYPE_SYSCLK
                              |RCC_CLOCKTYPE_PCLK1|RCC_CLOCKTYPE_PCLK2;
  RCC_ClkInitStruct.SYSCLKSource = RCC_SYSCLKSOURCE_HSI;
  RCC_ClkInitStruct.AHBCLKDivider = RCC_SYSCLK_DIV1;
  RCC_ClkInitStruct.APB1CLKDivider = RCC_HCLK_DIV1;
  RCC_ClkInitStruct.APB2CLKDivider = RCC_HCLK_DIV1;

  if (HAL_RCC_ClockConfig(&RCC_ClkInitStruct, FLASH_LATENCY_0) != HAL_OK)
  {
    Error_Handler();
  }
}


static void MX_GPIO_Init(void)
{
  GPIO_InitTypeDef GPIO_InitStruct = {0};

  __HAL_RCC_GPIOA_CLK_ENABLE();

  HAL_GPIO_WritePin(GPIOA, GPIO_PIN_5, GPIO_PIN_RESET);

  GPIO_InitStruct.Pin = GPIO_PIN_0;
  GPIO_InitStruct.Mode = GPIO_MODE_INPUT;
  GPIO_InitStruct.Pull = GPIO_PULLUP;
  HAL_GPIO_Init(GPIOA, &GPIO_InitStruct);

  GPIO_InitStruct.Pin = GPIO_PIN_5;
  GPIO_InitStruct.Mode = GPIO_MODE_OUTPUT_PP;
  GPIO_InitStruct.Pull = GPIO_NOPULL;
  GPIO_InitStruct.Speed = GPIO_SPEED_FREQ_LOW;
  HAL_GPIO_Init(GPIOA, &GPIO_InitStruct);

}


void Error_Handler(void)
{

  __disable_irq();
  while (1)
  {
  }
}

#ifdef  USE_FULL_ASSERT

void assert_failed(uint8_t *file, uint32_t line)
{

}
#endif
```



## Output screen shots of proteus  :




## Button off :
<img src = "https://github.com/karnankasinathan/EXPERIMENT--03-SIMULATION-OF-PUSHBUTTON-AND-LED-WITH-PROTEUS-/assets/118787064/d3fcf3dc-3d21-411d-a01c-6a047fae955b" width=450 height=450>

 ## Button on :
 <img src = "https://github.com/karnankasinathan/EXPERIMENT--03-SIMULATION-OF-PUSHBUTTON-AND-LED-WITH-PROTEUS-/assets/118787064/9fbadc84-0875-4321-95f5-d3e7b7a7c809" width=450 height=450>

 
## Result :
Interfacing a digital output and digital input  with ARM microcontroller are simulated in proteus and the results are verified.


