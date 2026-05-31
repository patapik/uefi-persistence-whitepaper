# Firmware Persistence Attack Chain

```mermaid
flowchart TB
    subgraph Phase1["PHASE 1: Initial Access"]
        A1["OS-level compromise (user/ring-0 access)"]
        A2["Physical access (SPI programmer)"]
        A3["Supply chain compromise (pre-implanted firmware)"]
    end
    
    subgraph Phase2["PHASE 2: Firmware Modification"]
        B1["NVRAM variable modification"]
        B2["WPBT ACPI table injection"]
        B3["SPI flash write (malicious DXE driver)"]
        B4["ESP bootloader replacement"]
    end
    
    subgraph Phase3["PHASE 3: Persistence Installation"]
        C1["Bootkit persists across disk replacement & OS reinstall"]
    end
    
    subgraph Phase4["PHASE 4: Execution & C2"]
        D1["Kernel-level payload (Ring 0)"]
        D2["C2 communication"]
        D3["Lateral movement"]
    end
    
    A1 --> B1
    A1 --> B2
    A1 --> B3
    A2 --> B3
    A3 --> B3
    
    B1 --> C1
    B2 --> C1
    B3 --> C1
    B4 --> C1
    
    C1 --> D1
    D1 --> D2
    D2 --> D3
