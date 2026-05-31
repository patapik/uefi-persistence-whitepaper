# SPI Flash Layout – UEFI Firmware Storage

```mermaid
flowchart TD
    subgraph "SPI Flash Memory (32MB typical)"
        direction TB
        A["Descriptor Region<br/>Flash layout, master access"]
        B["Intel ME / AMD PSP<br/>Management Engine firmware"]
        C["GbE Firmware<br/>Gigabit Ethernet controller"]
        D["UEFI BIOS Region<br/>SEC, PEI, DXE, BDS, NV data"]
        E["NVRAM Variables<br/>BootOrder, Secure Boot keys, etc."]
        F["Padding / Unused<br/>Reserved space"]
        
        A --> B --> C --> D --> E --> F
    end
    
    subgraph "Attack Vectors"
        A1["SPI flash reprogramming<br/>(requires physical or ring-0 access)"]
        A2["ME/PSP compromise<br/>(persistence below UEFI)"]
        A3["DXE driver injection<br/>(MoonBounce, LoJax)"]
        A4["NVRAM variable abuse<br/>(persistence via SetVariable)"]
    end
    
    A -.-> A1
    B -.-> A2
    D -.-> A3
    E -.-> A4
