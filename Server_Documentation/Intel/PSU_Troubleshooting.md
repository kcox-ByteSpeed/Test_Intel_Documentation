# Power Supply Unit (PSU) Troubleshooting Guide
> This guide provides information to help diagnose and troubleshoot issues related to the Power Supply Unit (PSU) in a server system. The PSU's status can be identified using the LED indicators and the built-in protection circuits that help prevent damage to the system.

## General Troubleshooting Steps
1. **Check Power Connections:** Ensure that all power cables are securely connected and that the PSU is properly seated in its bay. Verify the PSU is connected to a reliable power source, such as a UPS or directly to a wall receptacle. Be cautious of using inexpensive UPS units, which may cause power issues.

2. **Inspect LEDs:** Use the PSU status LED to determine the immediate condition of the PSU. Refer to the LED states above for guidance.
3. **Review System Logs:** Access the server's event log to identify any PSU-related warnings or errors that might indicate an overcurrent, overvoltage, or over-temperature event.
4. **Verify Environmental Conditions:** Ensure that the server operates within its specified temperature range and that all cooling systems are functioning properly. Check that the server is located in an environment with adequate ventilation and cooling.

5. **Reseat the PSU:** Unplug the affected PSU, reseat it firmly in its bay, and check all connections. If issues persist, power off the server completely, unplug both PSUs, wait for at least 15 seconds, and then reseat both PSUs before powering the server back on.

6. **Check for Firmware Updates:** Outdated firmware can cause or fail to report degraded PSU states properly. Verify that the PSU and server firmware are up to date, and apply any necessary updates.

7. **Test with a Known Good PSU:** Swap the suspect PSU with a known good unit to determine if the issue is with the PSU itself or another component.
8. **Bypass the UPS:** If the server is connected to a UPS, temporarily plug the PSU directly into a wall receptacle to rule out [issues caused by the UPS][UPS_Recommendation]. 
9. **Replace Faulty Components:** If a PSU repeatedly fails or indicates a fault even after reseating and updates, replace it to prevent potential damage to the server and other components.

10. Monitor for Recurrence: After taking corrective actions, monitor the PSU status and server operation for any recurrence of issues.


## Power Supply Status LED Indicators
> The PSU status LED provides a quick visual indication of the PSU's operating state and any potential faults:

![](https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/blob/main/Images/PSU_Statis_Indicator_LED.png)

1. **No LED (Off):** Indicates no source power is available to the PSU. Check the power cord connection, power source, and circuit breakers.
2. **Solid Green:** The PSU is operating normally, and output is on and within the expected range.
3. **Blinking Green (1 Hz):** The PSU is receiving AC power, but the main output is off. This could indicate the PSU is in a cold redundant state, or the system is in standby mode. Verify if the system is powered on and functioning as expected.
4. **Solid Amber:** Indicates a critical condition where the PSU has shut down due to an internal fault due to a [protection circuit](#protection-circuits) or a fan failure. Ensure proper ventilation, check for obstructions, and verify all fans are operational.
5. **Blinking Amber (1 Hz):** A warning state where the PSU continues to operate but has detected a condition like high temperature, high power usage, or a fan running slower than expected. Check the system’s cooling, airflow, and load to prevent further escalation.


## Protection Circuits
The PSU contains several protection circuits designed to safeguard against abnormal operating conditions. These circuits include Overcurrent Protection (OCP), Over-Voltage Protection (OVP), and Over-Temperature Protection (OTP).

> Check the system log for power events on the PSU.

### Overcurrent Protection (OCP)
OCP prevents the PSU from delivering more current than it is designed to handle. If the output exceeds the specified limits, the PSU will shut down to protect itself and the server components.
- **Diagnosis:** If the PSU shuts down and the system's event logs indicate an overcurrent event, it is likely that the system's power demand is exceeding the PSU's capacity. Reduce the load or redistribute it across multiple PSUs if possible.
- **Solution:** To reset, remove the cause of the overload and cycle the AC power off for at least 15 seconds. Ensure the server configuration does not exceed the PSU's maximum current rating.

### Over-Voltage Protection (OVP)
OVP activates when the voltage on any output exceeds its preset limit, which could cause damage to the server hardware.
- **Diagnosis:** If a power shutdown is accompanied by event log entries about an over-voltage condition, check the power supply outputs with a voltmeter if possible.
- **Solution:** Replace the PSU if it repeatedly triggers OVP. Before resetting, power down the system and unplug the PSU for a few seconds. This step will reset the OVP latch, allowing the PSU to start again.

### Over-Temperature Protection (OTP)
OTP is triggered when the PSU detects temperatures beyond safe operating limits, which can occur due to inadequate ventilation, failed fans, or excessive ambient temperatures.
- **Diagnosis:** The system event logs might show thermal events, and the PSU LED may blink amber or turn solid amber if it shuts down. Check for blocked vents, non-functioning fans, or a high ambient temperature around the server.
- **Solution:** Improve airflow around the PSU by ensuring all fans are operational and vents are unobstructed. Allow the PSU to cool down before restarting. Reduce ambient temperatures or move the server to a cooler environment if necessary.

> Most PSU-related issues in server systems can be quickly identified and resolved, ensuring minimal downtime and maintaining optimal server performance.


## Sources
- [Troubleshooting PSU -- LED Status indicator][PSU_Status_Indicators]
- [Understanding UPS Types and Their Impact on High Performance PSUs][UPS_Recommendation]

[PSU_Status_Indicators]: https://www.intel.com/content/dam/support/us/en/documents/server-products/server-boards/m20ntp1ur-1u-tps.pdf
[UPS_Recommendation]: https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/wiki/Understanding-UPS-Types-and-Their-Impact-on-High%E2%80%90Performance-PSUs

## Revision History
| Revision | Date       | Comments                                                                 | Author     |
|----------|------------|--------------------------------------------------------------------------|------------|
| 1.0      | 08/28/2024 | Initial release | Keegan Cox |
| 1.1      | 08/29/2024 | Added media and revised | Keegan Cox |