# Sending SMS from a Console Interface

This guide provides step-by-step instructions on how to send SMS from a console interface using various Linux AT commands and tools. It covers modem connection, issuing AT commands, and troubleshooting tips for seamless communication with GSM modems.

## Table of Contents
1. [Linux AT Commands](#linux-at-commands)
2. [Connecting to the Modem](#connecting-to-the-modem)
   - [Using /dev/ttyACM0](#using-devttyacm0)
   - [Using Socat and /dev/ttyUSB2](#using-socat-and-devttyusb2)
3. [AT Command Basics](#at-command-basics)
   - [Text vs PDU Mode](#text-vs-pdu-mode)
   - [Common AT Commands](#common-at-commands)
4. [Issuing AT Commands](#issuing-at-commands)
5. [Sending SMS with AT Commands](#sending-sms-with-at-commands)
6. [Dialing and Receiving Calls](#dialing-and-receiving-calls)
7. [Troubleshooting and Tips](#troubleshooting-and-tips)

## Linux AT Commands

AT commands (Attention commands) are instructions used to control modems. These commands enable communication with the modem for sending SMS, making calls, and querying network status. AT commands are sent via a serial interface such as `/dev/ttyACM0` or `/dev/ttyUSB2`.

## Connecting to the Modem

### Using `/dev/ttyACM0`
To connect to a modem via a serial port, use the following command:
```sh
cu -l /dev/ttyACM0
```
If `cu` is not installed, install it using:
```sh
sudo apt install cu
```

### Using Socat and `/dev/ttyUSB2`
If the modem is connected via USB, you can use `socat`:
```sh
socat - /dev/ttyUSB2
```
This creates a communication channel with the modem.

## AT Command Basics

### Text vs PDU Mode
Modems support two SMS modes:
- **Text Mode (AT+CMGF=1):** Human-readable format.
- **PDU Mode (AT+CMGF=0):** Encoded binary format.

Example:
```sh
echo -e "AT+CMGF=1\r" > /dev/ttyACM0
```

### Common AT Commands
1. **Check modem response:**
   ```sh
   AT
   ```
2. **Check signal strength:**
   ```sh
   AT+CSQ
   ```
3. **Set text mode for SMS:**
   ```sh
   AT+CMGF=1
   ```
4. **Select character set:**
   ```sh
   AT+CSCS="GSM"
   ```

## Issuing AT Commands
Commands are sent via the serial interface using tools like `echo` or `atinout`. Example:
```sh
echo -e "AT+CMGF=1\r" > /dev/ttyUSB2
```
Alternatively, use `atinout`:
```sh
echo -e "AT+CMGF=1\r" | atinout - /dev/ttyUSB2 -
```

## Sending SMS with AT Commands
To send an SMS in text mode:
```sh
AT+CMGF=1
AT+CMGS="+1234567890"
>Hello, this is a test message!
Ctrl+Z  # (Press Ctrl+Z to send)
```

## Dialing and Receiving Calls
To dial a number:
```sh
ATD+1234567890;
```
To answer an incoming call:
```sh
ATA
```
To hang up:
```sh
ATH
```

## Troubleshooting and Tips
- **Check modem connection:** Ensure the modem is recognized with `ls /dev/tty*`.
- **Verify modem response:** Run `AT` and check for `OK`.
- **Check network registration:**
  ```sh
  AT+CREG?
  ```
  - `0,1` or `0,5` indicates a registered network.
- **Restart modem if unresponsive:**
  ```sh
  AT+CFUN=1,1
  ```

By following this guide, you should be able to send SMS from a console interface effectively.

