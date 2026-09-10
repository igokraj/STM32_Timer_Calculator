# STM32 Timer Calculator — PSC / ARR

A simple web-based calculator for computing the **Prescaler (PSC)** and **Counter Period (ARR)** registers for STM32 timers, based on the timer clock and the desired Update Event interrupt period.

<img width="1002" height="1277" alt="image" src="https://github.com/user-attachments/assets/763b21f1-5072-4b57-b343-2a63b5abf097" />

🔗 **Demo:** _(GitHub Pages link once enabled)_

## How it works

Based on the formula:

```
f_timer = f_clock / ((PSC+1) × (ARR+1))
```

The algorithm searches for a PSC/ARR pair (16-bit range: 0–65535) that minimizes rounding error against the target period.

## Usage

1. Enter the timer clock frequency in MHz (APB timer clock, not SYSCLK — check it in CubeMX → Clock Configuration).
2. Enter the desired period in seconds (e.g. `0.02` for 50 Hz).
3. Click **Calculate** — you'll get PSC, ARR, the actual achieved period, and the error in %.

The LED in the results blinks live at the computed period — a quick visual sanity check.

## Notes

- The calculator assumes a 16-bit timer (like TIM1/TIM3/TIM4 on STM32F4). For very long periods at a low clock, it suggests a 32-bit timer (TIM2/TIM5) or a software counter in the callback.
- Default values tested on NUCLEO-F446RE (APB1 timer clock 84 MHz, APB2 timer clock 180 MHz).

## License

MIT
