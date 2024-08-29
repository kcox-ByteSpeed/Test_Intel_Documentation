# Power Supply Unit (PSU) Troubleshooting Guide
> This guide provides information to help diagnose and troubleshoot issues related to the Power Supply Unit (PSU) in a server system. The PSU's status can be identified using the LED indicators and the built-in protection circuits that help prevent damage to the system.

## Power Supply Status LED Indicators
> The PSU status LED provides a quick visual indication of the PSU's operating state and any potential faults:
- **No LED (Off):** Indicates no source power is available to the PSU. Check the power cord connection, power source, and circuit breakers.
- **Solid Green:** The PSU is operating normally, and output is on and within the expected range.
- **Blinking Green (1 Hz):** The PSU is receiving AC power, but the main output is off. This could indicate the PSU is in a cold redundant state, or the system is in standby mode. Verify if the system is powered on and functioning as expected.
- **Solid Amber:** Indicates a critical condition where the PSU has shut down due to an internal fault such as overcurrent protection (OCP), overvoltage protection (OVP), or a fan failure. Ensure proper ventilation, check for obstructions, and verify all fans are operational.
- **Blinking Amber (1 Hz):** A warning state where the PSU continues to operate but has detected a condition like high temperature, high power usage, or a fan running slower than expected. Check the system’s cooling, airflow, and load to prevent further escalation.


## Protection Circuits
> The PSU contains several protection circuits designed to safeguard against abnormal operating conditions. These circuits include Overcurrent Protection (OCP), Over-Voltage Protection (OVP), and Over-Temperature Protection (OTP).

### Overcurrent Protection (OCP)
> OCP prevents the PSU from delivering more current than it is designed to handle. If the output exceeds the specified limits, the PSU will shut down to protect itself and the server components.
- **Diagnosis:** If the PSU shuts down and the system's event logs indicate an overcurrent event, it is likely that the system's power demand is exceeding the PSU's capacity. Reduce the load or redistribute it across multiple PSUs if possible.
- **Solution:** To reset, remove the cause of the overload and cycle the AC power off for at least 15 seconds. Ensure the server configuration does not exceed the PSU's maximum current rating.

### Over-Voltage Protection (OVP)
> OVP activates when the voltage on any output exceeds its preset limit, which could cause damage to the server hardware.
- **Diagnosis:** If a power shutdown is accompanied by event log entries about an over-voltage condition, check the power supply outputs with a voltmeter if possible.
- **Solution:** Replace the PSU if it repeatedly triggers OVP. Before resetting, power down the system and unplug the PSU for a few seconds. This step will reset the OVP latch, allowing the PSU to start again.

### Over-Temperature Protection (OTP)
> OTP is triggered when the PSU detects temperatures beyond safe operating limits, which can occur due to inadequate ventilation, failed fans, or excessive ambient temperatures.
- **Diagnosis:** The system event logs might show thermal events, and the PSU LED may blink amber or turn solid amber if it shuts down. Check for blocked vents, non-functioning fans, or a high ambient temperature around the server.
- **Solution:** Improve airflow around the PSU by ensuring all fans are operational and vents are unobstructed. Allow the PSU to cool down before restarting. Reduce ambient temperatures or move the server to a cooler environment if necessary.

## General Troubleshooting Steps
1. **Check Power Connections:** Ensure that all power cables are securely connected and that the PSU is properly seated in its bay.
2. **Inspect LEDs:** Use the PSU status LED to determine the immediate condition of the PSU. Refer to the LED states above for guidance.
3. **Review System Logs:** Access the server's event log to identify any PSU-related warnings or errors that might indicate an overcurrent, over-voltage, or over-temperature event.
4. **Verify Environmental Conditions:** Ensure that the server operates within its specified temperature range and that all cooling systems are functioning properly.
5. **Replace Faulty Components:** If a PSU repeatedly fails or indicates a fault, replace it to prevent potential damage to the server and other components.
6. **Monitor for Recurrence:** After taking corrective actions, monitor the PSU status and server operation for any recurrence of issues.

> By following these steps, most PSU-related issues in server systems can be quickly identified and resolved, ensuring minimal downtime and maintaining optimal server performance.