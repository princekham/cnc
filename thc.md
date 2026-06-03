### THC
- https://github.com/guiguijke/SmartTHC

- I used visual studio to build.
- I opened the whole folder and visual studio began to install necessary dependencies.

```
// ============================================================================
// PINS - Arduino Uno R4 Minima
// ============================================================================

// Plasma & THC I/O
#define PLASMA_PIN      12  // Input: plasma arc OK signal
#define ENABLE_PIN      10  // Input: THC enable (pull-up)
#define THC_OFF_PIN     11  // Input: THC off signal
#define PLASMA_VOLTAGE  A0  // ADC: plasma voltage

// Z motor control
#define DIR_PIN         8   // Direction
#define STEP_PIN        6   // Step
#define SWITCH1         9   // Output switch 1
#define SWITCH2         13  // Output switch 2

// Rotary encoder KY-040
#define ENCODER_PIN_A   4   // CLK
#define ENCODER_PIN_B   5   // DT
#define BUTTON_PIN      7   // SW (button)

// X/Y speed interrupts
#define STEP_X_PIN      2   // X interrupt
#define STEP_Y_PIN      3   // Y interrupt
```

### EasyEDA

- 6 pins : PZ254V-11-06P
- 4 pins : PZ254V-11-04P
