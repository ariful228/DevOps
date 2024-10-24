# Computer Basic Workflow

**Power On**
>[!TIP]
> **Power Supply**: Sends electricity to components. <br>
> **ROM**: BIOS/UEFI provides startup instructions. <br>

**BIOS/UEFI Initialization**
>[!TIP] 
> **POST**: Checks critical components. <br>
> **Bootloader**: Loads the Operating System (OS) into RAM. <br>

**OS Loading**
>[!TIP] 
> Loads OS from disk (HDD/SSD) into RAM. <br>
> Initializes the kernel, managing system resources. <br>

**CPU Fetch-Decode-Execute Cycle**
>[!TIP] 
> **Fetch**: Retrieves instructions from RAM. <br>
> **Decode**: Understands actions to take. <br>
> **Execute**: Performs actions, like calculations and memory access. <br>

**Data Transfer via Buses**
>[!TIP] 
> Data moves between CPU, RAM, disk, and devices using buses. <br>

**Running Applications**
>[!TIP] 
> Loads applications into RAM for faster access. <br>
> CPU executes application instructions. <br>

**Memory Management**
>[!TIP] 
> Manages RAM usage and may use virtual memory when RAM is full.

**Multitasking and Process Management**
>[!TIP] 
> Manages multiple applications using task scheduling and interrupts.

**Device Interaction**
>[!TIP] 
> Communicates with hardware using device drivers.

**Program Execution and Resource Management**
>[!TIP] 
> Manages resources (CPU, memory) and file access.

**Program Termination and Cleanup**
>[!TIP] 
> Frees up memory and resources when applications are closed.
- Uses garbage collection to clear unused memory.

**System Monitoring**
>[!TIP] 
> Continuously monitors system performance (CPU, memory, disk usage).

<br><br>

# Workflow of computer working process

```mermaid
flowchart TD
    A[Power On] --> B[BIOS/UEFI Initialization]
    B --> C[OS Loading]
    C --> D[CPU Fetch-Decode-Execute Cycle]
    D --> E[Data Transfer via Buses]
    E --> F[Running Applications]
    F --> G[Memory Management]
    G --> H[Multitasking and Process Management]
    H --> I[Device Interaction]
    I --> J[Program Execution and Resource Management]
    J --> K[Program Termination and Cleanup]
    K --> L[System Monitoring]
```
<br>

# Related
[Python](https://github.com/ariful228/DevOps/tree/main/DevOps/Python)