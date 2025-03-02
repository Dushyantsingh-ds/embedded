## Embedded

## Concept
<details>
<summary>Click to expand!</summary>
   
   [- INO-EEPROM](https://github.com/Dushyantsingh-ds/embedded/blob/main/Projects/INO-EEPROM.md) <br>
   
</details>   

## Concept Projects
<details>
<summary>Click to expand!</summary>
   
[- Finding I2C connected devices](https://github.com/Dushyantsingh-ds/dotnet-api/blob/main/README.md) </br>
[- I2C connect 20x4 LCD(LiquidCrystalDisplay) ](https://github.com/Dushyantsingh-ds/embedded/blob/main/Projects/I2C%20connect%2020x4%20LCD(LiquidCrystalDisplay)%20with%20Ardunio.md  )  </br>
[- I2C connect 4 Button Keypad with Ardunio]( https://github.com/Dushyantsingh-ds/embedded/blob/main/Projects/I2C%20connect%204%20Button%20Keypad%20with%20Ardunio.md )</br>
[- Serial communication with Voltage & Current Sensor ](https://github.com/Dushyantsingh-ds/embedded/blob/main/Projects/Serial%20communication%20with%20Voltage%20%26%20Current%20Sensor%20Mega%202650.md  )  </br>
[- Simple On-OFF push button with LED ]( https://github.com/Dushyantsingh-ds/embedded/blob/main/Projects/Simple%20On-OFF%20push%20button%20with%20LED.md)  </br>
 [- Single phase Square Wave Generator Up to 1MHz](https://github.com/Dushyantsingh-ds/embedded/blob/main/Projects/Square%20Wave%20Generator%20Up%20to%201MHz%20.md)</br>
  [- Using Arduino board as ISP to program ATmega328 IC without a crystal](https://github.com/Dushyantsingh-ds/embedded/blob/main/Projects/Boot%20Atmega328%20with%20ISP%20to%20program%20ATmega328%20IC%20without%20a%20crystal.md)</br>
  [- Method 2- Boot Atmega328 with ISP to program ATmega328 IC with a crystal.md](https://github.com/Dushyantsingh-ds/embedded/blob/main/Projects/Method%202-%20Boot%20Atmega328%20with%20ISP%20to%20program%20ATmega328%20IC%20with%20a%20crystal.md)</br>
   [- Differential Input Signal Circuit - 12v to 5v.md](https://github.com/Dushyantsingh-ds/embedded/blob/main/Projects/Differential%20Input%20Signal%20Circuit%20%20-%2012v%20to%205v.md)</br>
      [- ULN2003 for 12v relay and MCU controlled - 5v to 12v.md](https://github.com/Dushyantsingh-ds/embedded/blob/main/Projects/ULN2003%20for%2012v%20relay%20and%20MCU%20controlled.md)</br>
[- Measuring Air Pressure HX710B with MCU.md](https://github.com/Dushyantsingh-ds/embedded/tree/main/Projects/Assets/AirPressure_V1)</br>      
</details>  


## Communication
<details>
<summary>Click to expand!</summary>
   ## RS485

   <details>
   <summary>Click to expand!</summary>
<summary>Click to expand!</summary>
  
 ## Flow
   <details>
   <summary>Click to expand!</summary>
      
   ##Communicate with multiple RS485 devices over an RS485-to-Ethernet converter using the Modbus RTU over TCP or a custom protocol depending on your devices. Here's a high-level plan for your application:
Steps to Build

### Identify Protocol

Are your RS485 devices using Modbus RTU over TCP
If Modbus, use a library like NModbus.

### Establish Connection with RS485 Devices

Communicate via TCP/IP to the RS485-to-Ethernet converter.
Get the IP address and port of the converter.
Implement socket programming if needed.

### Read Data from Each Device

Loop through each RS485 device address.
Send requests & process responses.

### Send Commands to Each Device Separately

Based on logic, send specific commands to each device.
Handle acknowledgment & error checking.
   </details>  
</details>
   ## Basic Oprations

   <details>
   <summary>Click to expand!</summary>

Here is a structured C# program that includes:
✅ Scanning all RS485 devices connected via an RS485-to-Ethernet converter
✅ Assigning device IDs using software configuration
✅ Sending commands to a particular device by ID
✅ Receiving data from a particular device by ID
✅ Reading data from all devices
✅ Sending data to all devices
✅ Auto-reconnect mechanism in case of disconnection

The program is written using Modbus TCP (NModbus4 library). If your devices use a custom protocol, I can modify it accordingly.

1. Install Required Library
Run this command in NuGet Package Manager Console:

```
Install-Package NModbus4
```

2. Full C# Program
Here’s the complete structured program:
```
using System;
using System.Net.Sockets;
using System.Threading;
using NModbus;

class RS485Manager
{
    private string converterIP = "192.168.1.100"; // Change to your RS485-to-Ethernet Converter IP
    private int port = 502; // Default Modbus TCP port
    private TcpClient client;
    private IModbusMaster master;

    public RS485Manager()
    {
        Connect();
    }

    // Auto-reconnect mechanism
    private void Connect()
    {
        while (true)
        {
            try
            {
                if (client != null && client.Connected)
                    return;

                Console.WriteLine("Connecting to RS485-to-Ethernet converter...");
                client = new TcpClient(converterIP, port);
                var factory = new ModbusFactory();
                master = factory.CreateMaster(client.GetStream());
                Console.WriteLine("Connected successfully!");
                break;
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Connection failed: {ex.Message}, Retrying in 5 seconds...");
                Thread.Sleep(5000);
            }
        }
    }

    // 1. Scan for Active Devices
    public void ScanDevices()
    {
        Console.WriteLine("\nScanning for RS485 devices...");
        for (byte address = 1; address <= 247; address++)
        {
            try
            {
                ushort[] registers = master.ReadHoldingRegisters(address, 0, 1);
                Console.WriteLine($"Device found at Address: {address}");
            }
            catch
            {
                // No response, ignore
            }
        }
    }

    // 2. Assign Device ID (Software Configuration)
    public void AssignDeviceID(byte oldAddress, byte newAddress)
    {
        try
        {
            master.WriteSingleRegister(oldAddress, 0, newAddress);
            Console.WriteLine($"Device {oldAddress} ID changed to {newAddress}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to change device ID: {ex.Message}");
        }
    }

    // 3. Read Data from a Particular Device
    public void ReadDataFromDevice(byte deviceID)
    {
        try
        {
            ushort[] registers = master.ReadHoldingRegisters(deviceID, 0, 2);
            Console.WriteLine($"Device {deviceID} Data: {string.Join(", ", registers)}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error reading from Device {deviceID}: {ex.Message}");
        }
    }

    // 4. Send Command to a Particular Device
    public void SendCommandToDevice(byte deviceID, ushort command)
    {
        try
        {
            master.WriteSingleRegister(deviceID, 1, command);
            Console.WriteLine($"Command {command} sent to Device {deviceID}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error sending command to Device {deviceID}: {ex.Message}");
        }
    }

    // 5. Read Data from All Devices
    public void ReadAllDevices(byte[] deviceAddresses)
    {
        foreach (byte address in deviceAddresses)
        {
            ReadDataFromDevice(address);
        }
    }

    // 6. Send Data to All Devices
    public void SendDataToAllDevices(byte[] deviceAddresses, ushort command)
    {
        foreach (byte address in deviceAddresses)
        {
            SendCommandToDevice(address, command);
        }
    }
}

class Program
{
    static void Main()
    {
        RS485Manager rs485 = new RS485Manager();

        // 1. Scan for Devices
        rs485.ScanDevices();

        // 2. Assign a new device ID (Example: Change device ID 1 to 10)
        rs485.AssignDeviceID(1, 10);

        // 3. Read data from a specific device (Example: Read from ID 10)
        rs485.ReadDataFromDevice(10);

        // 4. Send command to a specific device (Example: Send command 50 to ID 10)
        rs485.SendCommandToDevice(10, 50);

        // 5. Read data from all devices
        byte[] deviceList = { 10, 2, 3 }; // Example list of device addresses
        rs485.ReadAllDevices(deviceList);

        // 6. Send command to all devices (Example: Send command 75 to all devices)
        rs485.SendDataToAllDevices(deviceList, 75);

        Console.WriteLine("\nProcess Complete!");
        Console.ReadKey();
    }
}

```
💡 Explanation of the Code:
✅ Auto-reconnect feature: If the connection to the RS485-to-Ethernet converter fails, it retries every 5 seconds.
✅ Scanning all devices: Loops through all possible addresses (1-247) to find active RS485 devices.
✅ Assigning new device IDs: Changes a device’s ID from oldAddress to newAddress using Modbus register.
✅ Reading data from a single device: Reads holding registers of a specific device.
✅ Sending commands to a specific device: Writes a single register (for example, turning ON/OFF a relay).
✅ Reading data from all devices: Iterates through a list of device addresses and reads data.
✅ Sending data to all devices: Sends the same command to multiple devices.

🚀 How to Use the Program
Modify the IP Address (converterIP = "192.168.1.100") to match your RS485-to-Ethernet converter.
Run the program → It will automatically scan all RS485 devices.
Assign device IDs as needed.
Send & receive data from any specific device or all devices.
</details>  
   </details>  
</details>  

## Components
<details>
<summary>Click to expand!</summary>
   
### PHOTOCOUPLER/OCTOCOUPLER : Isolation
   
| Name | Pins | Input Pins | Output pins | Oprating Volts | Amps| ANODE/CATHODE/EMITTER/COLLECTOR/GATE |
| :--- | :---:|  :---:     |  :---:      |  :---:         | :---: |          :---:                      |
| TLP281 | 4  |   2        |     2       | 5 V-dc AN-CA   | 300 mah| 5-9 v-dc / EM-CL |
| TLP281-4 | 16 | 8 | 8 | 5V-dc AN-CA |  300 mah | 5-9 v-dc / EM-CL   |
   
### Driver IC: Motor Driver/ Realy Driver : 

| Name | Pins | Input Pins | Output pins | Oprating Volts | Amps| ANODE/CATHODE/EMITTER/COLLECTOR/GATE |
| :--- | :---:|  :---:     |  :---:      |  :---:         | :---: |          :---:                      |
| ULN2003 | 16  |   8       |     8       | 5 V-dc AN-CA   | 500 mah| 5-9 v-dc / EM-CL |
| ULN2803APG | 16  |   8       |     8       | 5 V-dc AN-CA   | 500 mah| 5-9 v-dc / EM-CL |

### I2C IC | Communcation IC/ IO expender 
| Name | Pins | Input Pins | Output pins | Oprating Volts | 
| :--- | :---:|  :---:     |  :---:      |  :---:         |
| PCF8574 | 16  |   8       |    4      | 5 V-dc AN-CA   |
   
   
   
</details>
   
   
## Projects
<details>
<summary>Click to expand!</summary>
  
### 1. IoT projects
   - Smart Agriculture System
   - Home Automation System.
   - Smart Garage Door 
   - Air Pollution Monitoring System
   - Smart Parking System
   - Smart Gas Leakage Detector Bot
   - Streetlight Monitoring System
   - Liquid Level Monitoring System
   - Smart Irrigation System
   - Mining Worker Safety Helmet
   - Covid face mask detection

### 2. Embedded Programming
   - Plc programming
   - HMI programming
   - Custom microcontroller circuits
   - VFD 
   - Encoders
   - wireless connectivity
   - I/O cards

### 3. Semiconductor
   - Single Phase Converter & Inverter
   - Three Phase Converter & Inverter
   - Solar Controller
   - DC controllers
   - Chargers

</details>
   
