# ตัวอย่างโปรแกรม ESP32 GPIO

```c
#include "freertos/FreeRTOS.h"
#include "freertos/task.h"
#include "driver/gpio.h"

#define LED_PIN     GPIO_NUM_32  // กำหนดพอร์ตที่เชื่อมต่อกับ LED
#define BUTTON_PIN  GPIO_NUM_36 // กำหนดพอร์ตที่เชื่อมต่อกับ BUTTON

void app_main(void)
{
    // กำหนดทิศทางพอร์ต LED เป็น output
    gpio_set_direction(LED_PIN, GPIO_MODE_OUTPUT);   

    // กำหนดทิศทางพอร์ต BUTTON เป็น input
    gpio_set_direction(BUTTON_PIN, GPIO_MODE_INPUT);

    while(1) {       
        // อ่านค่าปุ่มกด ถ้าเป็นระดับ 0 ให้ LED ติด ถ้าเป็น 1 ให้ LED ดับ
        if (gpio_get_level(BUTTON_PIN) == 0) {  // If button is pressed
            gpio_set_level(LED_PIN, 1);         // Turn the LED on
        } else {
            gpio_set_level(LED_PIN, 0);         // Turn the LED off
        }

        vTaskDelay(1); // หน่วงเวลา 1 tick  (10 ms) เพื่อป้องกันไม่ให้ WDT ทำการรีเซ็ตระบบ
    }
}
```
