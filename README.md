# synchronous-buck-boost-converter

# Design

This high efficiency DC-DC converter is centered around the [TPS552892-Q1](https://www.ti.com/lit/ds/symlink/tps552892-q1.pd) automotive grade synchronous programmable IC. It provides up to 5A output at >=95% efficiency and is automotive qualified.

### EN/UVLO

This pin acts as programmable UVLO input with 1.23-V internal reference.

Below 1.15V the device is in shutdown mode. Using a basic voltage divider circuit, we can use this to set the voltage cutoff for critical battery levels.

For example, for an 8‑V cutoff we must choose R1 with $\left(\frac{8}{1.15}-1\right)\approx6$ times greater value than R2.

The preliminary design was made with $R_{\text{ent}} = 560\ \text{k}\Omega,\ R_{\text{enb}} = 100\ \text{k}\Omega$ for a $7.6\ \text{V}$ cutoff. This may be replaced with a potentiometer for user controllable cutoff in future designs.

### PG & CC

- PG: Open-drain; high ≥95%, low <90%
- CC: Open-drain; outputs low when current-limiting

The primary design ties these to $100\ \text{k}\Omega$ resistors. These may be replaced with warning LEDs for debug.

### ISP & ISN

Current sense positive and negative. Disabled by connection in the preliminary design.