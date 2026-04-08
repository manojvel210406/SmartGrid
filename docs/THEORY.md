# Power System Theory Reference

## Load Flow Analysis

### Bus Types
- **Slack Bus**: V and θ are known (reference). P and Q are calculated.
- **PV Bus**: P and |V| are specified. Q and θ are calculated.
- **PQ Bus**: P and Q are specified. V and θ are calculated.

### Newton-Raphson Method

The power flow equations in polar form:

```
P_i = Σ_j |V_i||V_j|(G_ij cos θ_ij + B_ij sin θ_ij)
Q_i = Σ_j |V_i||V_j|(G_ij sin θ_ij - B_ij cos θ_ij)
```

Mismatch equations:
```
ΔP_i = P_i^sch - P_i^calc
ΔQ_i = Q_i^sch - Q_i^calc
```

Jacobian matrix:
```
[ΔP]   [H  N] [Δθ  ]
[ΔQ] = [J  L] [ΔV/V]
```

## Fault Analysis

### Types of Faults
1. **3-Phase Balanced Fault** (most severe, least common)
2. **Single Line-to-Ground** (most common, ~70% of faults)
3. **Line-to-Line Fault**
4. **Double Line-to-Ground Fault**

### Z-Bus Method
```
Z_bus = Y_bus^(-1)

I_f = V_f / (Z_ff + Z_f)
```

Where:
- V_f = prefault voltage at fault bus
- Z_ff = driving point impedance
- Z_f = fault impedance

### Voltage at Other Buses During Fault
```
V_i^fault = V_i^0 - Z_if * I_f
```

## Transient Stability

### Swing Equation
```
2H/ω_s * d²δ/dt² = P_m - P_e - D * dδ/dt
```

Where:
- H = inertia constant (MWs/MVA)
- ω_s = synchronous angular frequency
- δ = rotor angle
- P_m = mechanical power input
- P_e = electrical power output
- D = damping coefficient

### Equal Area Criterion
System remains stable if accelerating area < decelerating area on P-δ curve.

## Economic Dispatch

### Optimization Problem
```
min Σ C_i(P_i)
s.t. Σ P_i = P_D (power balance)
     P_i^min ≤ P_i ≤ P_i^max
```

### Lambda Iteration
At optimal dispatch:
```
dC_i/dP_i = λ  for all online generators
```

Quadratic cost function:
```
C_i(P_i) = a_i*P_i² + b_i*P_i + c_i
dC_i/dP_i = 2*a_i*P_i + b_i = λ
P_i^opt = (λ - b_i) / (2*a_i)
```

## Per-Unit System

Conversions:
```
Z_pu = Z_actual / Z_base
Z_base = V_base² / S_base
I_base = S_base / (√3 * V_base)
```

Standard base values:
- S_base = 100 MVA
- V_base = rated voltage at each level
