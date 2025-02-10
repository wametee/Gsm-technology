# Global System for Mobile (GSM)

## Send SMS from a Command Line Interface (CLI)
This document covers the process of sending SMS messages using a command-line interface (CLI). It delves into establishing connections, issuing AT commands, and leveraging Windows and Java tools to interact with a GSM modem or phone.

---

## Table of Contents
1. [Windows Commands and Terminal Connection](#windows-commands-and-terminal-connection)
2. [HyperTerminal and Modem Connection](#hyperterminal-and-modem-connection)
3. [Sending AT Commands](#sending-at-commands)
4. [Cscript.exe - Windows Script Host](#cscriptexe---windows-script-host)
5. [MSCOMM32.OCX - GSM Modem Communication](#mscomm32ocx---gsm-modem-communication)
6. [Send & Receive SMS using Hayes AT Commands](#send--receive-sms-using-hayes-at-commands)
7. [Comm.jar & comm32.dll](#commjar--comm32dll)
8. [Best Practices](#best-practices)

---

## 1. Windows Commands and Terminal Connection
### Establishing Terminal Communication
To interact with a GSM modem via CLI:
- Open **Command Prompt (cmd.exe)** in Windows.
- Identify the correct **COM port** connected to the GSM device:
  ```sh
  mode
  ```
- Open a serial connection using PowerShell:
  ```powershell
  $port= new-Object System.IO.Ports.SerialPort COM3,9600,None,8,one
  $port.open()
  ```

---

## 2. HyperTerminal and Modem Connection
### Using HyperTerminal for Modem Communication
HyperTerminal allows you to send AT commands to a modem:
- Open **HyperTerminal** (`hypertrm.exe`).
- Configure the **COM port settings**:
  - **Bits per second**: 9600 (or as per modem specs)
  - **Data bits**: 8
  - **Parity**: None
  - **Stop bits**: 1
  - **Flow control**: None
- Establish a connection and type `AT` to check modem response (`OK`).

---

## 3. Sending AT Commands
AT (Attention) commands are used to interact with the GSM modem:
- **Check connection**:
  ```sh
  AT
  ```
  Response:
  ```sh
  OK
  ```
- **Send an SMS**:
  ```sh
  AT+CMGF=1   # Set to text mode
  AT+CMGS="+1234567890"  # Recipient phone number
  > Hello, this is a test message. (Press CTRL+Z to send)
  ```
  Response:
  ```sh
  +CMGS: 23  # Message sent successfully
  ```

---

## 4. Cscript.exe - Windows Script Host
### Automating SMS with Windows Scripting
`Cscript.exe` executes Windows script files such as `.vbs` and `.js`.
Example of sending an SMS using **VBScript**:
```vbscript
Dim objShell
Set objShell = WScript.CreateObject("WScript.Shell")
objShell.Run "cmd /c echo AT+CMGF=1 > COM3"
objShell.Run "cmd /c echo AT+CMGS="+1234567890" > COM3"
objShell.Run "cmd /c echo Hello, SMS from script. > COM3"
objShell.Run "cmd /c echo ^Z > COM3"
Set objShell = Nothing
```

---

## 5. MSCOMM32.OCX - GSM Modem Communication
### What is MSCOMM32.OCX?
`MSCOMM32.OCX` is an ActiveX control used to communicate with serial ports in **Visual Basic applications**.

To register it on Windows:
```sh
regsvr32 MSCOMM32.OCX
```
**Example VBScript for sending SMS:**
```vbscript
Set MSComm1 = CreateObject("MSCommLib.MSComm")
MSComm1.CommPort = 3
MSComm1.Settings = "9600,N,8,1"
MSComm1.PortOpen = True
MSComm1.Output = "AT+CMGF=1" & vbCrLf
MSComm1.Output = "AT+CMGS=\"+1234567890\"" & vbCrLf
MSComm1.Output = "Hello from VB!" & Chr(26)
MSComm1.PortOpen = False
```

---

## 6. Send & Receive SMS using Hayes AT Commands
Hayes AT Commands are industry-standard commands for modem control.
- **Send SMS (Text Mode)**:
  ```sh
  AT+CMGF=1
  AT+CMGS="+1234567890"
  > Message Body (CTRL+Z to send)
  ```
- **Read SMS Messages**:
  ```sh
  AT+CMGL="ALL"
  ```
  Response:
  ```sh
  +CMGL: 1,"REC UNREAD","+1234567890",,"21/10/22,12:34:56"
  Hello, this is a received message.
  ```
- **Delete SMS Messages**:
  ```sh
  AT+CMGD=1,4
  ```

---

## 7. Comm.jar & comm32.dll
### Java Serial Communication with `comm.jar`
The `comm.jar` and `javax.comm` library allow Java applications to interact with serial ports.

**Example Java Code to Send SMS:**
```java
import java.io.*;
import java.util.*;
import javax.comm.*;

public class SMSSender {
    public static void main(String[] args) throws Exception {
        CommPortIdentifier portId = CommPortIdentifier.getPortIdentifier("COM3");
        SerialPort serialPort = (SerialPort) portId.open("SMSApp", 2000);
        OutputStream outputStream = serialPort.getOutputStream();

        outputStream.write("AT+CMGF=1\r".getBytes());
        outputStream.write("AT+CMGS=\"+1234567890\"\r".getBytes());
        outputStream.write("Hello from Java!\u001A".getBytes());

        outputStream.close();
        serialPort.close();
    }
}
```

---

## 8. Best Practices
- **Use appropriate COM port settings** matching your modem.
- **Ensure correct AT command syntax** to avoid errors.
- **Test AT commands in HyperTerminal** before automating.
- **Handle exceptions in Java/Python scripts** to prevent crashes.
- **Register ActiveX controls (`MSCOMM32.OCX`) properly** when using VBScript.
- **Use `comm.jar` for Java applications** requiring serial communication.

---

## Conclusion
This guide provides an in-depth exploration of sending SMS via CLI using Windows commands, scripting, AT commands, and Java-based solutions. Mastering these techniques allows automation and remote control over SMS messaging.

---

## References
- [Hayes AT Command Reference](https://en.wikipedia.org/wiki/Hayes_command_set)
- [Java Comm API](https://www.oracle.com/java/technologies/java-communications.html)
- [MSCOMM32.OCX Documentation](https://support.microsoft.com/en-us)
 