```markdown
# Firmware Persistence Attack Chain

```mermaid
flowchart LR
    subgraph "Phase 1: Initial Access"
        I1["OS-level compromise<br/>(user/ring-0)"]
        I2["Physical access<br/>(SPI programmer)"]
        I3["Supply chain<br/>(pre-implanted firmware)"]
    end
    
    subgraph "Phase 2: Firmware Modification"
        F1["SPI flash write<br/>(malicious DXE driver)"]
        F2["WPBT ACPI table injection"]
        F3["NVRAM variable modification"]
        F4["ESP bootloader replacement"]
    end
    
    subgraph "Phase 3: Persistence Installation"
        P1["Malicious DXE driver<br/>loaded at every boot"]
        P2["WPBT binary executed<br/>at OS startup"]
        P3["Bootkit persists<br/>across disk replacement"]
    end
    
    subgraph "Phase 4: Execution"
        E1["Kernel-level payload<br/>(Ring 0)"]
        E2["C2 communication"]
        E3["Lateral movement"]
    end
    
    I1 --> F1
    I1 --> F2
    I1 --> F3
    I2 --> F1
    I3 --> F1
    
    F1 --> P1
    F2 --> P2
    F3 --> P1
    F4 --> P1
    
    P1 --> E1
    P2 --> E1
    E1 --> E2
    E2 --> E3
    
    style F1 fill:#ffcccc,stroke:#cc0000
    style F2 fill:#ffcccc,stroke:#cc0000
    style P1 fill:#ff9999,stroke:#990000
    style E1 fill:#ff6666,stroke:#660000
