# BJU CubeSat Communication Protocols

## Scope
The purpose of this document is to detail what protocols/conventions, and programming language should be used in outward and incoming communication aboard the BJU CubeSat.  
The focus of this document is the transmission of data to and from the sattelite and ground base.  

## Recommended Language
The recommended language for this section of the on-sattelite code is C++ or Python.  
  
C++ has these following benefits:
 * Low level performance and flexibility similar to C, without many of C's common pitfalls
 * Native Static Typing
 * Well-documented Interoperability with Python
 * Many main boards and instruments for the sattelite have existing APIs in C++
 * [Extensive Documentation](https://cplusplus.com/)

Python has these following benefits:
 * It is easy to learn
 * It is fast to write
 * The old Pycubed software is written in Python already
 * [Extensive Documentation](https://docs.python.org/3/)
  
## Recommended Protocol(s)
The recommended primary protocol for data transfer for the sattelite is SCPS-TP (Space Communications Protocol Specification - Transport Protocol).
This protocol is detailed [here](https://ccsds.org/wp-content/uploads/gravity_forms/5-448e85c647331d9cbaf66c096458bdd5/2025/01//714x0b2.pdf).  
A pdf copy should be in the github repository.  
  
This protocol was ratified by the CCSDS (Consultative Committee for Space Data Systems) and is utilized by NASA.  
In the case additional protocols for data transmission are required, the CCSDS has likely defined all the protocols we would require for any data type.  
[CCDS Homepage](https://ccsds.org/)  
[CCDS documents](https://ccsds.org/publications/bluebooks/)  

## Recommended Code Structure
### Data Transmission as a Service Object
All transmission of data should be defined in a class as a service object. This will aid in testing and security.  
This service class should hold all necessary data and functionality for decoding, encoding, sending, and receiving data.  
  
All data within the class should be privatized, and only allowed to be altered via functions in which the allowed operations on the data are strictly defined.  
The functionality for storing data should be defined in a separate class.
  
### Testing
For testing, a mock Data Transmission Service class should be defined.  
It should contain all the same functions of the Primary Data Transmission Service, without access to real data.  

### Document version 0.1
* Edward Taylor