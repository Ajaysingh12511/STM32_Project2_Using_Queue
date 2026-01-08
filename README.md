FreeRtos---->Implementation of Communication between two task by using Que this is for STM32
1.Define Two separate task 
2.Creat one Queue
this project is controlling FAN switching based on Temperature values.

1. Threads and Queue


Threads:

defaultTask: Placeholder, does nothing.
TempCheck: Simulates temperature readings and sends them to a queue.
FanControl: Reads temperature from the queue and controls a fan based on the temperature.


Queue:

myQueue01: Used for communication between TempCheck and FanControl.

2. Temperature Simulation

TempCheck simulates a temperature sensor:

Starts at 25°C.
Increments by 1°C until it reaches 35°C, then resets to 25°C.
Sends the temperature to the queue every second.

3. Fan Control Logic

FanControl reads the temperature from the queue:

If temperature ≥ 30°C, turns the fan ON.
If temperature < 30°C, turns the fan OFF.
Prints the fan state to the console.


Observations and Suggestions
1. Queue Size and Data Type
The queue is created with a size of 5 and a data type of int. This is fine for this example, but ensure the queue size is sufficient for your real-world use case.

2. Error Handling
There is no error handling for queue operations (osMessageQueuePut, osMessageQueueGet). In a real application, you should check the return values and handle errors (e.g., queue full or empty).

3. Real-World Adaptation
Temperature Sensor:
Replace the simulated temperature with a real sensor (e.g., LM35, DS18B20) and read its value using HAL or LL drivers.

Fan Control:
Replace the printf with actual GPIO control to turn a fan on/off.

4. Thread Priorities
TempCheck has a lower priority (osPriorityLow6) than FanControl (osPriorityLow5). This is fine for this example, but ensure priorities match your system requirements.

5. Debugging
Use printf for debugging, but consider using a proper logging system or RTOS-aware debug tools for production code.

