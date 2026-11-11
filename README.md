# TFTP Router Assistant

A Windows assistant for preparing router firmware recovery over TFTP. It provides a guided setup, Ukrainian, English, and Russian interface, `.bin` firmware selection, network adapter selection, and a customizable TFTP filename.

The application uses the Tftpd64 4.74 server to transfer files. It does not install firmware automatically: you must put your router into its manufacturer-specific recovery mode.

> **Status: early release.** The application has been compiled and launched, but has not yet been tested with a physical router.

## Features

- First-run guide with step-by-step instructions
- Interface in Ukrainian, English, and Russian
- Firmware file picker restricted to `.bin`
- Custom TFTP filename for routers that expect a specific name
- Network adapter selection and display of the computer’s IPv4 address
- TFTP server control through the included Tftpd64 4.74
- Temporary TFTP folder containing only the selected firmware file
- Activity log display

## Requirements

- Windows
- .NET Framework desktop runtime
- The complete portable package, including its `Tftpd64` folder

TFTP uses UDP port 69. Windows Firewall may ask whether to allow Tftpd64 to communicate. Allow access on the private network used for the direct router connection.

## How to use

1. Connect the computer to the router with an Ethernet cable.
2. Run `TftpRouterAssistant.exe`.
3. On first launch, follow the setup guide.
4. Choose a `.bin` firmware file made for the exact router model and hardware revision.
5. Select the Ethernet adapter connected to the router.
6. If your router requires a specific TFTP filename, enter it in the filename field. It must end in `.bin`.
7. Click **Start TFTP server**.
8. Follow the manufacturer’s instructions to put the router into recovery mode.
9. If requested by the router, provide the displayed computer IP address and TFTP filename.
10. Wait for the router to finish writing the firmware. Do not disconnect its power during this process.

Some routers request the firmware file automatically in recovery mode. Others require you to enter the server IP address and filename in a bootloader or recovery screen. Consult the instructions for your exact router model.

## Important

This assistant does not:

- Put the router into recovery mode
- Determine which firmware is compatible with your router
- Verify the contents of a firmware file
- Confirm that the router completed flashing successfully

Using firmware for a different model or hardware revision can damage the device. Follow the router manufacturer’s instructions and do not disconnect power while firmware is being written.

## File handling

While the TFTP server is running, the assistant copies the selected firmware into a temporary folder under:

```text
%APPDATA%\TftpRouterAssistant\transfer-sessions
