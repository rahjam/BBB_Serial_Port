# BBB_rdSerial

A C++ application for reading text messages from UART-1 serial port and saving them to a text file on BeagleBone Black.

## Description

This program establishes a serial connection to UART-1 (`/dev/ttyO1`), reads incoming text messages, and writes them to a file while also echoing the data back to the serial port. It's designed for BeagleBone Black single-board computers but can be adapted for other Linux systems.

## Features

- Serial communication via UART-1 at 115200 baud rate
- Automatic file creation and appending
- Data validation (expects minimum 142 bytes)
- Echo functionality - sends received data back to serial port
- Error handling for serial port operations
- Configurable timeout settings

## Hardware Requirements

- BeagleBone Black or compatible single-board computer
- Serial device connected to UART-1 (`/dev/ttyO1`)
- Properly configured serial pins

## Software Requirements

- Linux operating system (tested on Debian)
- GCC compiler with C++17 support
- Standard C++ libraries
- POSIX terminal control libraries

## Installation

1. Clone or download the source code
2. Compile the program:
```bash
g++ -std=c++17 -o BBB_rdSerial BBB_rdSerial.cpp
```

## Configuration

### Serial Port Settings
- **Port:** `/dev/ttyO1` (configurable via `DEFAULT_PORT`)
- **Baud Rate:** 115200 (configurable via `BAUD_RATE`)
- **Data Bits:** 8
- **Parity:** None
- **Stop Bits:** 1
- **Flow Control:** None

### File Settings
- **Output Directory:** `/home/debian/rms/` (configurable via `Path`)
- **Output File:** `tokenfile.txt`
- **Write Mode:** Append

## Usage

1. Ensure the serial device is connected to UART-1
2. Make sure the output directory exists:
```bash
mkdir -p /home/debian/rms/
```
3. Run the program:
```bash
sudo ./BBB_rdSerial
```

**Note:** Root privileges may be required for serial port access.

## Program Flow

1. Opens/creates the output file in append mode
2. Configures the serial port with specified settings
3. Waits for incoming serial data
4. Validates received data (minimum 142 bytes expected)
5. Writes valid data to file
6. Echoes data back to serial port
7. Closes file and serial port connections

## Error Handling

The program includes error handling for:
- Serial port opening failures
- Terminal attribute configuration errors
- File operations
- Partial data reads (less than 142 bytes)
- Buffer flushing operations

## Customization

### Changing Serial Port
```cpp
#define DEFAULT_PORT "/dev/ttyUSB0"  // Example for USB serial adapter
```

### Changing Baud Rate
```cpp
#define BAUD_RATE B9600  // Example for 9600 baud
```

### Changing Output Directory
```cpp
#define Path "/custom/path/"
```

### Adjusting Data Size Validation
```cpp
if (num_bytes < 142){  // Change 142 to your required minimum
```

## Troubleshooting

### Permission Denied
- Run with `sudo` or add user to `dialout` group:
```bash
sudo usermod -a -G dialout $USER
```

### Device Not Found
- Verify the serial device exists: `ls -la /dev/ttyO*`
- Check if UART is enabled in device tree

### Partial Reads
- The program automatically flushes and retries for reads < 142 bytes
- Adjust the minimum byte requirement if needed

## Technical Details

### Serial Configuration
- Non-canonical mode (raw input)
- No echo or special character processing
- 1-second timeout for read operations
- Hardware flow control disabled

### Memory Management
- 256-byte read buffer
- Buffer cleared before each read operation
- Automatic memory cleanup on program exit

## License

Your copyright notice here.

## Author

RaJa

## Version History

- Initial version: Basic UART read/write functionality with file logging

## Contributing

When contributing to this project, please:
1. Test on actual hardware
2. Maintain compatibility with BeagleBone Black
3. Follow existing code style
4. Update documentation as needed
