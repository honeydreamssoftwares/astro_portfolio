---
title: FLIR Thermal Image Processing
publishDate: 2023-8-01 00:00:00
img: /assets/FLIR.png
img_alt: FLIR image processing
description: |
  Ported Java-based thermal image scanner software to Amazon Web Services by fixing Linux low-level libraries.
tags:
  - FLIR
  - Thermal Image Processing
  - JAVA
  - AWS
---

**Porting Java-based Thermal Image Scanner Software to AWS and Addressing Linux Low-Level Library Issues**

Modernizing traditional applications by porting them to cloud platforms, such as Amazon Web Services (AWS), offers benefits like scalability, resilience, and global reach. However, migrating applications, especially those interacting with low-level hardware and libraries, presents unique challenges. This discussion delves into the porting of a Java-based thermal image scanner software to AWS, with a focus on addressing the intricacies associated with Linux low-level libraries.

**1. Initial Assessment and Migration Strategy**

Before the migration began, the software's dependencies, particularly those tied to specific hardware or operating systems, were thoroughly analyzed. The objective was to identify the components that would require modifications, replacements, or workarounds to function correctly in a Linux environment on AWS.

**2. Java on AWS**

Java-based applications benefit from platform independence, but specific libraries or components might still be platform-dependent. AWS offers Amazon Corretto, a no-cost, production-ready distribution of the OpenJDK, ideal for running Java applications. The software was tested on Corretto to ensure compatibility.

**3. Challenges with Low-Level Libraries on Linux**

The primary challenge encountered during the migration was with the low-level libraries that the thermal image scanner software relied upon. These libraries were likely developed for a specific OS or even a custom environment, and moving to a standard Linux distribution on AWS posed issues:

- **Hardware Dependencies**: The software's tight coupling with specific thermal imaging hardware meant that virtual or cloud-based environments couldn't access these devices directly.
  
- **Library Compatibility**: Some native libraries, possibly developed for Windows or another OS, weren't directly compatible with Linux. Dynamic Link Libraries (DLLs) needed replacement or alternatives on Linux, which uses shared objects (.so files).

**4. Addressing Library Issues**

- **Hardware Abstraction**: To overcome direct hardware dependencies, an abstraction layer was introduced. This allowed the software to communicate with thermal devices via standardized APIs or protocols, making it more adaptable to cloud environments.

- **Library Replacement or Emulation**: For incompatible or outdated libraries, two primary strategies were employed:
  
  1. **Replacement**: Wherever possible, native Linux libraries that provided the same functionalities were identified and integrated. This might have required code changes, especially if function signatures or behaviors differed.
  
  2. **Emulation**: In cases where a direct replacement wasn't feasible or would be too time-consuming, emulation tools like Wine were considered. Wine allows Windows applications to run on Linux, offering a bridge for certain library functions.

- **Custom Wrappers**: For libraries with no direct replacements or those that couldn't be emulated effectively, custom wrapper libraries were developed. These wrappers acted as intermediaries, translating function calls between the Java software and the Linux OS.

**5. AWS Integration**

Once the library issues were addressed, the software was integrated with various AWS services:

- **Amazon EC2**: The Elastic Compute Cloud provided the virtual servers where the software ran. EC2 instances equipped with the necessary GPU or computational power were chosen to handle the intensive thermal image processing.

- **AWS Lambda & API Gateway**: For certain modular functionalities, serverless architectures were considered. AWS Lambda allowed specific functions of the software to be executed without provisioning an entire virtual server, while API Gateway facilitated the software's interaction with other services or devices over the web.

- **Amazon S3**: Thermal images, logs, and other relevant data were stored in S3 buckets, benefiting from its durability and scalability.

**6. Testing and Optimization**

After migration, rigorous testing was undertaken. This involved not only checking software functionalities but also ensuring that the replaced or wrapped libraries performed as expected.

In conclusion, while porting a Java-based thermal image scanner software to AWS presented challenges, particularly with low-level libraries, a methodical approach focusing on abstraction, emulation, and integration ensured a successful migration. The newly cloud-enabled software now benefits from the robustness, scalability, and global accessibility that AWS offers.