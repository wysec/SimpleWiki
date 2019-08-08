## Secure Software Implementation/Coding

### Fundamental Concepts of Programming

#### Computer Architecture

- 现代计算机主要构成：computer processor、system memory、Input/Output(I/O)devices。
- Computer processor即central processing unit(CPU)，由这些组成：Arithmetic Logic Unit (ALU)（对数据算术和逻辑操作）、Control unit（控制系统其他部分）、Registers（内部存储区）。
 -Internal memory layout has the following segments: program text, data, stack and heap.

#### Evolution of Programming Languages

- Machine Language, Assembly Language, High-level language, Very High-level Language, Natural Language。
- **Compiled Languages** - COBOL, Fortran, BASIC, Pascal, C, C++ and Visual Basic。程序源码转为机器码，有两步：Compilation、Linking(staic\dynamic)。
- **Interpreted Languages** - have the need for an intermediary host program to read and execute each statement of instruction line by line. Eg: REXX, PostScript, Perl, Ruby and Python.
- **Hybrid Languages** - the source code is compiled into an intermediate stage which resembles object code. The intermediate stage code is then interpreted as required。Java、.Net

### Common Software Vulnerabilities and Controls

- 导致系统被攻破的根本原因：design flaws、coding(implementation)issues、improper configuration and operations、software coding weaknesses。
- 一些主要的vulnerability databases：The National Vulnerability Database (NVD)、US Computer Emergency Response Team (CERT) Vulnerability Notes Database、Open Source Vulnerability Database、Common Vulnerabilities and Exposures (CVE)、OWASP Top 10、Common Weakness Enumeration (CWE™)。
- 以下是常见的软件安全漏洞和风险的介绍：

#### Buﬀer Overﬂow

- A buffer overflow is the condition that occurs when data that is being copied into the buffer (contiguous allocated storage space in memory) is more than what the buffer can handle.
- **Stack Overﬂow** - the memory buffer has been overflowed in the stack space。strcpy()和strcat()函数会导致栈溢出。[参考](https://bbs.pediy.com/thread-131340.htm)
- **Heap Overﬂow** - 
- 防御缓冲区溢出攻击的措施：1选择有自己的内存管理和类型安全的语言（Java、.Net等）；2使用安全的库或框架（如SafeStr）；3使用安全的函数；4验证值的最大、小值；4利用编译器安全性（/GS、StackGuard）；5利用操作系统功能（ASLR、DEP、ESP）；6使用内存检查工具（MemCheck、Memwatch...）。

#### Injection Flaws

- 攻击者提交的数据被作为命令执行。SQL injection、OS Command injection、LDAP injection、XML injection。
- 注入的防御措施：1验证所有用户输入；2用恰当的字符集对输出进行编码；3结构化机制分离代码和数据；4避免动态查询（SQL、LDAP、XPATH、XQuery）；5使用安全API（ESAPI）；6参数化查询；7显示通用错误信息；8重定向所有错误到通用错误页面并记录日志；9移除数据库所有不需要的函数和过程；10使用视图来实施最小权限；11审计查询日志；12在沙箱执行OS命令；13允许执行命令白名单；14LADP查询使用\escape method。

#### Broken Authentication and Session Management

- 防御措施：1使用成熟的认证和会话管理机制；2使用单一和集中的认证机制；3使用唯一随机不可预知的会话标识符；4认证凭证加密；5不要硬编码数据库连接字符串；6通过安全信道认证用户；7不要暴露会话ID在URL中；8确保XSS保护机制有效；9密码改变时要求重新认证；10不要用自定义的cookie；11不要在客户端存储、缓存、维护状态信息；12所有页面有logout链接；13设置会话超时时间等；14设置认证失败次数限制；15加密client/server通信；16实施传输层加密。

#### Cross-Site Scripting (XSS)

- 防御措施：1输出到客户端要先被净化处理（转义、编码）；2白名单验证用户输入内容；3不允许上传.htm/.html文件；3在存储输入数据时使用innerText代替innetHtml；4使用处理XSS的安全的库和编码框架（ESAPI）；5客户端可禁用脚本；6使用HTTPOnly标志；6使用WAF。

#### Insecure Direct Object References

- 应避免使用直接对象引用暴露内部功能。
- 防御措施：1通过映射表使用间接对象引用；2不要通过URL或表单参数暴露内部对象；3掩码或加密暴露的参数；4验证参数以确保修改时允许的；5每次参数修改时执行多访问控制和认证检查；6使用RBAC

#### Security Misconfguration

- 防御措施：1安装后修改所有默认配置；2移除所有不需要的服务和进程；3建立和维护基线安全配置；4建立加固应用的流程；5建立补丁流程；6建立扫描和检测流程；7处理错误时从定向到错误页；8移除样本应用；9部署应用是低耦合、高内聚。

#### Sensitive Data Exposure

- 敏感数据暴露的主要原因：Insufcient data-in-motion protection（传输泄露）、Insufcient data-at-rest protection（存储泄露）、Electronic social engineering。
- 防御措施：1阻止脚本访问cookie中的数据；2设置浏览器不要保存/缓存历史纪录；3禁用自动完成功能；4禁止缓存敏感数据，或加密保存；5不要在生产环境放备份文件；6加固服务器以保护日志文件；7安装脚本和修改日志不要放在生产系统；8注释中不要有敏感信息；9使用静态代码分析工具；10不需要就不要收集和存储敏感信息，存储的加密保存；11密码哈希处理；12端到端加密保护（TLS、IPSec）；13所有通信加密；14cookie有secure标志；15使用安全的加密算法；16恰当配置数字证书；17安全意识培训，防钓鱼灯；18敏感数据和管理员访问职责分离。

#### Missing Function Level Checks

- 失败的限制对特权功能/URLs的访问。

#### Cross-Site Request Forgery (CSRF)

- 防御措施：1使用nonce；2使用CAPTCHAs；3在服务端验证；4使用POST方法；5检查referrer；6敏感事务再次认证；7自动登出功能；8使用已有方案（ESAPI等）；9防止XSS。

#### Using Known Vulnerable Components

#### Unvalidated Redirects and Forwards

- 防御措施：1避免重定向和转发；2使用白名单的目标URLs；3不允许用户指定目标URL；4使用映射；5使用中间页提醒用户重定向到外部站点；6防止脚本攻击的漏洞。

#### File Attacks

- 防恶意文件执行：1使用允许文件格式的白名单；2一个文件仅允许一个后缀名；3重定向映射；4明确的污点检查；5使用自动产生的文件名；6上传文件到加固的临时环境；7避免使用文件函数和基于流的API来构造文件名；8配置要求恰当的文件权限；
- 防路径遍历：1使用白名单验证文件路径和位置；2限制字符；3不允许目录浏览；4解码并标准化；5映射；
- 防文件包含：1在根目录或系统目录之外存储；2限制对特定目录文件的访问；3限制从远程位置包含文件；4下载代码进行完整性检查；5检测DNS欺骗攻击；6监控文件的执行情况；

#### Race Condition

- 发生竞争条件要同时满足这三个属性：并发、共享对象、改变状态。
- 防御措施：1识别和消除竞争窗口；2共享资源执行原子操作；3使用互斥操作；4关键代码周围使用synchronization primitives；5使用多线程和线程安全；6尽量少使用共享资源；7禁用关键代码段上的中断或信号；8避免无线循环；9实施简单设计原则；10对错误和异常处理。

#### Side Channel Attacks

- 边信道攻击类型：
	- Timing attacks - the attacker measure how long each computational operation takes and uses that side channel information to discover other information about the internal makeup of the system. Eg:利用错误信息延迟时间来进行盲注攻击。
	- Power Analysis attacks - the attacker measures the varying degrees of power consumption by the hardware during the computation of operations。Eg:破解RSA key。
	- TEMPEST attacks - 根据泄露的电磁辐射分析相关信息。
	- Acoustic Cryptanalysis attacks - 根据计算过程产生的的声音进行分析攻击。
	- Diﬀerential Fault Analysis attacks - 差分故障分析攻击旨在通过故意将故障注入计算操作并确定系统如何响应故障来发现系统的秘密。
	- Distant Observation attacks - 攻击者从远处间接观察并发现系统信息。如，通过望远镜或使用反射图像观察某人的眼睛，眼镜，监视器或其他反射设备。
	- Cold Boot attacks - 攻击者可以通过冻结内存芯片的数据内容并启动以恢复内存中的内容来提取秘密信息。
- 防御措施：1使用最佳实践的加密算法；2使用计算操作的时间与输入数据或密钥大小无关的系统；3避免使用IF-THEN-ELSE；4标准化每次计算所需的时间；5独立于操作类型的平衡功耗；6增加噪声；7物理屏蔽；8双重加密（防差分错误）；9物理保护内存芯片。

### Defensive Coding Practices – Concepts and Techniques

- The secure software is more than just writing secure code, implementing controls in code can have a huge impact on the resiliency of the software against hacker threats.
- To reduce attack surface of code：1.reducing the amount of code and services that are executed by default; 2.reducing the volume of code that can be accessed by untrusted users; 3.limiting the damage when the code is exploited.
- The following section is about *defensive coding practices and techniques* are used in reducing the attack surface and assuring the reliability, resiliency and recoverability of software.

#### Input Validation

- It is more important to verify, all input is evil and validate all user input.
- Input validation ensures the data that is supplied: 1 correct data type and format; 2 expect and allow range of values; 3 is not interpreted as code; 4 don't bypass security controls.

##### How to Validate?

- Regular expressions(RegEx), whitelist/blacklist.

##### Where to Validate?

- It is recommended that the input is validated both on the client(frontend) as well as on the server(backend). Minimally, server side validation must be performed.

##### What to Validate?

- These should be validated: 1.data type, 2.range, 3.length, 4.format, 5.values, 6.alternate representations of a standard (canonical) form.

#### Canonicalization

- Canonicalization/C14N is the process of converting data to a standard canonical form.
- The appropriate character set and output locale are set in the software to avoid any canonicalization issues.
- It is recommended to decode once and canonicalize inputs into the internal representation before performing validation.

#### Sanitization

- It is the process of converting something that is considered dangerous into its innocuous form. Both inputs and outputs can be sanitized.
- The methods of input sanitization(before data is processed): 1.**Striping**(removing harmful characters from user supplied input), 2.**Substitution**(replacing user supplied input with safer alternatives), 3.**Literalization**(using properties that render the user supplied input to be treated as a literal form).
- Output sanitization is usually performed by encoding: 1.**HTML entity encoding**(the meta-characters and HTML tags are encoded to their corresponding character entity references. eg:< = &lt), 2.**URL encoding**(characters be encoded into their Unicode Character set code. eg:< = %3C).
- It is important to make sure that *the integrity of the data is maintained when sanitization*.

#### Error Handling

- The error messages must be non-verbose and explicitly specified in the software.
- Organizations are tolerant of user errors which are inevitable. eg: user login.
- Tips: Use non-verbose error messages with just the needed information. Use an index of the error value or reference map. To redirect errors and exceptions to a custom defalut page.

#### Safe APIs

- Threat modeling should identify APIs as potential entry points. Banned and deprecated API that should be avoided an replaced with secure counterparts.
- It is imporatant to ascertain that proper authentication is in place, to audit the privileged functions actions, to use CryptoAPI Next Generation (CNG).


#### Memory Management

...

#### Exception Management

- Errors may be a result of user ignorance or software breakdown, exceptions are software issues that are not handled explicitly when the software behaves in an unintended or unreliable manner. 
- All exceptions must be explicitly handled. Eg: use try-catch-finally to catch all exception block.
- Compiled Languages can use the Safe Security Exception Handler (/SAFESEH) flag in system that support it.

#### Session Management

- Use the unique session token to track user activity and to prevent someone who is attempting to hijack a valid session.
- The controls can refer the Broken Authentication and Session Management section.

#### Confguration Parameters Management

- Two main configurable parameters include startup variables and cryptographic keys. 
- **Secure Startup** - It is imperative to ensure that the software startup process itself is secure. These environment variables and configuration parameters are initialized that need to be protected from disclosure, alteration or destruction threats.

#### Cryptography

- Prevention and mitigation techniques to address insecure cryptography issues:
- Some data-at-rest protection controls includes: 1.encrypting and storing the sensitive data as ciphertext; 2.storing salted ciphertext versions of the data; 3.not allowing sensitive data to cross trust boundaries(from safe zone into unsafe zone); 4.separating sensitive from non-sensitive data (if feasible).
- Appropriate algorithm usage: 1.not using custom algorithm; 2.use standard algorithm(eg:AES); 3.not use older cryptography APIs; 4. consider the ability to quickly swap cryptographic algorithms as needed
- Cryptographic agility, the application is architected to reference the cryptographic algorithm or hashing function outside the application code itself, so that it can be easily swapped, when required.
- SDL banned and acceptable/recommended cryptographic algorithms:

| Type of Algorithm | Banned Algorithm                                | Acceptable/Recommended Algorithm                      |
| ----------------- | ----------------------------------------------- | ----------------------------------------------------- |
| Symmetric         | DES, DESX, RC2, SKIPJACK, SEAL, CYLINK_MEK, RC4 | 3DES,  AES                                            |
| Asymmetric        | RSA (<2048bit), DifeHellman(<2048bit)           | RSA(>=2048bit), DifeHellman(>=2048bit), ECC(>=256bit) |
| Hash              | SHA-0 (SHA), SHA-1, MD2, MD4, MD5               | SHA-2 (includes: SHA-256, SHA-384, SHA-512)           |

- Don't hard-coded specific algorithms in code, maintaining the specification of the algorithm or hashing function outside the application code itself, such as configuration files at the application or machine level. In addition, the implementation of the algorithm should be abstract within the code, e.g: SymmetricAlgorithm or AsymmetricAlgorithm.
- Secure key management means that the: 1.generation of the key uses a random or pseudo random number generator(RNG or PRNG); 2.exchange of keys is done securely using out-of-band mechanisms or approved key infrastructure; 3.storage of keys is protected, preferably in a system that is not the same as that of the data; 4.rotation of the key where one key is replaced by another follows the appropriate process of frst decrypting data with the old key that will be replaced and then encrypting data with the new key that is replacing the old key; 5.archival and escrowing of the key is protected with appropriate access control mechanisms and preferably not archived in the same system as the one that contains the encrypted data archives; 6.destruction of keys ensures that once the key is destroyed, it will never again be used. 
- Adequate access control and auditing means that for both internal and external users, access to the cryptography keys and data is: 1.granted explicitly; 2.controlled and monitored using auditing and periodic reviews; 3. enough security; 4.contextually appropriate and protected, irrespective of whether the encryption is one-way or two-way.

#### Concurrency

- Concurrency (simultaneous operations) is a primary property in TOC/TOU attacks.
- Some of the protection measures against race conditions or TOC/TOU are: Avoid race windows; Atomic operations; Mutual Exclusion(Mutex).

#### Tokenization

- Tokenization is the process of replacing sensitive data with unique identification symbols that still retain the needed information about the data.

#### Sandboxing

- Sandbox creates a separation from the host operating system. Running code in a sandbox (or jail) restricts the access that the code has on other system resources. Eg:chroot, AppArmor, SElinux.

#### Anti-Tampering

- Some of the well-known anti-tampering techniques: 
- **Obfuscation** - To make the code with generic variable names, convoluted loops, conditional constructs and renaming textual and symbols within the code to meaningless character sequences, so that the source code is not easily readable and decipherable.
- **Anti-Reversing Techniques** - removing symbolic information (eliminating any symbolic information such as class names, class member names, names of global instantiated objects, etc., and stripping other textual information) from the Progam Executable (PE) and embedding anti-debugger code (a user or kernel level debugger detector is included as part of the code, eg:IsDebuggerPresent API, SystemKernelDebuggerInformation API). 
- **Code Signing** -  digitally signing the code (executables, scripts..) with the digital signature of the code author, it can assure authenticity of published code, integrity and anti-tampering.

### Secure Software Processes

- Software assurance is a confluence of secure processes, technologies, people.
- There are certain processes that must be conducted during the implementation phase that can assure the security of the software: 
- **Versioning (Confguration Management)** - 1.ensures that the development team is working with the correct version of code; 2.gives the ability to rollback to a previous version should there be a need to; 3.to track ownership and changes of code.
- **Code Analysis** - inspecting the code for quality and weaknesses that can be exploited, it include static code analysis and dynamic code analysis.
- **Code/Peer Review** - the code be inspected for the following: Insecure code(injection flaws, non-repudiation mechanisms, spoofing attacks, errors and exception handing, cryptographic strength, unsafe and unused functions and routines in code, reversible code, privileged code,maintenance hook, logic bombs, timing and synchronization implementations, cyclomatic complexity,); Inefficient code.

### Securing Build Environments

- The integrity of the build environment can be assured by: 1.Physically securing access to the systems that build code; 2.Using access control lists (ACLs) that prevent access to unauthorized users; 3.Using version control software to assure that the code built is of the right version; 4.Build automation is the process of scripting or automating the tasks that are involved in the build process. 


## Secure Software Testing

### Quality Assurance

- QA of software can be achieved by testing its reliability (functionality), recoverability, resiliency (security), interoperability and privacy. 
- Software is high quality may not necessarily mean that it is secure. Security is another attribute of quality, as is privacy and reliability. Software is secure can be considered higher quanlity.

#### Testing Artifacts

- The difference types of testing artifacts:
- **Test Strategy** - The test strategy outlines the testing approach that will be undertaken.It also includes information about the testing goals, methods, time needed, test environment configuration and needed resources. It describes the types of tests that are to be performed and the success/fail criteria at a high level. It usually reference design documents, the data classification, threat model, subject/object matrix, access control lists, etc.
- **Test Plan** - is much more granular document that details the testing approach systematically. it is the workflow that a tester would perform. The three primary components of a test plan includes: 1.test requirements (or responsibility), 2.test methods, 3.test coverage.
- **Test Case** - A test case takes the test requirements from the test plan and defines measurable conditions to validate that the requirements are indeed being met as expected. Generally a test case contains: 1) a unique identifier, 2) a reference to the requirements specification that is being validated, 3) any preconditions that need to be met, 4) actions (also known as test steps), 5) test inputs, 6) expected results (when the test steps are completed).
- **Test Script** - a test script answers the question “How am I going to perform the tests?”. Test scripts are developed using the test case.
- **Test Suite** - a collection of test cases makes up a test suite. such as functional tests, performance tests, etc.
- **Test Harness** - all the components that are necessary to conduct software testing. This includes: testing tools, test data samples, testing configurations, test cases and test scripts. It can be reused by multiple projects.

#### Types of Software QA Testing

##### Functional Testing

- Software testing is performed to primarily attest the functionality of the software as expected by the business or customer. It is also referred to as *reliability testing*. //软件按预期执行
- **Unit Testing**, to conduct by developers, it is the first process to ensure that the software is functioning properly, according to specifications, it is performed during implementation phase(coding) of SDLC, a small part is tested in isolation from others. It can be used to find Quality of Code (QoC) issues as well.
- **Logic Testing**, validates the accuracy of the software processing logic.
- **Integration Testing**,  individual units of code are aggregated and tested.
- **Regression Testing**,  to validate that the software did not break previous functionality or security. //重复执行以前的全部或部分相同的测试工作

##### Non-Functional Testing

- Non-functional testing covers testing for the recoverability and environmental aspects of the software.(load balancing, interoperability and disaster recovery mechanisms, etc.)
- **Performance Testing**, Load Testing identifying the maximum operating capacity for the software. Stress Testing to determine the breaking point of the software.
- **Scalability Testing**, to identify the loads and to mitigate any bottlenecks. Environment Testing. Interoperability Testing. Disaster Recovery (DR) Testing.
- **Simulation Testing**, 

##### Other Testing
- **Privacy Testing**
- **User Acceptance Testing (UAT)**, 

### Attack Surface Validation (Security Testing)

- Security testing is a test for the resiliency of software. To attest the presence and effectiveness of the security controls that are designed and implemented in the software. Security testing begins from high risk items to low risk items.

#### Motives, Opportunities and Means

- If an attack to be successful there needs the three aspects: motive, opportunity and means. 
- The opportunities and means can be determined by security testing.

#### Testing of Security Functionality versus Security Testing

- **Security testing** is testing with an attacker perspective to validate the ability of the software to withstand attack (resiliency), while **testing security functionality** (authentication mechanisms, auditing capabilities, error handling, etc.) in software is meant to assure that the functionality of protection mechanisms are working properly.
- Though security testing is aimed at validating software resiliency, it can also be performed to attest the reliability and recoverability of software.

#### The Need for Security Testing


### Security Testing Methods

- White Box Testing
- Black Box Testing

### Types of Security Testing

- Cryptographic Validation Testing
- Scanning
- Fuzzing

### Software Security Testing

- Security testing should ensure comprehensive coverage of the varied threats to software. Eg: STRIDE threat lists.

#### Testing for Input Validation

- Attributes of the input such as its range, format, data type, and values must all be tested. 
- Input validation test can be conducted using pattern matching expression(Regular Expression, RegEx) and/or fuzzing techniques
- To test white-list and black-list, canonicalization.

#### Testing for Injection Flaws Controls

#### Testing for Scripting Attacks Controls

#### Testing for Non-repudiation Controls

- Test cases should validate that audit trails can accurately determine the
actor and their actions.
- Test cases include the audit trail and the integrity of audit logs(NIST SP 800-92). The confidentiality of the audited information and its retention for the required period of time.

#### Testing for Spoofng Controls

- Both network and software spoofing test cases need to be executed.
- Network spoofing include: ARP poisoning, IP address spoofing, MAC address spoofing.
- Software spoofing include: user and certificate spoofing, phishing

#### Testing for Error and Exception Handling Controls (Failure Testing)

- Software security failure testing includes the verification of the following security principles:
    - Fail Secure (Fail safe)
    - Error and Exception Handling, to test the messaging and encapsulation of error details.
    - Testing for Buffer Overﬂow Controls

#### Testing for Privileges Escalations Controls

- vertical or horizontal

#### Anti-Reversing Protection Testing

### Tools for Security Testing

- Production data must never be imported into and processed in test
environments.
- Production environment --> Test data management(Data Subsetting, Data Masking, Dummy Data Generation) --> Test environment.

### Defect Reporting and Tracking

- Software defects(coding bugs, design flaws, behavioral anomalies (logic flaws), errors & faults， vulnerabilities) need to be reported, tracked and addressed.

#### Reporting Defects

- The goal of reporting defects is to ensure that they get addressed. Information that must be included in a defect report is:
    - Defect Identifer (ID)
    - Title
    - Description
    - Detailed steps, to detail steps as to how the defect can be reproduced by the software development team.
    - Expected Results, to describe what the expected result of the operation
    - Screenshot
    - Type, it is recommended to categorize the defect, 
    - Environment
    - Build Number
    - Tester Name
    - Reported On, The date and time (if possible) as to when the defect was reported needs to be specified.
    - Severity
    - Priority
    - Status -  ‘New’, ‘Confirmed’, ‘Assigned’, ‘Work-in-progress’, ‘Resolved/Fixed’, ‘Fix verified’, ‘Closed’, ‘Re-opened’, ‘Deferred’, etc.
    - Assigned to
    
#### Tracking Defects

- It is advisable to track all defects in a centralized system.

#### Impact Assessment and Corrective Action

- 可通过priority (urgency) 和severity (impact)来确定影响级别，并进行处理。
- Corrective actions have: 1Fixing the defect (mitigating the risk); 2Deferring the functionality (not the fix) to a latter version (transferring the risk); 3Replacing the software (avoiding the risk).


## Software Acceptance

### Guidelines for Software Acceptance

- Acceptance criteria must be predefined with respect to the following categories: Functionality, Performance, Quality, Safety, Privacy and Security.
- Some of the guiding principles of software that is ready for release from a security viewpoint are given below. 
    - be secure by design, default and deployment;
    - complement existing defense in depth protection;
    - run with least privilege;
    - be irreversible and tamper-proof;
    - isolate and protect administrative functionality and security management interfaces; 
    - have non-technical protection mechanisms in place.(legal..)
    
### Benefts of Accepting Software Formally

- Software acceptance ensure that new software has achieved a formally defined level of quality and security.

### Software Acceptance Considerations

- Some of the major items to consider before accepting software:
- **Completion Criteria** - All of the functional and security requirements completed as expected. _RTM, Threat model, Security architecture design, Code review report, Security test report_ ... have actual deliverable. It can be tracked and verified.
- **Change Management** - There is a process in place to handle change requests. All changes need to be formally requested and approved.Change requests should be approved based on risk.
- **Approval to Deploy or Release** - All of the required authorities signed off. It includes review and oversight through an established governance process for maximum effectiveness. Approvals must be documented and retained.
- **Risk Acceptance and Exception Policy** - The residual risk acceptable / tracked as an exception. A risk acceptance template include: Risk, Action, Issues, Decisions(RAID)
- **Documentation of Software** - All necessary documentation in place.(Eg: RTM, Threat Model, Risk Acceptance Document, Exception Policy Document , Change Requests, Approvals, BCP/DRP, Incident Response Plan (IRP), Installation Guide, User Training Guide/Manual.)

### Verifcation and Validation (V&V)

- **Verification** is defined as the process of evaluating software to determine whether the products of a given development phase satisfies the conditions imposed at the start of the phase. In other words, verification ensures that *the software performs as required and expected to*.
- **Validation** is the process of evaluating software during or at the end of the development process to determine whether it satisfies specified requirements. In other words validation ensures that *the software meets required specifications*.
- V&V is a required step in the software acceptance process. It is divided into two main activities: Reviews, Testing.
- the V&V process must verify the correct implementation of the security features.

#### Reviews

- Reviews can be conduct to ensure that the software performs as expected and meets business specifications.
- It include informal reviews and formal review.
- Design reviews are conducted to detect architectural flaw, it is the validation of software. Code review involve line-by-line review of the code and step-by-step inspection of of software functionality and assurance capabilities, it is in the verification of software.
- The use of tools is useful, but careful attention the false positive and false negatives. 

#### Testing

- Testing can help demonstrate that the software truly meets the requirements.
- The different kinds of test in V&V: 
    - Error Detection Tests，it include unit and component level testing. Errors may be flaws (design issues) or bugs (code issues).
    - Acceptance Tests, -  to demonstrate if the software is ready for its intended use or not.
    - Independent (Third party) tests, - it can be neutral and objective in reporting their findings.

### Certification and Accreditation (C&A)

- **Certification** is the *technical verification* of the software functional and assurance levels.(e.g., CC)
- **Accreditation** is *management’s formal acceptance* of the system after an understanding of the risks to that system rating in the computing environment.
- Software must not be accepted as ready for release unless it is certified and accredited. After the V&V process, evaluator can rate the software on functional and assurance requirements. then it can make a determination as to whether the software is to be accepted or not.

## Software Deployment, Operations, Maintenance, and Disposal

- Once software is deployed, it needs to be monitored to guarantee that the software will continue to function in a reliable, resilient and recoverable manner.

### Installation and Deployment

- Some of the necessary pre- and post-installation configuration management security considerations include:

#### Hardening

- Before the software is installed into production environment, the host hardware and operating system needs to be hardened.
- To use baseline or Minimum Security Baseline (MSB) to keep the system is secure level.
- Not only to harden host operating system by using MSB, updates and patches, but it is also should harden the application and software run on top of it.
- Hardening of software involves correct configuration settings and architecting the software to be secure by default. 
- Hardening software code include: 1Removal of maintenance hooks; 2Removal of debugging code and ﬂags; 3removing unneeded comments or sensitive information.

#### Environment Configuration

- Coniguration should meet security principles(least privilege, defense in depth...).
- the development and test environment match the configuration makeup of the production environment.
- Additional configuration considerations include: 1Test and default accounts need to be turned off; 2Unnecessary and unused services need to be removed; 3Access rights need to be denied by default and granted explicitly even in development and test environments.

#### Release Management

- Software release should be in formal and controlled manner.
- Release management is the process of ensuring that all changes that are made to the computing environment are planned, documented, thoroughly tested and deployed with least privilege, without negatively impacting any existing business.
- bugs->fix in development environment->to the test environment->user acceptance testing environment->production environment.
- The versioning, backups, check-in and check-out practices are all managed as part of the release management process. These need to be maintained and documented.
- To document and maintain the configuration information in a formal and structured manner.(such as： CMDB)

#### Bootstrapping and Secure Startup

- Power-on self-test(POST) of Initial Program Load (IPL) be protected by TCB.
- The access to the BIOS be protected by using password.
- the hardware’s Trusted Platform Module (TPM) chip that provides heightened tamperproof data protection during startup. TPM chip can store cryptographic keys and provide identification information from mobile devices for authentication and access management. It have a system fingerprint.

### Operations and Maintenance

- Released software needs to be monitored and maintained. Software operations and maintenance need to take into account the assurance aspects of reliable, resilient and recoverable processing. It is about risk management.
- Operations security is about staying secure or keeping the resiliency levels of the software above the acceptable risk levels.
- Types of Operations Security Controls: 
    - **Detective** 侦探 (Auditing/logging, IDS)
    - **Preventive** 预防 (input validation, output encoding, IPS)
    - **Deterrent** 威慑 (auditing)
    - **Corrective** 纠正 (Load balancing, clustering, failover of data and systems)
    - **Compensating** 补偿
- Some of the ongoing activities that are useful to ensure that the software stays secure:

#### Monitoring

##### Why Monitor?

##### What to Monitor?

- Monitoring can be performed on any system, software or their processes. 
- Firstly, to determine the monitoring requirements. it come from business, governance requirements(internal and external regulatory policies).
- 监控内容：1any operations that can cause a disruption to the business；2operations that are administrative, critical and privileged；3operate in environments that are of low trust(DMZ).
- physical access also should be monitored. that can use video cameras. the data must be stored for a minimum of three months(from PCI DSS)

##### Ways to Monitor

- The primary ways of monitor:
    - Scanning 
    - Logging
    - Intrusion detection
    
##### Metrics in Monitoring

- Characteristics of good metrics include: Consistency, Quantitative, Objectivity, Relevance, Inexpensive
- Although it is important to use good metrics, but bad metrics also maybe is useful.

##### Audits for Monitoring

- Audit can be used to determine the organization’s compliance with the regulatory and governance (policy) requirements and report on violations of the security policies.

#### Incident Management

- NIST SP 800-61 Computer Security Incident Handling Guide prescribe guidance:1monitoring; 2to determine if the reported or suspected incident is truly, 3to determine the type of incident; 4to minimize the loss and destruction and to correct, mitigate, remove and remediate exploited weakness;...

##### Events. Alerts, and Incidents

- Any action that is directed at an object which attempts to change the state of the object is an **event**. In other words, an event is *any observable occurrence in a network, system or software*.
- When events match preset conditions or patterns, they generate **alerts** or red flags.
- Alerts can be categorized into incidents and adverse events can be categorized into security incidents if they violate or threaten to violate the security policy of the network, system or software applications.
- Events generate alerts which can be categorized into incidents.

##### Types of Incidents

- There are several types of incidents and the main security incidents include:
    - Denial of Service (DoS)
    - Malicious Code
    - Unauthorized Access
    - Inappropriate Usage
    - Multiple Component
- The creation of what is known as a diagnosis matrix is also recommended. 帮助进行事件分类    

##### Incident Response Process

- The major phases of the incident response process are:
1. **Preparation** - to limit the number of incidents by implementing controls that were deemed necessary from the initial risk assessments. create, provision and operate a formal incident response plan.
2. **Detection and Analysis** -  to look at the logs or audit trails. The log analysis process: 1Collection, 2Normalization, 3Correlation, 4Visualization. (Logging, reporting and alerting are all part of the information gathering activity and is the first step in incident analysis)
3. **Containment, Eradication and Recovery** - 当发现事故时，首先是要控制住，避免破坏扩大。Incident data and information is privileged information and must be restricted to only authorized personnel. Upon the containment of the incident, the steps necessary to remove and eliminate components of the incident. To eradicate should be appropriate authorization, the steps to eradicate must be defined. Recovery mechanisms aim to restore the resource back to its normal state.
4. **Post-Incident Analysis** - 对安全事件进行学习总结。Organization should maintain an incident database with detailed information about the incident that occurred and how it was handled.若组织要与外界沟通事件的结果，应在沟通前先进行事件后分析。提前建立沟通指南以防向外界泄露事件相关敏感信息，应与IRT、法务、公关等部门讨论后在由授权人员和外界沟通。Post-incident analysis should include these at least: 5W.

##### Problem Management

- Determining the reasons as to why the incident occurred is the first step in problem management.
- Problem management is focused on improving the service and business operations.
- When the cause of an incident is unknown, there it is said to be a **problem**.
- The goal of problem management is to determine the root cause of incident and to eliminate it, to avoid the same issue be repeated again.
- two main critical success factors (CSFs) of problem management: 1to make sure that the same problem does not occur again; 2to minimize the adverse impacts of incidents and problems on the business.
- Problem Management Process Flow: incident notification->root cause analysis/RCA->solution determination(temporary workarounds or permanent fixes)->request for change->implment solution->monitor and report.


##### Change Management including Patch and Vulnerability Management

- Only authorized changes should be allowed and rogue unauthorized changes should be detected and addressed.
- Patching is a subset of change management.
- 补丁管理时要确保补丁在模拟测试环境中充分测试，确保补丁不会和已有软件冲突，没有兼容问题等。保证不会对生产业务造成影响。
- 漏洞的修复方式（安装补丁、修改配置、删除软件）。对于人员威胁的防御方法是安全意识培训和教育。
- 应尽快完成漏洞或补丁管理过程。

##### Backup, Recovery and Archiving

- backups, recovery and archiving assure the business continuity.
- In addition to regularly scheduled backups, when patches and software updates are made,it is advisable to perform a full backup of the system that is being changed. It is also crucial that the integrity and restorability of the backup.
- Recovery procedures must be controlled. Only those with need-to-know privileges should be authorized to retrieve and restore backups.
- 归档文档也要保证其完整性，保存时间要符合相关规定，到期后使用安全的方式对其进行处理。

### Disposal

#### End-of-Life Policies

- The first requirement in secure disposal of software and its related data and documents is that there is an End-of-Life (EOL) policy that is established.
- The EOL policy must provide the conditions in which systems and software must be securely disposed and provide guidance on how to accomplish this objective.

#### Sun-Setting Criteria

- It provide guidance as to when a particular product must be disposed or replaced. some criteria...

#### Sun-setting Processes

- Organization should establish appropriate EOL processes that is compliance with EOL policy.

#### Information Disposal and Media Sanitization

- Information is primarily stored in the two types of media: Hardcopy or physical representation of information(纸); Softcopy or electronic representation of information(disk, rom..).
- Some most common means of media sanitization:
    - **Disposal**/任意处理 is the act of discarding media without giving any considerations to sanitization.
    - **Clearing** is the process of sanitizing media by using software or hardware products that overwrite logical (e.g., file allocation tables) and addressable storage space on the media with non-sensitive random data.
    - **Purging** is the process of sanitizing media by rendering the data into an unrecoverable state. degaussing/消磁
    - **Destroying** is the process of ensuring that the media can no longer be reused as originally intended and the recovery of data from the media is virtually impossible or prohibitively costly. Techniques that can be used for physically destroying media:
        - **Disintegration**/瓦解 is the act of separating the media into component parts.
        - **Pulverization**/粉碎 is the act of grinding the media into a power or dust.
        - **Melting**/融化 is the act of changing the state of the media from a solid into liquid by using an extreme application of heat.
        - **Incineration or Burning**/焚烧 is the act of completely burning the media into ashes.
        - **Shredding**/碎片 is the act of cutting or tearing the media into small particles.
- *NIST sp 800-88 the Guidelines for Media Sanitization* illustrates the data sanitization and decision flow.

## Supply Chain and Software Acquisition

### Software Acquisition and the Supply Chain

- Security requirements should explicitly state prior, and it must be verified as well.
- Constituents of a software supply chain include the *products*, *processes* and the *people*.

#### Acquisition Lifecycle

- **Planing** - conducting an initial risk assessment to determine the functional and assurance needs
- **Contracting** - 
- **Development & Testing** - involves the implementation of reliable, resilient and recoverable code and attestation of security controls
- **Acceptance** -  involves the defnition of acceptance criteria, verifcation and validation activities,
- **Delivery** - involves the establishment of code escrow agreements,
- **Deployment** -  involves the installation and confguration of the software,
- **Operations & Monitoring** - 
- **Retirement**

#### Software Acquisition Models and Benefts

- 通常获取软件的方法有: direct purchase, Original Equipment Manufacturer (OEM) licensing, partnering (alliance) with the software vendor, outsourcing and managed Services。主要还是外包。
- **Outsourcing** -
- **Managed Services**/托管服务 - 将资源密集型业务的运营和服务转移到专门从事此类运营或服务的经验丰富的公司的管理。这使得公司能够专注于其核心业务战略。如：software development and subscription services，vulnerability assessments and penetration testing

#### Supply Chain Software Goals

- Conformance – 确保软件符合一系列规范、标准和最佳实践。
- Trustworthiness – 确保软件没有引入恶意漏洞。
- Authenticity - 确保软件没有伪造、盗版或者违法任何知识产权。

#### Threats to Supply Chain Software

- Software supply chain attack result include: modification of software logic/file / inertion of additional logic/file into software.
- Product/Data Threats : 
- Processes/Flow Threats:
- People Threats :

### Software Supply Chain Risk Management (SCRM)

- Managing risks in the software supply chain includes the management of the risk arising from the supplier itself and their software development and delivery processes.

- Software supply chain controls must follow these security principles:
    - Least Privilege
    - Separation of Duties
    - Location Agnostic Protection
    - Code Inspection
    - Tamper Resistance and Evidence
    - Chain of Custody
- 可能安全责任最终还是在采购方，公司需确保在SLA中实施了恰当级别的合同和技术控制，并确保其有履行的能力。

#### Supplier Risk Assessment and Management

- In software supply chain, there are two primary kinds of relationships – *workfor-hire* (subcontracting or staff augmentation) and *licensing* relationships.

### Supplier Sourcing

- Supplier sourcing begins with the identification of suppliers that can create the products required by the acquirer. An evaluation include: their responses to solicitations, their security practices, how they protect intellectual property, their secure storage and transfer practices, their security track record in managing vulnerabilities and incidents, protection against malware. Once a supplier is identified then contractual controls need to be established.

#### Supplier Evaluation (Pre-Qualifcation Assessment)

- **Organization**
    - fnancial history
    - Competing/Conﬂicts of Interests and Foreign Ownership and Control or Inﬂuence (FOCI)
    - Compliance with Security Policies, Regulatory and Privacy Requirements
    - Service Level Agreements (SLAs)
    - Past Performance in Supporting Other Customers
- **People**
    - Personnel Security Knowledge, Experience and Training
- **Processes**
    - Security Development Lifecycle Processes
    - Security Track Record (Vulnerability/Patch Management Processes)
    
#### Response Evaluation

- request for proposal (RFP)
- request for information (RFI)
- request for quote (RFQ)

### Contractual Controls

- 写到合同中的要求才是有效的，在合同中详细描述相关要求：
- about disclaimer

#### Intellectual Property (IP) Ownership and Responsibilities

- Intellectual property (IP) is the creations of the mind, it include inventions, literary and artistic works, software programs, symbols, names, images, and designs that are used in commerce.
- The ownership of intellectual property and the responsibilities of the supplier and the acquirer in protecting it must be explicitly articulated in the contract agreements.

##### Types of Intellectual Property (IP)

- IP is primarily of two types (industrial protection and copyright).
- Industrial property: Innovative(Inventions (Patents), Trade Secret); Fair Competition(Trademark).
- Copyright: Literary&Artistic (Software Programs)
    
##### Licensing (Usage and Redistribution Terms)

- A software license is a legal instrument that governs the use and/or redistribution of software.
- The category of licenses can be based on the: Number, Time, Functionality, Temitory.
- Software be grouped into the following categories based on its accessibility to source code: Closed source(OEM, Off-the-shelf); Open source(Permissive, Copyleft).

### Software Development and Testing

- 恶意人员可以在开发测试阶段访问源码并引入恶意逻辑和代码。所以要保证以下控制措施安全实施：

#### Assurance Requirement Conformance Validation

- Acquirers must mandate that the suppliers identify and describe the evidence of controls they build in to the software.
- 供应商应能够证明其工作内容与购买者要求的相符。可以通过回归测试、渗透测试、C&A等来验证。assurance不仅是确保软件没有defects，更是要证明存在的安全控制和组件能够有效的缓解安全威胁。供应商应能提供证据证明其保证声明。

#### Code Review

- Security code review can validate and verify the integrity of the software code, components and configurations, in a software supply chain.
- It can inspect to detect the presence of vulnerable and exploitable coding patterns, such as lack of input validation, lack of output encoding, dynamic construction of queries, direct parameter manipulation references, use of insecure APIs, non-malicious maintenance hooks, etc.
- It is useful in detecting the presence of malicious code and logic that is implanted by a threat agent.
- it is imperative that automated code reviews are performed in conjunction with manual code reviews.

#### Code Repository Security

- the software code, components and configurations must be restricted to ensure that only authorized changes can be made to the code. 
- Developers should have access only to the version of code necessary to complete their responsibilities for only the time period that they need to complete their operation. least privilege & need to know
- 任何代码更改能被跟踪，并识别是谁做的修改，以便能够进行审计和问责。
- 代码中的功能必须和指定需求对应，并且代码的更改应该在requirements traceability matrix (RTM)中可以被跟踪。代码的更改都需要有正式的审批流程，有日志记录和变更过程记录，以便日后可以进行审计和分析。
- 除了对源代码的访问控制，代码容器的服务端也要恰当的保护。
- 要严格控制有源代码的测试系统，只有授权人员被授予对这些测试系统的访问权。
- 变更和配置管理可被跟踪，确保修复的bug不会再写到代码中。维护代码资产列表，。

#### Build Tools and Environment Integrity

- The build environment should only have a limited number of owners and actions on build scripts that are used for automation purposes, should be also tracked and maintain within a secure code repository./编译环境只有授权者才能访问，软件编译活动过程可被跟踪。

#### Testing for Code Security

- It is advisable to create a library of tests that can be run after each hand-off of the software by the suppliers in the supply chain.
- Security testing tools: Static Source Code Analyzers(Fortify), Static Byte Code Scanners(FindBugs), Static Binary Code Scanners(IDA Pro, Veracode), Dynamic Vulnerability Scanning Tools(Nessus, BurpSuite), Malware Detection and Combat Tools(MBSA), Security Compliance Validation Tools(PCI DSS Self-Assessment Questionnaire (SAQ))

### Software SCRM during Acceptance

- Prior to acceptance, it is vital to verify the supplier claims and attest the existence and effectiveness of the security controls in the software.

#### Anti-Tampering Resistance and Controls

- 当软件在供应链中发布和传播时，要确保其不被篡改，或者篡改后也能恢复。这可以使用哈希或签名算法。

#### Authenticity and Anti-Counterfeiting Controls

- Authenticity and anti-counterfeiting controls are one of the most important elements of software assurance in a supply chain. We can use these techniques: code signing, license-checking technologies and online product registration, a “whitelist” of software applications.

#### Supplier Claims Verifcation

- Always verify supplier's claims. first determining if there are any known vulnerabilities. We can use: disclosure lists and security bug tracking lists, black box testing, reverse engineering the object code.
- 确保供应商的声明确实存在且有效。

### Software SCRM during Delivery (Handover)

#### Chain of Custody

- It is extremely important to make sure that the chain of custody is controlled, until the software reaches the final user or acquirer of the software. It means that each change to the software and handoff is *authorized*, *transparent* and *verifiable*.

#### Secure Transfer

- The code is transferred and exchanged security, the proposal is using session encryption and end-to-end authentication, e.g: TLS, IPSec.

#### Code Escrows

#### Export Control and Foreign Trade Data Regulations Compliance

- 出口软件/数据时应符合相关监管要求。

### Software SCRM during Deployment (Installation/Confguration)

- Firstly, Operational Readiness Reviews (ORR), include:

#### Secure Confguration

- it must be configured to be secure by default and secure in deployment. 

#### Perimeter (Network) Security Controls

- it is important to ensure that unauthorized individuals are cannot tap into a supplier’s network and tamper the software. We can use firewalls, secure communications protocols...

#### System-of-Systems (SoS) Security

- All suppliers of SoS must implment secure development process.
- input validate
- Testing the interfaces and interdependencies between components in an SoS

### Software SCRM during Operations and Maintenance

#### Runtime Integrity Assurance

- code signing also provides runtime permissions to the code at runtime, when the code is trusted and so it functions as a runtime integrity control as well.
- Trusted Platform Module (TPM) can provide runtime integrity verifcation. it can be used in conjunction with signed code.

#### Patching and Upgrades

- To address vulnerabilities by patching (updating) the software with hotfixes or upgrading to a version that is more secure.
- Each supplier should have a formal path management process to track, manage and resolve vulnerabilities in a timely manner.
- a reputable and secure update process: update notifications prior to patching, a secure repository from where to get the patch, publication of valid checksums and hashes for verification after patching, publication of test validation suites to determine the effectiveness of the patch, and a mechanism to report postpatching findings.

#### Termination Access Controls

- Staff should be revoked of any access to the software if they are terminated or if they change roles that do not require them to have continued access.

#### Custom Code Extensions Checks

- the custom code written to extend the existing functionality of the software also follows secure development practices.

#### Continuous Monitoring and Incident Management

- Periodic testing and evaluation of the software supply chain’s products, processes and people involved, is necessary to provide insight into the effectiveness of security controls that are planned, designed, implemented, deployed or inherited.
- Scanning (vulnerability, network, operating systems), penetration testing, and intrusion detection systems are useful to monitor the software and operational environment in a supply chain.

### Software SCRM during Retirement

- Retirement of software includes decommissioning of the software from operations, and also disposal of the data.
