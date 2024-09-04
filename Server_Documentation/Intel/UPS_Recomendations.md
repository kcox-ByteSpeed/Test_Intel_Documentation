# Understanding UPS Types and Their Impact on High Performance PSUs
> Newer, more sensitive PSUs (Power Supply Units) in servers can experience power issues when connected to certain types of UPS (Uninterruptible Power Supply) systems. The main types of UPS systems that can cause these issues include:

## Common UPS Types That Can Cause Issues
> Yes, they are cheeper, but they cause issues in Newer Server PSUs

1. Standby (Offline) UPS
    - **Description:** This is the most basic type of UPS. It provides power from its battery only when it detects a loss of utility power or a significant voltage drop.
    - **Potential Issues:**
        - **Switching Time:** There is a slight delay (typically 4-10 milliseconds) when switching from utility power to battery power. Sensitive PSUs might detect this as a power interruption.
        - **Modified Sine Wave Output:** Many standby UPS systems produce a modified sine wave (also called a simulated sine wave) when running on battery. Some newer PSUs require a pure sine wave for reliable operation and may not function correctly with the modified sine wave, causing potential power issues or failures.

2. Line-Interactive UPS
    - **Description:** This type of UPS provides more sophisticated power protection than standby models by regulating voltage fluctuations through an autotransformer. It switches to battery power during a complete power loss.
    - **Potential Issues:**
        - **Modified or Step-Wave Output on Battery:** Similar to standby UPSs, some line-interactive UPS systems also output a modified or step-wave sine wave when on battery power. Sensitive PSUs may have trouble with this kind of output, leading to power instability or noise.
        - **Switching Time:** Although typically faster than standby models, there is still a minor delay in switching to battery power, which could affect some sensitive PSUs.

3. Older or Low-Quality UPS Systems
    - **Description:** Older UPS models or low-quality, budget UPS systems often lack the advanced features and power quality controls of newer or more expensive models.
    - **Potential Issues:**
        - **Poor Voltage Regulation:** Inconsistent or poor voltage regulation can result in frequent power corrections or fluctuations that may be interpreted by the PSU as power instability.
        - **Low Battery Capacity or Degradation:** Batteries that are old or degraded may not provide adequate power under load, causing unexpected shutdowns or power dips.

4. UPS Systems with Inadequate Load Capacity
    - **Description:** A UPS with a load capacity (measured in VA or watts) that is too low for the equipment connected to it can cause problems.
    - **Potential Issues:**
        - **Overload Conditions:** If a UPS is overloaded, it may not be able to provide adequate power, especially during a power outage or surge, leading to shutdowns or errors in sensitive PSUs.

5. UPS with High Total Harmonic Distortion (THD)
    - **Description:** Total Harmonic Distortion (THD) is a measure of the distortion in the power signal. UPS systems that do not provide clean power (i.e., with high THD) can affect sensitive electronics.
    - **Potential Issues:**
        - **Signal Noise and Instability:** High THD can cause "dirty" power with signal noise that interferes with the PSU’s ability to convert AC to DC power efficiently, leading to potential errors or hardware issues.

## Recommendations for Using UPS with Sensitive PSUs:
- **Pure Sine Wave Output:** Choose a UPS that provides a pure sine wave output, especially when on battery. This type of power is closest to the power provided by utility companies and is better suited for sensitive electronics and newer PSUs.

- **Double-Conversion (Online) UPS:** For the best protection, use an online UPS, which constantly runs connected devices off its battery while simultaneously charging the battery from utility power. This provides an uninterrupted power supply with no switching time and maintains a consistent pure sine wave output, regardless of power fluctuations.

- **Adequate Capacity:** Ensure the UPS has adequate power capacity (in VA or watts) for the connected equipment, including any startup surges or peaks.

- **Regular Maintenance and Battery Replacement:** Perform regular maintenance checks and replace batteries as needed to ensure the UPS is functioning correctly.
By choosing the right type of UPS and ensuring it is well-maintained, you can minimize the risk of power issues with sensitive PSUs in modern server systems.