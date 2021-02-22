# Computer Networks


# Computer Networks

- Foreword:

    References:

    1. Videos: [2021王道计算机网络 on YouTube](https://www.youtube.com/watch?v=GOQInimk1Xc&list=PLuolGRW5AOPxEa0A2GNVIeFW9z0J-EIMe)
    2. eBook: [Google Drive Link here (Chinese) ](https://drive.google.com/file/d/1us0gQd7kkpIUF4DMEHh93aFiRIYEi_IV/view?usp=sharing)
    3. Power Point: [Google Drive Link here (Chinese) ](https://drive.google.com/drive/folders/1Mo-IynolgR-Js2qHV4k_0TX1HJZVbge6?usp=sharing)

## Ch 01. System's Structure of Computer Networks

- Definition:

    A System that connects distributed and independent Computer Systems through Devices and Cables, therefore the Resources-Sharing and Information-Transportation are realized. It's a Combination of connected and independent Computers.

- Functions:
  
    1. Data Communication

    2. Resources-Sharing

    3. Process distributly

    4. Improve the Reliability
   
    5. Balance the Load

- Development:

    APARnet -> internet -> Internet

- 3-Structures Internet:

    Bottom layer network -> middle layer network -> backbone network

- Some Terminologys:

    1. ISP - Internet Service Provider

        ![ISP]()

    2. IXP - Internet Exchange Point
    
    3. PCI ( Protocol Control Information ) + SDU ( Service Data Unit ) = PDU ( Protocol Data Unit, Unit between same-level Transportation )

- Standards

    1. OSI, TCP/IP

    2. RFC ( Request For Comments ):

        - Internet Draft
        - Proposed Standard
        - Draft Standard
        - Internet Standard

### __Performance Indicators__

1. Speed:

    - Transportation's Speed:
     __b/s ( $\times10^3$ ) $\rarr$ kb/s ( $\times10^3$ ) $\rarr$Mb/s ( $\times10^3$ ) $\rarr$Gb/s ( $\times10^3$ ) $\rarr$Tb/s...__

    - __Difference in Storage:__ 1Byte = 8bit, 1KB = $2^{10}$ B = 1024B = 1024 $\times$ 8b

2. Band-Width:

    - The Capacity of the Transportation of the Cable. Normally it refers to the highest Speed from one Point to another Point in Internet in Element-Time. Unit see above.

3. Throughput:

    - The Amount of Data that go through the Internet in Unit-Time. Unit see above. 

    - It's limited by Band-Width.

4. Delay:

    - Sending-Delay:

        $\text{S-Delay} = \frac{\text{Length of Data}}{\text{Band-width}}$ 
    - Transportation-Delay:

        $\text{T-Delay} = \frac{\text{Length of Band}}{\text{Electromagnetic wave speed}}$

    - Pending-Delay:

        Wait for the Usage of I/O Route

    - Process-Delay:

        Procedure with the Data

5. Time delay bandwidth product:

    - $\text{Time delay bandwidth product} = \text{Transportation-Delay} \times \text{Band-width}$

    - It talks about the Capacity of the Pipe.

6. RTT:

    - Delay between Sending and the Receive-Confirmation

    - Includes Transportation-Delay * 2 + Process-Time

7. Utilization rate

   1. Band Utilization Rate: $\frac{\text{Time, when Data pass}}{\text{Time, when Data pass and not pass}}$

### __OSI Reference Module__

1. Structure:
        
    Physic Layer $\rarr$ Data Link Layer $\rarr$ Network Layer $\rarr$ Transportation Layer ($\rarr$ Session Layer $\rarr$ Representation Layer) $\rarr$ Uasge Layer

2. Functions of __Representation Layer__

   - Transform the Data Format
   - Encrypt / Decrypt the Data
   - Compress and Decompress the Data

3. Functions of __Session Layer__

    - Creates, manage and terminites the Session 
    - Restore the Communication through Checkpoint when something wrong goes with the Communication ( SYN ).

4. Functions of __Transportation Layer__

    p.S. Responsible for the Communications between 2 Processes ( P2P )
    
    - Reliable / Unreliable Transportation
    - Control of Errors
    - Control of Flow
    - Multiplexing and splitting

5. Functions of __Network Layer__

    p.S. Transport the Groups from Source to the End, provide the Communication Service for the Groups to swap different Hosts.

    - Select the Route
    - Control of Flow
    - Control of Errors
    - Control of Congestion

6. Functions of __Data Link Layer__

    - Define the Begin and the End of the Frame
    - Control of Errors ( Frame Error, Bit Error )
    - Control of Flow
    - Control of Access

7. Functions of __Physic Layer__

    - Define the Features of Interface
    - Define the Transportation Mode
    - Define the Transportation Speed
    - Synchronization the Bits
    - Encode the Bits

## Ch 02. Physical Layer

### Basic Concepts

- Physical Layer solves how to transport Data Bit Flow on the Transportation Media on Hosts.

- Contains Mechanical Features, Electronic Features, Functional Features and Process Features.
