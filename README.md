# BBB_Serial_Port
BeagleBone Black read serial port

## Description

This is a simple C++ program designed to run on a BeagleBone system. It reads a message from UART-1 (`/dev/ttyO1`) and writes the received message into a text file located at `/home/debian/rms/tokenfile.txt`. If the message size is less than 142 bytes, it flushes the UART buffer and retries.

---

## Features

- Configures UART-1 with 115200 baud rate and 8N1 settings.
- Reads ASCII text from the UART port.
- Ensures full data reception (minimum 142 bytes).
- Logs the received data to a file.
- Echoes the received data back through UART.
- Appends data to an existing file or creates it if not present.

---

## File Structure

- **Source File**: `BBB_rdSerial.cpp`
- **Log File Output**: `/home/debian/rms/tokenfile.txt`

---

## Dependencies

Standard C++ and POSIX libraries:
- `<iostream>`, `<fstream>`, `<cstring>`, `<unistd.h>`
- `<fcntl.h>`, `<errno.h>`, `<termios.h>`, `<filesystem>`

Ensure your system supports:
- POSIX serial communication
- File I/O

---

## Compile Instructions

To compile this code on a Linux-based system (e.g., BeagleBone), run:

```bash
g++ beagle_test.cpp -o beagle_test
