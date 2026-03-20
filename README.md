# STM32 Microsecond Delay using Timer (TIM2)

## Overview
This project demonstrates the implementation of a precise microsecond delay using a hardware timer (TIM2) in STM32. The delay function is further used to generate a square wave signal by toggling a GPIO pin.

This approach ensures higher accuracy compared to software-based delay loops.

---

## Objectives
- Implement microsecond-level delay using a hardware timer
- Configure GPIO for signal generation
- Generate a square wave using precise delay
- Understand timer configuration using STM32CubeMX

---

## Hardware Requirements
- STM32 Development Board (e.g., STM32F4 series)
- USB Programmer / ST-Link
- Oscilloscope (for signal verification)

---

## Software Requirements
- STM32CubeMX
- STM32CubeIDE / Keil / IAR
- Embedded C

---

## Project Structure
.
├── include/
│ └── main.h
├── src/
│ └── main.c
├── README.md

---

## Timer Configuration (CubeMX)
- Timer: TIM2
- Clock Source: Internal Clock
- Prescaler: 84 - 1 (for 1 MHz timer clock assuming 84 MHz system clock)
- Counter Period: 0xFFFFFFFF
- Mode: Up-counting

---

## GPIO Configuration
- Pin: PA8
- Mode: Output Push-Pull
- Used for square wave generation

---

## Microsecond Delay Function

```c
void delay_us(uint32_t us)
{
    __HAL_TIM_SET_COUNTER(&htim2, 0);
    while (__HAL_TIM_GET_COUNTER(&htim2) < us);
}
```

Explanation : 

1. The timer counter is reset to zero
2. The loop waits until the counter reaches the desired microsecond value
3. Since the timer runs at 1 MHz, each increment equals 1 microsecond

---

## Square Wave Generation : 

```c
while (1)
{
    HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_8);
    delay_us(100);
}
```

Explanation : 

1. GPIO pin is toggled continuously
2. Delay of 100 microseconds creates a square wave
3. Frequency depends on delay duration

---

## Peripheral Initialization : 

```c
HAL_TIM_Base_Start(&htim2);
```

Functionality : 
Starts TIM2 timer required for delay generation

---

## Key Learnings

1. Hardware timer-based delay implementation
2. GPIO configuration and control
3. Accurate timing using prescaler settings
4. Square wave generation using delay loops
5. Practical use of STM32 HAL drivers

---
