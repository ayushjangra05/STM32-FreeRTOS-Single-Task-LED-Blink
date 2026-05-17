# STM32 FreeRTOS Single Task LED Blink

A basic FreeRTOS-based embedded systems project implemented on the STM32F446RE Nucleo Board to demonstrate RTOS task creation, LED blinking, and SWV ITM trace debugging using CMSIS-RTOS V2.

---

## Overview

This project demonstrates the implementation of a single FreeRTOS task on the STM32F446RE microcontroller using STM32CubeIDE and STM32CubeMX.

The RTOS task periodically:

- Toggles the onboard LED
- Sends execution messages to the SWV ITM Data Console
- Demonstrates task scheduling using `osDelay()`

The project uses:

- FreeRTOS Middleware
- CMSIS-RTOS V2 API
- SWV ITM Trace Debugging

---

## Features

- FreeRTOS task creation
- LED blinking using RTOS scheduling
- SWV ITM console tracing
- CMSIS-RTOS V2 implementation
- Non-blocking task delay using `osDelay()`
- Real-time debugging support

---

## Hardware Requirements

- STM32 Nucleo-F446RE Development Board
- USB Type-A to Mini-B Cable

---

## Software Requirements

- STM32CubeIDE
- STM32CubeMX
- FreeRTOS Middleware

---

## Peripheral Configuration

| Peripheral | Configuration |
|------------|----------------|
| PA5 | GPIO Output (Onboard LED) |
| SYS Debug | Trace Asynchronous SW |
| Timebase Source | TIM6 |
| RTOS Interface | CMSIS_V2 |

---

## RTOS Task Configuration

| Task Name | Function |
|------------|-----------|
| Task_1 | LED Toggle and Console Trace |

The task executes every 500 ms using:

```c
osDelay(500);
```

---

## Working Principle

FreeRTOS manages task execution using a preemptive scheduler.

The single RTOS task:

1. Toggles the onboard LED
2. Prints a debug message using SWV ITM
3. Delays for 500 ms
4. Repeats continuously

The scheduler automatically handles task blocking and CPU management.

---

## Source Code

### SWV ITM Retarget Function

```c
int _write(int file, char *ptr, int len)
{
    for (int i = 0; i < len; i++)
    {
        ITM_SendChar(*ptr++);
    }

    return len;
}
```

---

### Task Function

```c
void Task1_function(void *argument)
{
    for(;;)
    {
        HAL_GPIO_TogglePin(LED_GPIO_Port, LED_Pin);

        printf("Task_1 Executing for LED Toggle \n");

        osDelay(500);
    }
}
```

---

## SWV ITM Trace Debugging

The SWV ITM Data Console is used for:

- Real-time task monitoring
- Viewing debug messages
- Verifying task execution timing
- Non-intrusive embedded debugging

### Configuration

- Enable Serial Wire Viewer (SWV)
- Select Port 0
- Set Core Clock to 84 MHz
- Start Trace during debugging

---

## Build and Run

1. Open the project in STM32CubeIDE
2. Configure FreeRTOS middleware
3. Build the project
4. Connect STM32 board via USB
5. Start debugging mode
6. Enable SWV ITM Data Console
7. Start Trace and resume execution

---

## Expected Output

- Onboard LED blinks every 500 ms
- SWV ITM console displays:

```text
Task_1 Executing for LED Toggle
```

- Stable RTOS task execution without timing drift

---

## Learning Outcomes

- Understanding RTOS fundamentals
- FreeRTOS task management
- CMSIS-RTOS V2 API usage
- SWV ITM debugging
- Task scheduling using osDelay()
- Embedded systems debugging techniques

---

## Future Improvements

- Add multiple RTOS tasks
- Implement task priorities
- Add UART communication
- Integrate sensor interfacing
- Use semaphores and queues

---

## Author

**Ayush Jangra**  
ECE Student | Chitkara University
