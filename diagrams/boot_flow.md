# UEFI Boot Flow – Attack Surface

```mermaid
flowchart TD
    SEC["SEC"] --> PEI["PEI"] --> DXE["DXE"] --> BDS["BDS"] --> TSL["TSL<br/>(OS Loader)"] --> RT["RT"]
    
    SEC -.-> A1["SPI flash modify"]
    DXE -.-> A2["Malicious DXE<br/>(MoonBounce)"]
    BDS -.-> A3["WPBT / Boot order"]
    TSL -.-> A4["Bootkit injection<br/>(BlackLotus)"]
