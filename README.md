# cklink-lite-fw-convertor

'cklink_lite.hex' shipped with C-Sky debug server can be programmed to STM32F103 bluepill to make your own CK-Link lite debugger.

The 'cklink_lite.hex' is designed to work with 'cklink_lite_iap.hex' (address range from 0x0800_0000 to 0x0800_4000). due to the circuit differences between Official CKLink lite debugger and STM32F103 bluepill, IAP bootloader + 'cklink_lite.hex' not works with STM32F103.

The firmware need changed to copy the vector table to the beginning of FLASH, then it can be used standalone without requirement to 'cklink_lite_iap.hex'.

To change 'cklink_lite.hex':

- open 'cklink_lite.hex' in your favorite editor.
- copy the lines before address 0x4100 and paste them to the start of file.
- modify address of all lines just copied, from '0x40XX' to '0x00XX'.
- fix the checksum of all lines just copied.

For convenient, I made this tool to convert 'cklink_lite.hex' automatically, the result firmware is 'cklink_lite-for_stm32f103.hex', you can program it to STM32F103 bluepill directly.

After programmed, connect the target device to STM32F103 as:

| STM32F103 | XT-E804  |
|-----------|----------|
| A0        | RESET    |
| A1        | CLK(PA1) |
| A5        | DAT(PA4) |
| 3V3       | 3V3      |
| GND       | GND      |



