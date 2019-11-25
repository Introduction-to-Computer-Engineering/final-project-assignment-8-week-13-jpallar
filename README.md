This assignment [README](README.md) is _intentionally_ blank. It is part of the assignment to fill it. Read the [requirements](requirements.md) and [criteria](criteria.md).

<header> Oscilloscope </header>

<title>Part i. </title>

<title> Part ii </title>
[Standalone Rigol Function video]https://photos.app.goo.gl/8eP3Gk7zjhSjB1fF9

<title> Part iii </title> 
[Pulse With Modulation video]https://photos.app.goo.gl/D4ta7tvuR4jfj43FA that shows the code down low working the servo motors. 
Code:
basic.forever(function () {
    pins.servoSetPulse(AnalogPin.P0, 3500);
})

<title> Part iv </title> 
Using what was learned on part i and iii, created a code that allowed for the extension of the wave lengths. [video]https://drive.google.com/file/d/1W6JHFHM1cMT18kYS765pSNH6VbwBPQIu/view?usp=sharing

let percent_list: number[] = [15, 20, 30, 35, 40, 45, 50, 55, 60, 65, 70, 75, 80, 85, 90, 95, 90, 85, 80, 75, 70, 65, 60, 55, 50, 45, 40, 35, 30, 25, 20, 15];
let i: number = 0
const P: number = 20000 
basic.forever(function () {
    pins.servoSetPulse(AnalogPin.P0, P * percent_list[i] / 100.0);
    i = (i + 1) % percent_list.length
    basic.pause(2000);
})


<title> i2C Warmup </title> 

<title> i </title> 
The main issue with UART is that it is a 'asynchronous port.' This means that connected devices must first agree on data rate, communication is restricted to only two devices, hardware overhead, and data rate. SPI has issues because of the amount of pins needed, which effects layout, and the fact that it only allows for one master on the bus. I2C fixes these issues by giving these problems more capabilities. Asynchronous ports supports more slaves, it allows more masters on bus, and better communication rates.

<title> ii </title> 
The two wires for I2C are SDA and SCL. SDA is the clock signal and SCL is the data signal.

<title> iii </title> 
The clock distinguishes the master and slaves. It is always transmitted by the bus master, although some slaves can delay the master from sending data.

<title> iv </title> 
The two types of protocol frames are Address and Data. Address frames always come first and dictates the order of operations in an address. Data frames follow after address frames and begins the data transmitting process.

<title> v </title> 
What is the most appropriate trigger for capturing an I2C frame on the oscilloscope? Clock stretching is the most appropriate trigger for capturing an I2C frame on an oscilloscope. This is because the slaves hold the clock low, forcing the master to wait for its signal.

<title> vi (advanced) </title> 
If the micro:bit is configured by default as a master, and two micro:bits, connected to each other via the SDA and SCL lines, communicate over I2C? (Bonus for a convincing argument, one way or another.)

<title> i2C Write </title> 
[Write Code Wave Picture]https://drive.google.com/file/d/1z2_w0ebiZM4Jd7hbwXTNnrrM5e7ExiZj/view?usp=sharing

a. I captured two waves, one writing code on the SLA going up when the SLA improves wave length. 
b. When the i2C is not connected to anything it continues to receive some signals that I do not know where they come from. 
c. When testing the other writes to different addresses since the number is still correct the same outcome is the same. 

Code: 
basic.forever(function () {
    pins.i2cWriteNumber(30, 1500, NumberFormat.Int8LE, false)
})

<title> i2C Read </title> 
[Read Code Wave Length]https://drive.google.com/file/d/17aHMapHNtr6xaQkxTecolT_MDQLBLvyw/view?usp=sharing

d. The values viewed through the picture are of increasing SDA values 1 trasnmitting constant values of SLA 1 and 0. 
e. I do get different values, when moving the micro-bit the magnometer changes, while displaying the values I was getting big values as I moved it from 70 to 170 on the first shake and a continous shake would give values of 250. 

Code: 
basic.forever(function () {
    let numb1 = pins.i2cReadNumber(0x19E, NumberFormat.Int8LE, false);
    basic.showNumber(numb1);
})
