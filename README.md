# automobil
elektron
import obd

# Initialize connection to the OBD-II adapter (COM4 port for Windows, /dev/ttyUSB0 for Linux)
connection = obd.OBD(portstr="COM4")

# Get and print a list of all supported commands
commands = connection.supported_commands
print("Supported OBD-II commands:")
for cmd in commands:
    print(cmd.name)

# Get and print data for a specific command (e.g., vehicle speed)
speed_command = obd.commands.SPEED
response = connection.query(speed_command)
if response.is_null():
    print(f"Unable to get speed data. Response: {response}")
else:
    print(f"Vehicle Speed: {response.value} {response.unit}")

# Close the connection
connection.close()
