

## 安全开发方法论


### 威胁建模

威胁建模是安全开发方法论的核心组件。由于IoT技术和产品都位于不断变化的环境中，因此确保相关的威胁和问题被恰当的识别和处理是非常重要的。对软硬件实施威胁建模，识别潜在的威胁和恰当的缓解措施。

以下是针对IoT设备的威胁分类。

- 欺骗
- 篡改 
- 抵赖
- 信息泄漏
- 拒绝服务
- 权限提升
- 绕过物理安全

### 安全要求

根据相关法律法规的要求确定需要满足的安全要求。确保最小集的安全要求在开发中实施，并需要跟踪这些要求的在开发过程中的实施情况。

### 安全流程

可按照BSIMM模型构建安全开发流程。
- Governance
- Intelligence
- SSDL Touchpoints
- Deployment


### 安全影响评估

IoT将物理和电子世界融合在一起，对于大型IoT系统，即使很小的设备被破坏也可能产生严重的后果。这就需要相关人员考虑这点，并将安全影响评估作为其设计过程的一部分。

## 安全开发和集成环境

### 程序语言

不管使用什么语言进行IoT开发，都需要确保开发人员了解相关语言的安全开发最佳实践。

- C
  - [SEI CERT C Coding Standard](https://www.securecoding.cert.org/confluence/display/c/SEI+CERT+C+Coding+Standard)
  - [Motor Industry Software Reliability Association (MISRA)](http://www.programmingresearch.com/coding-standards/misra/misra-c3/)

- C++
  - [SEI CERT C++ Coding Standard](https://www.securecoding.cert.org/confluence/pages/viewpage.action?pageId=637)
  - [Motor Industry Software Reliability Association (MISRA)](http://www.programmingresearch.com/coding-standards/misra/misra-c3/)

- Java
  - [The CERT Oracle Secure Coding Standard for Java](https://www.securecoding.cert.org/confluence/display/java/The+CERT+Oracle+Secure+Coding+Standard+for+Java)
  - [Oracle Secure Coding Guidelines](http://www.oracle.com/technetwork/java/seccodeguide-139067.html)

### 集成开发环境

IDE可以使用一些安全插件。比如OWSAP ASIDE project可以集成到Eclipse中对Java和PHP进行漏洞扫描。其他还有Contrast for Eclipse，IOT eclipse。

### CI插件

在CI中可以使用像OWASP ZAP (Jenkins ZAP Plugin)来进行自动化的动态扫描。

### 测试和代码质量



### 流程

确保IoT产品使用的库来自可信站点。

在GitHub和GitLab中监控代码，防止插入未授权的代码。

## 识别框架和平台的安全特性

### 选择集成框架

在IoT开发时，有许多好的集成框架可以使用。可以根据实际需求和框架的特点进行选择。


### 评估平台安全特性

在开始设计系统的技术架构时，应充分考虑每个软硬件组件提供的安全特性。

此外还有操作系统的安全，现在很多IoT设备都运行在能够运行实时操作系统（RTOS）的小型但功能强大的SoC单元。

## 隐私保护

在设计阶段应考虑以下指导措施。

1. 设计IoT设备、服务和系统仅搜集最少且必须的数据内容

IoT生产商应该人工审查数据模型，应确保：尽量少的存储数据； 避免数据泄漏。

2. 分析设备用例以在必要时支持合规性要求

常见的合规要求有：
- Health Insurance Portability and Accountability Act (HIPAA)
- Children’s Online Privacy Protection Act - COPPA
- EU General Data Protection Regulation
- EU-US Privacy Shield

3. 设计IoT设备，服务和系统功能的选择要求

IoT设备开发者应该尽量想法来允许用户选择存储和共享的个人信息，并且应尽量提供细粒度的选择。

4. 实施技术隐私保护

- Privacy-enhanced Discovery Features
- Rotating Certificates

## 基于硬件的安全控制的设计

### The MicroController (MCU)

在选择SoC时应该考虑以下内容：
1. Does the SoC offer a cryptographic bootloader that can be leveraged to support secure firmware updates?
2. Does the SoC offer a cryptographic hardware accelerator to support efficient cryptographic processing, and what algorithms are supported by
the accelerator?
3. Does the SoC offer secure memory protection
4. Does the SoC offer built-in tamper protections (e.g., JTAG security fuses)
5. Does the SoC offer protection against reverse engineering?
6. Does the SoC offer secure mechanisms for cryptographic key storage in nonvolatile memory?

### Trusted Platform Modules

对于设备要处理或存储敏感信息的，建议在IoT设备中使用Trusted Platform Module (TPM)。

### Use of Memory Protection Units (MPUs)

MPUs provide access rules to memory locations, allowing IoT products that incorporate an MPU to control what memory can be read, written and executed.

### Incorporate Physically Unclonable Functions

Physically Unclonable Functions (PUFs) are information security devices that capture the value of deriving an identity from a physical attribute of an object

### Use of specialized security chips/coprocessors

安全芯片提供的功能有：
- Tamper-detection and and tamper-evidence
- Conductive shield layers in the chip that prevent reading of internal signals.
- Controlled execution to prevent timing delays from revealing any secret information.
- Automatic zeroization of secrets in the event of tampering.
- Chain of trust boot-loader which authenticates the operating system before loading it.
- Chain of trust operating system which authenticates application software before loading -t.
- Hardware-based capability registers, implementing a one-way privilege separation model.

### Use of cryptographic modules
The Federal Information Processing Standard (FIPS) 140-2 should be followed whenever implementing cryptographic protections within an IoT device. 

### Device Physical Protections
Tamper Protections
A good advice for implementing tamper protections ([link](http://electronics360.globalspec.com/article/5619/how-hackers-will-attack-your-embedded-system-and-what-you-can-do-about-it)).

### Guard the Supply Chain
所有供应链上的三方组件/库都需要进行安全检查以确保其安全性。

### Self-Tests
在启动时进行自检，以检查设备的安全性。如果识别到错误，则记录此错误并在恰当的地方停止继续处理。

### Secure Physical Interfaces
保护物理接口主要是防止提取产品固件并进行分析和修改。

Two areas of concern within IoT products are exposed:
- Universal Asynchronous Receiver Transmitter (UART) pins,
- Joint Test Action Group (JTAG) interface

It is therefore important to include a step in the engineering process that disables the interfaces before shipment. 
When possible, lock down USB ports to only trusted connections. 
Finally, remove debug code from the operational product to limit the attack surface.

## 数据保护



