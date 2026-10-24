**BCA188 - Laboratory 8: Wired Interfaces**

**GPIO Pin Configuration**

| Signal | GPIO Used |
| ---------- | ------------- |
| UART TX    | 17            |
| UART RX    | 18            |
| I2C SDA    | 8             |
| I2C SCL    | 9             |
| SPI SCK    | 12            |
| SPI MOSI   | 11            |
| SPI MISO   | 13            |
| SPI CS     | 10            |

**Wiring Diagram**

UART:<img width="2000" height="1414" alt="Untitled (29 7 x 21 cm) (2)" src="https://github.com/user-attachments/assets/e0b345c2-8d38-434d-b7a1-525aa15d0184" />

SPI:<img width="2000" height="1414" alt="Untitled (29 7 x 21 cm) (1)" src="https://github.com/user-attachments/assets/93ce65c1-25b0-44a9-be1d-bc0502945418" />

I2C:<img width="2000" height="1414" alt="Untitled (29 7 x 21 cm)" src="https://github.com/user-attachments/assets/d0716f28-2f33-4b5a-8c3f-80cf1b40d58e" />

**Outputs**
1. UART
<img width="4032" height="3024" alt="706f89e6-253e-4951-9c7e-8edd691d6e1b" src="https://github.com/user-attachments/assets/c54c88ac-9acf-4016-a8e2-a0b41f739543" />
Serial Monitor:
   (with jumper wires)
  <img width="1920" height="1080" alt="uart_loopback (with jumper wires)" src="https://github.com/user-attachments/assets/e73a7915-4c28-4bd7-82de-b6a01e44e757" />
   (without jumper wires)
  <img width="1920" height="1080" alt="uart_loopback (without jumper wires)" src="https://github.com/user-attachments/assets/74b8135d-6264-43a5-a8d5-8d0c8e321558" />

2. I2C
<img width="4032" height="3024" alt="9a3da162-b894-41f3-902f-4c13dc80c2a3" src="https://github.com/user-attachments/assets/6bd4c277-1d20-4d91-91dd-ee4ba5da6b71" />
Serial Monitor:
   (with module)
<img width="1920" height="1080" alt="i2c_scanner (with jumper)" src="https://github.com/user-attachments/assets/f8924794-1ba4-446b-aa22-29114971d92b" />
   (without module)
<img width="1920" height="1080" alt="i2c_scanner (without jumper wires)" src="https://github.com/user-attachments/assets/625b0bca-7d7f-44ae-b29d-823f6c353ac3" />

3. SPI
<img width="4032" height="3024" alt="9912312c-f885-424e-8ecf-119592f28d54" src="https://github.com/user-attachments/assets/03c08b81-857f-4550-b4a0-dbdfd1943331" />
Serial Monitor:
   (with jumper)
<img width="1920" height="1080" alt="spi_loopback (with jumper)" src="https://github.com/user-attachments/assets/20f6799e-6581-4b9c-9e98-4912a854d1a2" />
   (without jumper)
<img width="1920" height="1080" alt="spi_loopback (without jumper wires)" src="https://github.com/user-attachments/assets/f9553aee-e38d-498f-907e-0a082dbfc586" />

7. Sketch at 9600, monitor at 115200
   SPI: <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/04eacdfe-4a48-4888-bbfe-1c15a27b1412" />
   UART:<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/ec89a9cf-9b29-4adb-aeee-c1d23c475152" />

9. Sketch at 9600, monitor at 9600
    SPI: <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5d53699e-82f6-4420-b513-a85f196e55e6" />
    UART:<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/089284f3-cab4-444a-8dc2-3d289610c6c8" />

**Guide Questions**

1. Why does UART need both sides to use the same baud rate, while SPI uses a clock line?

UART does not have a dedicated clock signal, so both devices must be configured to the same baud rate to send and receive bits at the correct timing. In contrast, SPI uses a clock line to coordinate when data is transmitted and received.

2. Why can two devices with the same address not share one I²C bus?

Each I²C device is identified by its address. If two devices have the same address, the controller cannot distinguish between them, and both may respond to the same command, resulting in communication conflicts.

3. Why is CS set HIGH between SPI transfers?

Setting CS HIGH deactivates the selected SPI device when a transfer is finished. When CS is pulled LOW, the device is selected and can communicate with the controller.

**Test Programs**

- **UART Loopback (`uart_loopback/uart_loopback.ino`)** – Sends `PING` through UART TX (GPIO 17) and reads the response through UART RX (GPIO 18).
- **I²C Scanner (`i2c_scanner/i2c_scanner.ino`)** – Searches for connected I²C devices using SDA (GPIO 8) and SCL (GPIO 9).
- **SPI Loopback (`spi_loopback/spi_loopback.ino`)** – Sends the byte `0xA5` through SPI and reads the returned byte using the configured SPI pins.

## Hardware

- ESP32-S3 development board
- I²C OLED module (for the I²C scanner test)
- Jumper wires
- USB cable for programming and power

## Loopback Connections

- **UART:** Connect GPIO 17 (TX) to GPIO 18 (RX).
- **SPI:** Connect GPIO 11 (MOSI) to GPIO 13 (MISO).
- **I²C:** Connect the OLED's SDA to GPIO 8 and SCL to GPIO 9, with VCC and GND connected appropriately.
