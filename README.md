# STM32F1_ADXL345_BandPass
STM32F1 Project implementing a digital filter with an ADXL345 accelerometer over I2C.

According to the acceleration function, the first derivative of the velocity. Which is given by the ADXL345 as a value x,y,z according to de differential in the transductor inside of the sensor which measures the acceleration of the three axes:

![OFF](https://github.com/Miguelest07/STM32F1_ADXL345_DigitalFilter/blob/main/1.PNG)

Considering x as a variable of the sensor output, which will change over time through the deterministic system that corresponds to the microcontroller.

![OFF](https://github.com/Miguelest07/STM32F1_ADXL345_DigitalFilter/blob/main/2.PNG)

According to the final function, the simplest way of obtaining the value of the acceleration in each axis is just make a subtraction of the last value measured with the actual value measured. This system does not have any kind of filter that suppress the noise that could disturb the final output.


Stationary state response of the sensor before filtering.

![OFF](https://github.com/Miguelest07/STM32F1_ADXL345_DigitalFilter/blob/main/3.PNG)

At the stationary state, the noise is notorious. The graph show that the peak average of the noise is almost 1 and it also has a few peaks of 2. The desired output should be 0 since the device is in a stationary state, it does not have any acceleration.

The digital filter can be implemented with a function which determines the unwanted behaviour and states the next following rules: If the dx value is between the useful data, the value of the output will be the same of the input. In the other way the value of the input will be remain as the same of the previous value.

![OFF](https://github.com/Miguelest07/STM32F1_ADXL345_DigitalFilter/blob/main/4.PNG)

According to the graph the values represented as a noise are below of three, so the minimum value to supress is the number 3.


Stationary state response of the sensor after filtering

![OFF](https://github.com/Miguelest07/STM32F1_ADXL345_DigitalFilter/blob/main/5.PNG)

The previous graph show that the stationary state response of the signal signal is clear of noise due the digital filter applied.
When debugging the different axis of the sensor, the noise became stronger, in such a way that it almost shown peaks above of 150. That behaviour is not desired because it is not detecting the proper axis but if we take a detailed look over the signal, we can observe that the movement is being registered but the noise disturbs the data. So once obtained the maximum values gotten as a noise the maximum value to suppress is 100.


Once the values of the filter are gotten, the final function of the filter is:

![OFF](https://github.com/Miguelest07/STM32F1_ADXL345_DigitalFilter/blob/main/6.PNG)

The final function is given by applying the function of the filter in the first equation:

![OFF](https://github.com/Miguelest07/STM32F1_ADXL345_DigitalFilter/blob/main/7.PNG)

![OFF](https://github.com/Miguelest07/STM32F1_ADXL345_DigitalFilter/blob/main/8.PNG)

The axes of the sensor are shown correctly due the application of the filter.
