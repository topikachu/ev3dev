The [AM1808 SoC](EV3 Processor) has 2 Enhanced High Resolution Pulse Width
Modulators (eHRPWMs) and 3 Enhanced Capture Modules (eCAPs) that can be configured as PWMs.

The EHRPWMs actually have 2 PWM outputs (A/B) per device for a total of 4 PWMs.

##Usage
__EHRPWM0A__: Not used/connected

__EHROWM0B__: Drives the EV3 speaker to produce sound

__EHRPWM1A__: Output port B motor driver

__EHRPWM1B__: Output port A motor driver

__ECAP0__: Output port D motor driver

__ECAP1__: Output port C motor driver

__ECAP2__: Bluetooth "slow clock" @ 32.767kHz