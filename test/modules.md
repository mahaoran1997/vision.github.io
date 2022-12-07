---
sort: 2
---

# Software Modules

There are two modules in our POVLib project: POV Module and HTML Module. We actually seperate them into two libraries because they can used individually without relying on each other. The POV module is to help programmers create patterns while the HTML module is to help programmers easily build a web server. The HTML module can also be used in many other scenarios.

## POV Module

The POV module contains a class called `POVLib` which is the same as our project name. There are in total 10 interfaces visible to external programmers.

```C++
class POVLib {
public:
    POVLib(int _led_pin, int _num_leds, int _brightness, int _rounds_per_min, int _intervals, char* _led_type, char* _color_order);
    void run_loop_body();
    void draw_curve(int interval_st, int interval_ed, int led_id, unsigned int color = CRGB::White);
    void draw_dot(int interval_id, int led_id, unsigned int color = CRGB::White);
    void draw_line(int interval_id, int led_st, int led_ed, unsigned int color = CRGB::White);
    void reset();
    void set_led(int led_id, unsigned int color);
    void set_texts(char* s);
    void show_texts();
};
```

- `POVLib(int _led_pin, int _num_leds, int _brightness, int _rounds_per_min, int _intervals, char* _led_type, char* _color_order);`
  - Constructor of POVLib: The first parameter is the pin number of LED. The second parameter is the number of leds we have on the stripe. The third specifies the brightness of LED and the fourth parameter specifies the speed of the motor. The fifth parameter is how many intervals we want to split for a single circle. The last two parameters are the type of our leds and the color order.
- `void run_loop_body();`
  - Function to show patterns. It changes LED values based on time. We need to frequently call this interface in the loop function.
- `void reset();`
  - This function resets all LEDs to black.
- `void draw_curve(int interval_st, int interval_ed, int led_id, unsigned int color = CRGB::White);`
  - We can draw a curve using this interface. The first two parameters specifies the start and end interval IDs of this curve and the third parameter specifies the LED ID of the curve. The last one gives the color of this curve. 
- `void draw_dot(int interval_id, int led_id, unsigned int color = CRGB::White);`
  - This function is used to draw a dot. The first parameter specifies the interval ID and the second parameter specifies the LED ID. The last one gives the color of this dot. 
- `void draw_line(int interval_id, int led_st, int led_ed, unsigned int color = CRGB::White);`
  - We can draw a line using this interface. The first parameter specifies the interval ID. The following two parameters specifies the start and end LED IDs of this line. The last one gives the color. 
- `void set_led(int led_id, unsigned int color);`
  - We can also directly manipulate LEDs through this function. We decide to expose this primitive function to external programmers to preserve flexibility.
- `void set_texts(char* s);`
  - Our POVLib supports showing texts. This interface is used to specify the texts to be shown.
- `void show_texts();`
  - Function to show texts. It changes LED values based on time. We need to frequently call this interface in the loop function.


## HTML Module

The interfaces of HTML Module is simple and is already covered in the step-by-step guide. Here we just show the formal interface:

```C++
class TemplateHtml {
public:
    static void initialize(int _button_num, String* _texts, const char* _ssid, const char* _passwd, int* _output_pattern_addr, char* _text_to_display);
    static void handle_client();
};
```