# synchronous-buck-boost-converter

# Design

This high efficiency DC-DC converter is centered around the [TPS552892-Q1](https://www.ti.com/lit/ds/symlink/tps552892-q1.pdf) automotive grade synchronous programmable IC. It provides up to 5A output at >=95% efficiency and is automotive qualified.

### EN/UVLO

This pin acts as programmable UVLO input with 1.23-V internal reference.

Below 1.15V the device is in shutdown mode. Using a basic voltage divider circuit, we can use this to set the voltage cutoff for critical battery levels.

For example, for an 8V cutoff we must choose R1 with $ \left(\frac{8}{1.15}-1\right)\approx6$ times greater value than R2.

The preliminary design was made with $ R_{\text{ent}} = 560\ \text{k}\Omega,\ R_{\text{enb}} = 100\ \text{k}\Omega$ for a $ 7.6\ \text{V}$ cutoff. This may be replaced with a potentiometer for user controllable cutoff in future designs.

### FB

Output voltage is configured with a voltage divider network. TI recommends $ R_{\text{FB\_UP}} = 100 \, \text{k}\Omega$. The reference voltage $ V_{\text{REF}} = 1.2 \, \text{V}$.

$\frac{R_{\text{FB\_DOWN}}}{(100\, \text{k}\Omega + R_{\text{FB\_DOWN}})} \cdot V_{\text{out}} = 1.2, \quad R_{\text{FB\_DOWN}} = 11\, \text{k}\Omega \text{ at } 12\, \text{V}.$

This may be replaced with a potentiometer for variable output in future designs.

### PG & CC

- PG: Open-drain; high ≥95%, low <90%
- CC: Open-drain; outputs low when current-limiting

The primary design ties these to $ 100\, \text{k}\Omega$ resistors. These may be replaced with warning LEDs for debug.

### ISP & ISN

Current sense positive and negative across $ R_{\text{sns}}$. $ V_{\text{isp}} \geq 50\, \text{mV} + V_{\text{isn}}$. $ R_{\text{sns}} = \frac{V_{\text{sns}}}{I_{\text{OUT\_LIMIT}}}$ where $ R_{\text{sns}}$ is a resistor in line with $ V_{\text{out}}$.

For a current limit of 5A, $ R_{\text{sns}} = 0.01\, \Omega$. This results in a power draw up to $ 0.25\, \text{W}$, determined to be not worth the efficiency loss, as this IC has built in over-temperature and short-circuit protection. As such, it is disabled by connection in the preliminary design.