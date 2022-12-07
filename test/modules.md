---
sort: 2
---

# Software Modules

There are two modules in our POVLib project: POV Module and HTML Module. We actually seperate them into two libraries because they can used individually without relying on each other. The POV module is to help programmers create patterns while the HTML module is to help programmers easily build a web server. The HTML module can also be used in many other scenarios.

## POV Module

The POV module contains a class called `POVLib` which is the same as our project name.
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



## HTML Module

This
```C++
class TemplateHtml {
public:
    static void initialize(int _button_num, String* _texts, const char* _ssid, const char* _passwd, int* _output_pattern_addr, char* _text_to_display);
    static void handle_client();
};
```