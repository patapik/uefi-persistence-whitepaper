# Firmware Persistence Attack Chain

```mermaid
flowchart TB
    subgraph Phase1["🔴 PHASE 1: Initial Access"]
        direction TB
        A1["OS-level compromise<br/>(user / ring-0 access)"]
        A2["Physical access<br/>(SPI programmer)"]
        A3["Supply chain compromise<br/>(pre-implanted firmware)"]
    end
    
    subgraph Phase2["🟠 PHASE 2: Firmware Modification"]
        direction TB
        B1["SPI flash write<br/>(malicious DXE driver)"]
        B2["WPBT ACPI table injection"]
        B3["NVRAM variable modification"]
        B4["ESP bootloader replacement"]
    end
    
    subgraph Phase3["🟡 PHASE 3: Persistence Installation"]
        direction TB
        C1["Malicious DXE driver<br/>loaded at every boot"]
        C2["WPBT binary executed<br/>at OS startup (kernel level)"]
        C3["Bootkit persists across<br/>disk replacement & OS reinstall"]
    end
    
    subgraph Phase4["🔴 PHASE 4: Execution & C2"]
        direction TB
        D1["Kernel-level payload (Ring 0)"]
        D2["C2 communication"]
        D3["Lateral movement"]
    end
    
    A1 --> B1
    A1 --> B2
    A1 --> B3
    A2 --> B1
    A3 --> B1
    
    B1 --> C1
    B2 --> C2
    B3 --> C1
    B4 --> C1
    
    C1 --> D1
    C2 --> D1
    D1 --> D2
    D2 --> D3
    
    style Phase1 fill:#ffcccc,stroke:#cc0000,stroke-width:2px
    style Phase2 fill:#ffcc99,stroke:#cc6600,stroke-width:2px
    style Phase3 fill:#ffffcc,stroke:#cccc00,stroke-width:2px
    style Phase4 fill:#ffcccc,stroke:#cc0000,stroke-width:2px
    style B1 fill:#ff9999,stroke:#990000,stroke-width:2px
    style B2 fill:#ff9999,stroke:#990000,stroke-width:2px
    style C1 fill:#ffcc99,stroke:#cc6600,stroke-width:2px
    style D1 fill:#ff9999,stroke:#990000,stroke-width:2px
