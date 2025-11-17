#include <stdio.h>
#include <stdint.h>

uint16_t adc_read_raw()
{
    static uint16_t v = 500;
    v += (v % 13) - 6;
    return v;
}

uint16_t oversampled_adc()
{
    uint32_t total = 0;
    for (int i = 0; i < 16; i++)
        total += adc_read_raw();
    return total >> 4;  // divide by 16
}

int main()
{
    for (int i = 0; i < 20; i++)
        printf("ADC(oversampled) = %u\n", oversampled_adc());

    return 0;
}
