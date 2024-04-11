# STM32F401CCU6_TIMER_LED

https://www.digikey.in/en/maker/projects/getting-started-with-stm32-timers-and-timer-interrupts/d08e6493cefa486fb1e79c43c0b08cc6

https://stm32-base.org/boards/STM32F401CCU6-WeAct-Black-Pill-V1.2.html



84MHz -> /(8400-1) (Prescalar) -> 10kHz (0.1ms) -> We can count up to 10000 to get 1sec pulse(1Hz)

count up to 5000 to get 0.5sec pulse(2Hz)

count up to 1000 to get 0.1sec pulse(10Hz)

and so on

Before While loop to start the timer
HAL_TIM_Base_Start(&htim10);
timer_val = __HAL_TIM_GET_COUNTER(&htim10);

Inside While loop to toggle the led when we count up to a desired number 
// 10000=10kHz corresponds to 1Hz, 5000 to 2Hz and so on
if (__HAL_TIM_GET_COUNTER(&htim10)-timer_val>=5000)
{
 HAL_GPIO_TogglePin(STATUS_GPIO_Port, STATUS_Pin);
 timer_val=__HAL_TIM_GET_COUNTER(&htim10);
}

We do not need the delay now and this runs in non-blocking mode. 
