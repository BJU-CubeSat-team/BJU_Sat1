# BJU CubeSat Data Storage Protocols

## Scope
The purpose of this document is to detail what protocols/conventions, and programming language should be used in data handling aboard the BJU CubeSat.  
The focus of this document is in data storage.  


## Recommended Language
The recommended language for this section of the on-sattelite code is C++ or Python.  
  
C++ has these following benefits:
 * Low level performance and flexibility similar to C, without many of C's common pitfalls
 * Native Static Typing
 * [Extensive Documentation](https://cplusplus.com/)
 * Well-documented Interoperability with Python
 * Many main boards and instruments for the sattelite have existing APIs in C++

Python has these following benefits:
 * It is easy to learn
 * It is fast to write
 * The old Pycubed software is written in Python already
 * [Extensive Documentation](https://docs.python.org/3/)

## Recommended structure for storage
Data storage in space has the added danger of radiation being able to corrupt data.  
Measures can be taken to minimized the danger of this happening, the best of which would be radiation hardened storage, but it shouldn't be our only insurance against data corruption.
  
Journaling should be enabled in the Operating System (and possibly database) we utilize onboard the sattelite (this is often NOT enabled by default).  

### In the case of a single computer
Data storage should take a similar approach to [RAID](https://en.wikipedia.org/wiki/RAID) 1, 5 and 10 storage protocols.  
While we likely will not have multiple data drives to work with, we can still create multiple partitions on a singular disk for storing data.  
  
These partitions should either have a RAID 1 approach where each partition is a copy of each other, or a RAID 5 approach where certain partitions are dedicated to parity.  
  
Ideally at the minimum, three partitions should be created. This will enable a voting system for preserving data.  
As part of the Data Service, a function should be defined to perform comparisons of multiple partitions with each other on a schedule (i.e. every 30 minutes, data integrity should be tested).  
In the case where one partition is found to be different from the other two(or more) partitions, it should be overwritten by the data from the other partitions.  
  
In the case where we have multiple computers aboard a sattelite, a similar approach may be taken with each computer acting as a data holder.  

Following each time data is received, a check should be initiated for each partition of data to ensure that all data was written uniformly.  

## Recommended Code Structure
### Data Storage as a Service Object
All storage of data should be defined in a class as a service object. This will aid in testing and security.  
This service class should hold all necessary data and functionality for decoding, encoding, storing and fetching data.  
  
All data within the class should be privatized, and only allowed to be altered via functions in which the allowed operations on the data are strictly defined.  
The functionality for transmitting/receiving data should be defined in a separate class.
  
### Testing
For testing, a mock Data Storage Service class should be defined.  
It should contain all the same functions of the Primary Data Storage Service, without access to real data. 

### Document version 0.1
* Edward Taylor