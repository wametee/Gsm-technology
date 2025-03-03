# GSM AT Commands

## Introduction
AT commands, also known as Hayes command set, are instructions used to control modems. GSM (Global System for Mobile Communications) modems, mobile phones, and other devices can be controlled using these commands. The acronym "AT" stands for "Attention".

## History
The AT command set was developed by Dennis Hayes in 1981 for the Hayes Smartmodem. It has since become a standard for modems and is used widely in GSM and GPRS devices.

## Types of AT Commands
1. **Basic AT Commands**: These commands are used to perform basic modem operations such as dialing, hanging up, and answering calls.
2. **Extended AT Commands**: These commands are used for more advanced operations such as SMS, network registration, and GPRS settings.

## Standard AT Commands
### Hayes Standard AT Commands
- **ATA**: Answer an incoming call.
  ```plaintext
  ATA
  ```
- **ATH**: Hang up a call.
  ```plaintext
  ATH
  ```
- **ATD**: Dial a number.
  ```plaintext
  ATD1234567890;
  ```
- **ATZ**: Reset the modem to its default configuration.
  ```plaintext
  ATZ
  ```

### ETSI GSM 07.07 Specific AT Commands
- **AT+CMGF**: Set SMS message format.
  ```plaintext
  AT+CMGF=1  // Set SMS format to text mode
  AT+CMGF=0  // Set SMS format to PDU mode
  ```
- **AT+CMGS**: Send SMS message.
  ```plaintext
  AT+CMGS="1234567890"
  > Hello, this is a test message! // Text of the message
  ```
- **AT+CPIN**: Enter PIN code.
  ```plaintext
  AT+CPIN="1234"
  ```

### GPRS Specific Commands
- **AT+CGATT**: Attach or detach from GPRS service.
  ```plaintext
  AT+CGATT=1  // Attach to GPRS
  AT+CGATT=0  // Detach from GPRS
  ```
- **AT+CGDCONT**: Define PDP context.
  ```plaintext
  AT+CGDCONT=1,"IP","internet"
  ```

## Syntax Character Sets
AT commands use a standardized character set for proper communication between the device and the modem. These include:
- **Carriage Return (CR)**: `\r`
- **Line Feed (LF)**: `\n`

## AT Command Syntax
AT commands follow a specific syntax that includes:
- **Prefix**: "AT" (Attention)
- **Command**: Specific command to be executed
- **Parameter**: Optional parameters for the command

### Example:
```plaintext
AT+CMGF=1
```
In this example:
- "AT" is the prefix.
- "+CMGF" is the command.
- "=1" is the parameter.

## String Type Parameters
Some AT commands require string type parameters, usually enclosed in double quotes.

### Example:
```plaintext
AT+CMGS="1234567890"
```
In this example:
- "1234567890" is the string type parameter, representing the recipient's phone number.

## AT Error Commands
When an AT command fails or is incorrect, the modem returns error responses. Common error responses include:
- **ERROR**: General error
- **+CME ERROR**: Mobile equipment error
- **+CMS ERROR**: SMS-related error

### Example:
```plaintext
AT+CMGF=3
// Response: ERROR (because 3 is not a valid parameter for +CMGF)
```

## Real-World Scenarios
1. **Sending an SMS**:
   ```plaintext
   AT+CMGF=1  // Set SMS to text mode
   AT+CMGS="1234567890"
   > Hello, this is a test message! // Type message and press Ctrl+Z to send
   ```

2. **Establishing a GPRS Connection**:
   ```plaintext
   AT+CGATT=1  // Attach to GPRS
   AT+CGDCONT=1,"IP","internet"  // Define PDP context
   ATD*99***1#  // Dial to connect to GPRS
   ```

3. **Answering an Incoming Call**:
   ```plaintext
   RING  // Incoming call indication
   ATA  // Answer the call
   ```

4. **Hanging Up a Call**:
   ```plaintext
   ATH  // Hang up the call
   ```

## Conclusion
AT commands provide a powerful interface to control GSM modems and perform a variety of operations ranging from basic call handling to complex GPRS settings. Understanding and utilizing these commands can greatly enhance the capability of communication devices in real-world applications.