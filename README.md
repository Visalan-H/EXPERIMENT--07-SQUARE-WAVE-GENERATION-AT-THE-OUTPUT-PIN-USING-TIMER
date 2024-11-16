# EXPERIMENT--05-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER

### Aim:
To generate a PWM wave at the timer pin output and  simuate it on  proteus using an virtual oscilloscope  

### Components required:
STM32 CUBE IDE, Proteus 8 simulator .

### Theory:

The timer modules can operate a variety of modes one of which is the PWM mode. Where the timer gets clocked from an internal source and counts up to the auto-reload register value, then the output channel pin is driven HIGH. And it remains until the timer counts reach the CCRx register value, the match event causes the output channel pin to be driven LOW. And it remains until the timer counts up to the auto-reload register value, and so on.

The resulting waveform is called PWM (pulse-width modulated) signal. Whose frequency is determined by the internal clock, the Prescaler, and the ARRx register. And its duty cycle is defined by the channel CCRx register value. The PWM doesn’t always have to be following this exact same procedure for PWM generation, however, it’s the very basic one and the easier to understand the concept. It’s called the up-counting PWM mode. We’ll discuss further advanced PWM generation techniques as we go on in this series of tutorials.

The following diagram shows you how the ARR value affects the period (frequency) of the PWM signal. And how the CCRx value affects the corresponding PWM signal’s duty cycle. And illustrates the whole process of PWM signal generation in the up-counting normal mode.

STM32 Timers – PWM Output Channels

Each Capture/Compare channel is built around a capture/compare register (including a shadow register), an input stage for capture (with a digital filter, multiplexing, and Prescaler) and an output stage (with comparator and output control). The output stage generates an intermediate waveform which is then used for reference: OCxRef (active high). The polarity acts at the end of the chain.
<img src="https://github.com/vasanthkumarch/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/36288975/87457b57-4311-440b-8cbe-a9d78db4335a" width="500">

STM32 Timers In PWM Mode

Pulse width modulation mode allows generating a signal with a frequency determined by the value of the TIMx_ARR register and a duty cycle determined by the value of the TIMx_CCRx register. The PWM mode can be selected independently on each channel (one PWM per OCx output) by writing 110 (PWM mode 1) or ‘111 (PWM mode 2) in the OCxM bits in the TIMx_CCMRx register. The user must enable the corresponding preload register by setting the OCxPE bit in the TIMx_CCMRx register, and eventually the auto-reload preload register by setting the ARPE bit in the TIMx_CR1 register.

OCx polarity is software programmable using the CCxP bit in the TIMx_CCER register. It can be programmed as active high or active low. For applications where you need to generate complementary PWM signals, this option will be suitable for you.

In PWM mode (1 or 2), TIMx_CNT and TIMx_CCRx are always compared to determine whether TIMx_CCRx≤TIMx_CNT or TIMx_CNT≤TIMx_CCRx (depending on the direction of the counter).

The timer is able to generate PWM in edge-aligned mode or center-aligned mode depending on the CMS bits in the TIMx_CR1 register.
STM32 PWM Frequency

In various applications, you’ll be in need to generate a PWM signal with a specific frequency. In servo motor control, LED drivers, motor drivers, and many more situations where you’ll be in need to set your desired frequency for the output PWM signal.

The PWM period (1/FPWM) is defined by the following parameters: ARR value, the Prescaler value, and the internal clock itself which drives the timer module FCLK. The formula down below is to be used for calculating the FPWM for the output. You can set the clock you’re using, the Prescaler, and solve for the ARR value in order to control the FPWM and get what you want.

STM32 PWM Frequency Formula - STM32 PWM Frequency Equation
<img src="https://github.com/vasanthkumarch/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/36288975/aca8a20e-9b99-40c1-bada-f31accaa2ae9" width="400">

STM32 PWM Duty Cycle

In normal settings, assuming you’re using the timer module in PWM mode and generating PWM signal in edge-aligned mode up-counting configuration. The duty cycle percentage is controlled by changing the value of the CCRx register. And the duty cycle equals (CCRx/ARR) [%].
<img src="https://github.com/vasanthkumarch/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/36288975/58ce0807-331e-49f7-bc8d-373f82592a92" width="400">



<h3>Step1: Open CubeMX & Create New Project</h3>
<img src="https://user-images.githubusercontent.com/36288975/226189166-ac10578c-c059-40e7-8b80-9f84f64bf088.png" width="400">

<h3>Step2: Choose The Target MCU & Double-Click Its Name select the target to be programmed as shown below and click on next</h3>
<img src="https://user-images.githubusercontent.com/36288975/226189215-2d13ebfb-507f-44fc-b772-02232e97c0e3.png" width="400">
<img src="https://user-images.githubusercontent.com/36288975/226189230-bf2d90dd-9695-4aaf-b2a6-6d66454e81fc.png" width="400">
<img src="https://user-images.githubusercontent.com/36288975/226189280-ed5dcf1d-dd8d-43ae-815d-491085f4863b.png" width="400">

<h3>Step3: Configure Timer2 Peripheral To Operate In PWM Mode With CH1 Output</h3>
<img src="https://github.com/vasanthkumarch/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/36288975/682c851a-7dfe-4089-8395-f76088d43896" width="400">

<h3>Step4: Set The RCC External Clock Source</h3>
<img src="https://github.com/vasanthkumarch/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/36288975/8888af3b-63e2-4760-a51b-17b477763941" width="400">
<p>STM32 RCC External Clock Selection CubeMX</p>

<h3>Step5: Go To The Clock Configuration</h3>

<h3>Step6: Set The System Clock To Be 72MHz</h3>
<img src="https://github.com/vasanthkumarch/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/36288975/4ea03faa-fb90-4b31-8079-3db5f959f2c3" width="400">

<h3>Step7: Name & Generate The Project Initialization Code For CubeIDE or The IDE You’re Using</h3>

<h3>Step8: Creating Proteus Project and Running the Simulation</h3>
<p>We are now at the last part of the step-by-step guide on how to simulate the STM32 project in Proteus.</p>

<h3>Step9: Create a New Proteus Project and Place STM32F40xx</h3>
<p>This is the same MCU for which the project was created in STM32Cube IDE.</p>

<h3>Step10: After Creation of the Circuit as Per Requirement</h3>
<img src="https://github.com/vasanthkumarch/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/36288975/4f377f5e-bdda-489e-a416-c712c893831d" width="400">

<h3>Step11: Double-Click on the MCU Part to Open Settings</h3>
<p>Next to the Program File option, provide the full path to the Hex file generated using STM32Cube IDE. Then set the external crystal frequency to 8M (i.e., 8 MHz). Click OK to save the changes.</p>

<h3>Step12: Click on Debug and Simulate Using the Simulation Option</h3>
<img src="https://github.com/vasanthkumarch/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/36288975/b8efbfc2-f0c5-4106-8117-3a6e7ac87f6c" width="400">


## STM 32 CUBE PROGRAM :

```
HAL_TIM_Base_Start(&htim2);
HAL_TIM_PWM_Init(&htim2);
HAL_TIM_PWM_Start(&htim2,TIM_CHANNEL_1);
```
<h3>Output Screenshots of Proteus</h3>
<img src="https://github.com/user-attachments/assets/48bf4a42-bde0-4489-b65f-d406ada862ab" width="400">


 
 <h3>Circuit Diagram</h3>
<img src="https://github.com/user-attachments/assets/f7d9fab6-5bc0-497e-8df5-95672fcb5918" width="400">



## DUTY CYCLE AND FREQUENCY CALCULATION 


<h3>Pulse at 500</h3>
<img src="https://github.com/user-attachments/assets/11c95597-fdcc-4890-b34a-10a678d70a41" width="400">

```
TON = 3 x 10 x 10^-6
    = 0.00003
TOFF=0.00003
TOTAL TIME = TON + TOFF
           = 0.00003+0.00003 
           = 0.00006
FREQUENCY = 1/(TOTAL TIME) 
          =1/0.00006 
          = 16666.7
DUTY CYCLE = TON /(TON+TOFF)
           = 0.00003/0.00006
           = 0.5
      IN % =0.5*100 
           = 50 %
```

<h3>Pulse at 700</h3>
<img src="https://github.com/user-attachments/assets/0b78741e-28d3-46d5-bd2c-f662ad87637e" width="400">

```
TON = 4 x 10 x 10^-6
    = 0.00004
TOFF= 2 x 10 x 10^-6
    = 0.00002
TOTAL TIME = TON + TOFF
           = 0.00004+0.00002
           = 0.00006
FREQUENCY = 1/(TOTAL TIME)
          = 16666.7
DUTY CYCLE = TON /(TON+TOFF)
           = 0.00004/0.00006
           = 0.7
      IN % =0.7*100 
           = 70 %
```

<h3>Pulse at 900</h3>
<img src="https://github.com/user-attachments/assets/4d1ca5c4-4ae8-4a5a-a608-d575ae0251ab" width="400">


```
TON = 1 x 50 x 10^-6
    = 0.00005
TOFF= 0.1 x 50 x 10^-6
    = 0.000005
TOTAL TIME = TON + TOFF
           = 0.00005 + 0.000005
           = 0.000055
FREQUENCY = 1/(TOTAL TIME)
          = 18181.82
DUTY CYCLE = TON /(TON+TOFF)
           = 0.00005/0.000055
           = 0.9
      IN % =0.9*100 
           = 90 %
```
## Result :
A PWM Signal is generated using the following frequency and various duty cycles are simulated 
