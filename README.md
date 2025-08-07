
# Robotic Arm Torque Calculation and Servo Motor Selection

---

## 1. Torque Calculation Method for Each Joint Motor

### 1.1 Understanding Loads on Joints

The robotic arm consists of multiple joints.  
Each joint must compensate for:

- The payload weight it carries  
- The weight of arm segments located beyond that joint (external parts)

### 1.2 Basic Parameters

- Payload weight `m_payload` (kg)  
- Weights of arm segments `m1, m2, ..., mn` (kg)  
- Length of each arm segment `L1, L2, ..., Ln` (meters)  
- Gravitational acceleration `g = 9.81 m/s²`

### 1.3 General Torque Formula at Joint *i*

```
τᵢ = g × Σ (from j = i to n) [ mⱼ × dᵢⱼ ]
```

Where:  
- `τᵢ` is the required torque at joint `i` (N·m)  
- `mⱼ` is the mass of segment `j` or payload if `j = n`  
- `dᵢⱼ` is the vertical distance from joint `i` to the center of mass of segment `j` (in meters)

---

### 1.4 Practical Example (3-Joint Arm)

| Joint       | Mass `mⱼ` (kg) | Segment Length `Lⱼ` (m) | Center of Mass Approx. `dᵢⱼ` (m) |
|-------------|----------------|--------------------------|-----------------------------------|
| Joint 3     | 1 (Payload)     | -                        | 0                                 |
| Joint 2     | 0.5            | 0.2                      | 0.1                               |
| Joint 1     | 0.7            | 0.3                      | 0.15                              |

- **Torque at Joint 3:**

```
τ₃ = 9.81 × 1 × 0 = 0 N·m
```

- **Torque at Joint 2:**

```
τ₂ = 9.81 × (1 × 0.1) = 0.981 N·m
```

- **Torque at Joint 1:**

```
τ₁ = 9.81 × [ (0.7 × 0.15) + (0.5 × (0.3 + 0.1)) + (1 × (0.3 + 0.2 + 0.1)) ]
    = 9.81 × [ 0.105 + 0.2 + 0.6 ]
    = 9.81 × 0.905 = 8.88 N·m
```

---

### 1.5 Safety Margin

It is recommended to choose motors with **20–30% higher torque** than the calculated value.

---

## 2. Choosing Suitable Servo Motors

| Motor                   | Torque (N·m) | Purchase Link                                           |
|-------------------------|--------------|----------------------------------------------------------|
| Dynamixel MX-64         | 6.0          | [Link](https://www.robotis.us/dynamixel-mx-64/)          |
| MG995 High Torque Servo | 1.8          | [Link](https://www.amazon.com/dp/B00DJYH7L6)             |
| Hitec HS-805BB          | 2.2          | [Link](https://www.amazon.com/dp/B0038WL9EO)             |

Make sure to select the motor according to the **required torque per joint** with the **safety margin** in mind.

---

## 3. Increasing Payload to 2 kg Using Gears

You can increase torque by using gear reduction:

- A **2:1 gear ratio** doubles the torque but halves the speed.
- Example:  
  If a motor produces 3 N·m, with a 2:1 gear ratio → 6 N·m output torque.

---

## 4. Disadvantages of Gear Systems

- Slower movement  
- Larger physical size  
- More friction and energy loss  
- Increased complexity in design and maintenance

---

## 5. Alternatives to Gear Systems

- Use **higher torque motors** directly  
- Choose **lighter materials** for robot arms  
- Optimize **mechanical design** and center of mass  
- Use **hydraulic or pneumatic** systems for heavy loads  
- Implement **smart control strategies** (e.g., motion planning)

---

## 6. References

- [Dynamixel Robot Manual](https://emanual.robotis.com/docs/en/dxl/)  
- Robotics Torque Calculation Guides  
- Gear System Principles
