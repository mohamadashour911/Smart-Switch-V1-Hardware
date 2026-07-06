# Smart Switch V1 (Hardware & Firmware)

This repository contains the full hardware design and core firmware for **Smart Switch V1**, developed as a key component of a decentralized, wireless Smart Home System.

<!-- 📸 مكان صورة الـ 3D الخاصة بالبوردة -->
<!-- امسح السطر الذي بالأسفل وضع مكانها صورة الـ 3D View للوحة بسحبها وإفلاتها هنا -->
![Smart Switch 3D PCB Render View](<img width="711" height="628" alt="Board_3D" src="https://github.com/user-attachments/assets/61820db3-135d-4676-829d-20406ce36751" />
)

## 🚀 Features
* **Wireless Load Control:** Direct, peer-to-peer control over electrical appliances such as lamps and small motors.
* **Local Mesh Communication:** Employs low-latency wireless communication between nodes without relying on an external Wi-Fi router[cite: 1].
* **Safe Power Switching:** Built-in hardware protection for handling high AC voltages safely[cite: 1].

---

## 🔌 Detailed Hardware & Circuit Architecture

The hardware design focuses on electrical safety, galvanic isolation, and robust AC load switching[cite: 1]. Below is a detailed breakdown of the schematic stages implemented on the board[cite: 1]:

<!-- 📸 مكان صورة الـ Schematic -->
<!-- امسح السطر الذي بالأسفل وضع مكانها صورة الـ Schematic بسحبها وإفلاتها هنا -->
![Smart Switch Circuit Schematic](  <img width="1117" height="702" alt="image" src="https://github.com/user-attachments/assets/15be3cb5-404f-4520-85b8-21d403a4a80f" />
    )

### 1. Isolated Power Supply Stage
* **AC-DC Conversion:** Utilizes an isolated **HLK-PM** power module to step down 220V AC to a safe low-voltage DC rail to power the ESP32 and peripheral logic[cite: 1].
* **Overvoltage & Surge Protection:** Features an onboard **Metal Oxide Varistor (MOV 471)** across the AC input lines to suppress transient voltage spikes, backed by a dedicated **Live Fuse** in a secure fuse holder for overcurrent safety[cite: 1].
* **Visual Diagnostics:** Includes a green LED power indicator to verify stable DC output[cite: 1].

### 2. Control Core (MCU)
* **Brain:** Powered by an **Sub-system ESP32** module managing wireless peer-to-peer data layout via ESP-NOW[cite: 1].
* **Peripherals Interfacing:** Integrated with standard hardware reset/boot circuitry and a dedicated programming pin-header for flashing firmware[cite: 1].

### 3. Galvanic Isolation & Zero-Cross Triac Driving
To completely isolate the high-voltage AC side from the low-voltage DC micro-controller circuit, a 3-channel optical isolation barrier is used[cite: 1]:
* **Optocoupler:** **MOC3041M** Zero-Cross Phototriac Drivers[cite: 1]. The integrated zero-cross circuit ensures that switching only occurs when the AC voltage waveform crosses 0V, heavily reducing Electromagnetic Interference (EMI) and current inrush stress[cite: 1].
* **Current Limiting:** 330-Ohm resistors protect the internal optocoupler LEDs from the ESP32 GPIO drive current[cite: 1].

### 4. Heavy-Duty Power Switching & Snubber Protection
* **Main Switch:** **BTA26-600B Triacs** control each independent load channel[cite: 1]. Rated at 600V and up to 25A/26A, providing an immense safety margin for domestic appliances, lighting banks, and small inductive motors[cite: 1].
* **RC Snubber Network:** Each Triac channel is protected by a series RC network consisting of a **270-Ohm Metal Oxide Resistor** and a **10nF High-Voltage Capacitor** across the main terminals (MT1-MT2)[cite: 1]. This network absorbs high dV/dt voltage spikes generated during the switching of inductive loads, eliminating false Triac triggering[cite: 1].

### 5. Input & Output Interfacing
* **Hardware-Debounced Inputs:** Includes a pin header for external mechanical switches (SW_1, SW_2, SW_3)[cite: 1]. Each line is equipped with a **100nF decoupling capacitor** to achieve robust hardware-level switch debouncing, stabilizing the inputs before they reach the MCU[cite: 1].
* **Outputs Terminal:** High-quality 3-position terminal block for solid, low-resistance connections to the external electrical loads[cite: 1].

---

## 🛠️ Repository Structure
* 📂 **Hardware/**: Altium Designer schematics and PCB layout project files[cite: 1].
* 📂 **Firmware/**: Core control logic and local wireless setup written in C++ using the Arduino IDE[cite: 1].
* 📂 **Outputs/**: Production-ready Gerber files, schematic PDF, and high-quality 2D/3D PCB layout render screenshots[cite: 1].

## 📡 Protocols Used
* **ESP-NOW:** For ultra-fast, direct peer-to-peer wireless communication between the switch nodes and the gateway[cite: 1].
