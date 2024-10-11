# Computer basic workflow

1. **Power On**  
   - **Power Supply**: The power supply sends electricity to all components.  
   - **ROM (Read-Only Memory)**: The BIOS/UEFI, stored in ROM, provides the instructions to start up the system.

2. **BIOS/UEFI Initialization**  
   - **POST (Power-On Self-Test)**: The BIOS checks if critical components like the CPU, RAM, and storage are working.  
   - **Bootloader**: After POST, the BIOS finds the bootloader, which is responsible for loading the Operating System (OS) into RAM.

3. **OS Loading**  
   - **Disk to RAM**: The Operating System (OS) is loaded from the disk (HDD/SSD) into RAM.  
   - **Kernel Initialization**: The kernel, which is the core part of the OS, is loaded first. The kernel manages system resources (CPU, memory, and devices).

4. **CPU Starts Fetch-Decode-Execute Cycle**  
   - **Fetching Instructions**: The CPU starts its main cycle (fetch-decode-execute):  
     - **Fetch**: The CPU retrieves instructions from RAM.  
     - **Decode**: It decodes the instructions to understand what action needs to be taken.  
     - **Execute**: The CPU executes the instructions, which might include calculations, memory access, or hardware communication.

5. **Data Transfer via Buses**  
   - **Buses**: Data moves between the CPU, RAM, disk, and other hardware via high-speed pathways called buses.  
   - **Memory Bus**: The CPU fetches instructions and data from RAM using the memory bus.  
   - **I/O Bus**: Data is transferred to and from devices (e.g., disk, keyboard, network) via I/O buses.

6. **Running Applications**  
   - **Loading Applications**: When you open a program (e.g., a web browser or Python script), the OS loads the program from disk into RAM for faster access.  
   - **CPU Executes Instructions**: The CPU fetches and executes the application’s instructions from RAM. The OS schedules tasks to be run by the CPU.

7. **Memory Management**  
   - **RAM Usage**: The kernel manages memory allocation. Active applications are stored in RAM for fast access.  
   - **Virtual Memory**: If RAM fills up, the OS may use virtual memory (on the disk) to extend available memory, though it's slower.

8. **Multitasking and Process Management**  
   - **Task Scheduling**: The OS kernel manages multiple applications (processes) at the same time, using multitasking. It allocates CPU time to each running program, making them appear to run simultaneously.  
   - **Interrupts**: The CPU handles multiple tasks by using interrupts, signals that tell the CPU to stop the current task and handle a more urgent one.

9.  **Device Interaction (I/O Operations)**  
   - **Input/Output Devices**: The CPU communicates with hardware devices (e.g., keyboard, monitor, printer) using device drivers (software that controls hardware).  
   - **Buses**: The I/O buses transfer data between the CPU and devices. For example, typing on a keyboard sends signals to the CPU, which are processed and displayed on the screen.

10. **Program Execution and Resource Management**  
    - **Kernel Control**: The kernel continuously manages resources like CPU cycles, memory, and devices to keep the system running smoothly.  
    - **File System**: When an application accesses files (e.g., reading/writing a file), the OS kernel manages file access and coordinates disk usage.

11. **Program Termination and Cleanup**  
    - **Closing Applications**: When you close an application, the OS frees up the memory in RAM and any other resources the program was using.  
    - **Garbage Collection**: In some programming languages (like Python), unused memory is automatically cleared using garbage collection to prevent memory leaks.

12. **System Monitoring**  
    - **Resource Monitoring**: The OS continuously monitors the system’s performance (e.g., CPU, memory usage, disk usage). It ensures that applications don’t use more resources than available.



```mermaid
graph TD
    A[Power On] --> B[BIOS/UEFI Initialization]
    B --> C[POST (Power-On Self-Test)]
    C --> D[Bootloader is found]
    D --> E[OS Loading]
    E --> F[Disk to RAM: OS loaded into RAM]
    F --> G[Kernel Initialization]
    G --> H[CPU Starts Fetch-Decode-Execute Cycle]
    H --> I[Fetch Instructions from RAM]
    I --> J[Decode Instructions]
    J --> K[Execute Instructions]
    K --> L[Data Transfer via Buses]
    L --> M[Memory Bus: Data moves between CPU and RAM]
    M --> N[I/O Bus: Data moves between CPU and Devices]
    N --> O[Running Applications]
    O --> P[Applications Loaded into RAM]
    P --> Q[CPU Executes Application Instructions]
    Q --> R[Memory Management]
    R --> S[RAM Usage]
    S --> T[Virtual Memory (if RAM is full)]
    T --> U[Multitasking and Process Management]
    U --> V[Task Scheduling: CPU time allocated to apps]
    V --> W[Interrupt Handling: CPU handles urgent tasks]
    W --> X[Device Interaction (I/O Operations)]
    X --> Y[Input/Output Devices communicate via drivers]
    Y --> Z[Data sent via I/O buses]
    Z --> AA[Program Execution and Resource Management]
    AA --> AB[Kernel controls CPU, memory, and devices]
    AB --> AC[File System: Manages file access on disk]
    AC --> AD[Program Termination and Cleanup]
    AD --> AE[Closing Applications]
    AE --> AF[Garbage Collection for unused memory]
    AF --> AG[System Monitoring]
    AG --> AH[OS monitors CPU, memory, disk usage]
```