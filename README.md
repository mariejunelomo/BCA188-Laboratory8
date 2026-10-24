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
