# Snippets for STM32H745

# LEDs initialization 

```C
static void MX_LED_Init(void){

  GPIO_InitTypeDef  gpio_init_structure;

  __HAL_RCC_GPIOB_CLK_ENABLE();
  __HAL_RCC_GPIOE_CLK_ENABLE();

  gpio_init_structure.Pin   = GPIO_PIN_0|GPIO_PIN_14;
  gpio_init_structure.Mode  = GPIO_MODE_OUTPUT_PP;
  gpio_init_structure.Pull  = GPIO_NOPULL;
  gpio_init_structure.Speed = GPIO_SPEED_FREQ_VERY_HIGH;

  HAL_GPIO_Init(GPIOB, &gpio_init_structure);
  HAL_GPIO_WritePin(GPIOB, GPIO_PIN_0, GPIO_PIN_RESET);
  HAL_GPIO_WritePin(GPIOB, GPIO_PIN_14, GPIO_PIN_RESET);

  gpio_init_structure.Pin   = GPIO_PIN_1;
  gpio_init_structure.Mode  = GPIO_MODE_OUTPUT_PP;
  gpio_init_structure.Pull  = GPIO_NOPULL;
  gpio_init_structure.Speed = GPIO_SPEED_FREQ_VERY_HIGH;

  HAL_GPIO_Init(GPIOE, &gpio_init_structure);
  HAL_GPIO_WritePin(GPIOE, GPIO_PIN_1, GPIO_PIN_RESET);
}
```

Use of these function

```C
HAL_GPIO_TogglePin(GPIOE,GPIO_PIN_1);
HAL_GPIO_TogglePin(GPIOB,GPIO_PIN_14);
HAL_Delay(2000);
```

# UART configuration

```C
#define HAL_TIMEOUT_VALUE 0xFFFFFFFF
#define countof(a) (sizeof(a) / sizeof(*(a)))
#define BUFFER_LENGTH 100
```

```C
uint8_t HeaderTxBuffer[] = "\r\nUART WakeUp!\r\n";
char buff[BUFFER_LENGTH];
```

```C
HAL_UART_Transmit(&huart3, (uint8_t*)&HeaderTxBuffer, countof(HeaderTxBuffer)-1, HAL_TIMEOUT_VALUE);

```

