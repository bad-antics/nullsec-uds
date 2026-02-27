# NullSec UDS

<p align="center">
  <img src="https://img.shields.io/badge/Protocol-UDS-blue?style=for-the-badge" alt="UDS"/>
  <img src="https://img.shields.io/badge/ISO-14229-orange?style=for-the-badge" alt="ISO 14229"/>
  <img src="https://img.shields.io/badge/CAN--FD-Supported-green?style=for-the-badge" alt="CAN-FD"/>
</p>

Unified Diagnostic Services (ISO 14229) security research and testing toolkit.

## 🔧 Features

- **Full UDS Implementation**: All standard diagnostic services
- **Security Access Bypass**: Multiple bypass techniques
- **Seed-Key Algorithms**: Reverse engineering support
- **Flash Programming**: Read/write ECU memory
- **Routine Control**: Execute diagnostic routines
- **Session Management**: Automated session handling

## 🔐 UDS Services

### Diagnostic Session Control (0x10)
```bash
uds-cli --session default        # 0x01
uds-cli --session programming    # 0x02
uds-cli --session extended       # 0x03
```

### Security Access (0x27)
```bash
# Request seed
uds-cli --security-seed --level 1

# Brute force key
uds-cli --bruteforce --level 1 --threads 4

# Use known algorithm
uds-cli --calc-key --algo vw_sa2 --seed 0xDEADBEEF
```

### Read/Write Memory (0x23/0x3D)
```bash
# Dump ECU memory
uds-cli --read-memory 0x00080000 --size 0x10000 -o dump.bin

# Write calibration
uds-cli --write-memory 0x00080000 -i calibration.bin
```

### Download/Upload (0x34/0x35/0x36/0x37)
```bash
# Extract firmware
uds-cli --upload --address 0x00000000 --size 0x200000

# Flash new firmware
uds-cli --download -i firmware.bin --address 0x00000000
```

## 🔓 Security Research

### Seed-Key Analysis
- Algorithm identification
- Timing attacks
- Replay protection bypass
- Key generation reverse engineering

### Common Bypasses
```bash
# Timing attack
uds-cli --timing-attack --service 0x27

# Session confusion
uds-cli --session-attack

# Diagnostic ID spoofing
uds-cli --spoof-tester-id 0xF1
```

## 📡 Protocol Support

| Transport | Standard | Speed |
|-----------|----------|-------|
| CAN 2.0A | ISO 15765-2 | 500 kbps |
| CAN 2.0B | ISO 15765-2 | 500 kbps |
| CAN-FD | ISO 15765-2 | 2/5 Mbps |
| DoIP | ISO 13400 | Ethernet |
| K-Line | ISO 14230 | 10.4 kbps |

## 🔌 Hardware

- SocketCAN (Linux native)
- J2534 passthru devices
- CANtact / CANable
- Vector CANalyzer
- PEAK PCAN-USB

## ⚠️ Disclaimer

For authorized security research only. Modifying vehicle ECUs may void warranties and violate regulations.

## 📜 License

MIT License - Part of NullSec Linux v5.0

**Discord**: [x.com/AnonAntics](https://x.com/AnonAntics)
