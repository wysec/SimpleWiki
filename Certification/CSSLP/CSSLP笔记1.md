## Secure Software Concepts

- 现在，要保障应用系统的安全，不仅需要确保软件程序的安全，还需要确保网络、主机系统等的安全。`安全是个整体`，应用系统的安全性依赖于最弱的部分。
- 普遍存在不安全软件的原因有：
	- 铁三角限制（如果软件开发时的scope、schedule/time、budget非常严格，则基本没有能力再考虑安全了）
	- 事后才考虑安全。//越早考虑安全越好。
	- 安全性与可用性的抉择
- 质量高的软件不代码安全高，安全高的软件将增加软件质量。
- 如何使软件安全？ 在软件开发生命周期的需求、设计、编码、发布和处置等阶段考虑安全（security concepts）。

### Core Security Concepts

- Confidentiality。不仅要确保数据的保密性，还要维护数据隐私。
- Integrity。1.确保传输、处理、存储的数据和最初一样;2.软件按预期可靠地运行。
- Availability。1.软件/数据只能被授权用户（who）访问;2.软件/数据在需要时（when）能被访问。
- Authentication。‘Are you whom you claim to be?’ 。认证时可以使用的三个因素：Knowledge、Ownership、Characteristic。重要系统或敏感信息的访问建议使用多因素认证。
- Authorization。根据主体的权限，控制对客体的访问。
- Accountability and Non-repudiation。
	- 审计内容至少包括：who（subject）、what(CRUD)、where(object)、when(timestamp)。
	- 对所有特权/管理操作，或者关键事务的信息变化前后要有日志记录。
	- 新的日志只能附加，不能覆盖旧日志。
	- 日志保存时间必须满足合规要求或者组织的策略要求。
	- Auditing is a detective control and it can be a deterrent control as well.
	- 记日志时要注意：1性能的影响（只记重要操作）；2.记录信息太多（日志分类，如： ‘Informational Only’, ‘Administrative’, ‘Business Critical’, ‘Error’, ‘Security’ and ‘Miscellaneous’：）；3.容量限制（容量计划，日志归档）；4.配置接口的保护（保护审计配置页）；5.日志的保护（日志不要记录敏感信息）。

### Design Security Concepts

安全设计原则（不可忽略的）：
- Least Privilege
- Separation of Duties / Compartmentalization Principle
- Defense in Depth / Layered Defense
- Fail Secure - 默认安全状态
- Economy of Mechanisms - 保持简单，减少攻击面
- Complete Mediation - 每次对每个客体的访问都要安全检查
- Open Design - 不依赖于隐秘的设计
- Least Common Mechanisms - 一个功能不能处理不同安全级别的任务
- Psychological Acceptability - 安全功能尽量对用户透明
- Weakest Link - 提高最弱部分的安全性
- Leveraging Existing Components - 使用已有安全的组件,不增加攻击面


### Risk Management

- One of the key aspects of managing security is risk management.
- 风险管理不仅是保护IT资产，更是要保护组织正常的业务执行，避免被中断。
- 风险管理过程包括：预评估、识别、开发、测试、实施、验证。
- 对软件安全的风险管理，是对保护IT资产和实施软件安全控制花费的平衡。因此应对风险进行恰当的处理。
- `风险管理贯穿整个SDLC`。
- 对所有资产都应恰当的评估损失风险。
- 漏洞可在*流程*、*设计*、*实施*过程中产生。
- 威胁可分为：*泄漏*、*更改*、*破坏*。
- 攻击者（attacker）利用漏洞（vulnerability）实现威胁（threat）导致风险（Risk）。
- Probability、Impact、Exposure Factor最终决定风险高低。
- 安全控制措施有：technical、administrative、physical方面。
-  Security controls can be broadly categorized into *countermeasures* and *safeguards*. 
- `将风险管理过程合并到软件开发生命周期中是降低软件整体风险最有效的办法`。
- *流程*、*人*、*技术*的风险都应恰当的考虑。
- 处理风险的方法：忽略风险、规避风险、迁移风险、接受风险、转移风险。

### Security Policies:

- 安全策略不仅仅只是文档，它指明需要保护的数字资产。安全策略识别组织的目标。安全策略帮助确保组织遵从合规要求。
- 安全策略范围：The scope of the information security policy may be organizational or functional.
- 安全策略开发的前提：管理层要支持，与相关方要充分沟通，所有人都被恰当教育。
- 安全策略开发过程：安全策略要周期的进行审查，持续监控，识别不合适的内容并进行修订。

### Security Standards

- High level security policies are supported by more detailed security standards。
- 安全标准类型：内部（coding standards），外部（Industry、Government、International、National）。
- 标准是强制的，guidelines不是。组织通常将外部标准作为指导，并设计为自己的标准，强制执行。
- SP 800-30: Risk Management Guide for IT
- SP 800-61 – Computer Security Incident Handling Guide
- SP 800-64: Security Considerations in the Information Systems Development Life Cycle
- SP 800-100: Information Security Handbook: A Guide for Managers
- ISO 27001/2 和 ISO 27005
- Payment Card Industry Data Security Standard (PCI DSS)
- Payment Application Data Security Standard (PA-DSS)
- 使用安全标准的好处：安全标准为构建和维护安全软件提供了通用和一致的基础。

### 最佳实践

- OWASP
- ITIL

### 软件开发方法

- Waterfall model、Iterative model、Spiral model、Agile development methodologies 

### 软件评估方法

- Socratic Methodology、Six Sigma、CMMI、OCTAVE、STRIDE and DREAD、OSSTMM、Flaw Hypothesis Method

### 企业应用和安全框架

- Zachman Framework、COBIT、COSO、SABSA

### 法规、隐私、合规

- SOX、BASEL II、GLB Act、HIPAA、GDPR、Computer Misuse Act、Mobile Device Privacy Act
- 隐私要求在开发安全且合规的软件时是重要的。
- 隐私需要考虑数据隐私和业务支持。
- 数据分类帮助识别需要隐私保护的数据，和控制措施。
- 数据隐私保护的建议：不需要的数据不要收集；只收集需要的数据，且获得用户同意；告知用户对其数据的处理方式并获得同意，且按此方式执行；
- 数据匿名化是移除其中个人信息的过程，可以使用的技术：Replacement/替换、Suppression/模糊化（省略部分信息）、Generalization（信息不具体）、Pertubation/随机化（对信息进行随机修改）。
- 匿名化的数据不可能与个人信息建立关联。
- 虽然数据匿名化可以确保隐私，但攻击者仍可能进行推理攻击，通过收集的信息进行聚合和关联匿名数据分析获得用户信息。
- 对于不再使用的敏感信息也要有恰当的安全控制措施（技术、管理、物理等方面），对于有敏感数据的介质的销毁可参考7章。

### 可信计算


## Secure Software Requirements

- 安全软件有这些质量属性的特征：Reliability（软件功能按预期执行）、Resiliency（不违背任何安全策略且能承受攻击或事故）、Recoverability（恢复到业务预期状态）。
- 将安全需求合并到软件需求收集和设计阶段是非常重要的，对软件的以上3点。
- 在软件需求规格文档中明确安全需求是非常重要的。

### 安全需求来源

- 内部来源：1.组织源（组织需要遵守的）：plicies,standards,guidelines,patterns and practices；2.业务功能源，业务要求->功能规格->安全需求。
- 外部来源：regulations,compliance initiatives,geographical requirements。
- 内、外部源的安全需求同样重要。
- Business owners决定接受风险等级，是风险的最终负责人。他需要被教育，让他认识到软件安全的重要性，以便更好的支持安全的工作。

### 安全需求类型

- 安全需求必需明确定义来处理公司目标，应该是可以测量的。全面的安全需求应包含核心安全的内容。
- 有这些类型的安全需求：
	- 核心安全需求（CIA+3A）
	- 一般要求（会话管理、错误&异常管理、配置参数管理）
	- 操作要求（部署环境、归档、隐私）
	- 其他要求（顺序和时间、国际、采购）

#### 核心安全要求
**Confdentiality Requirements**

- 保密性要求处理未授权的隐私或敏感信息泄漏问题。数据分类为非公共的适用于此要求。
- 保密性保护机制有：
	- Secret Writing/密写 -- Overt/公开的<Encryption、Hashing>，Covert/隐蔽的<Steganography、Digital Watermarking>;
	- Masking/掩蔽
- 整个信息生命周期都应定义清楚保密性要求，如获取、传输、处理、存储、销毁。
- 保密性要求可能会时间限制（如收购或合并信息），保密性要求需要基于数据分类。

**Integrity Requirements**

- 完整性主要确保软件的可靠性和防止为授权的修改。
- 防止对*软件*、*系统*、*数据*的修改的保护。
- 完整性保护保证可靠性，是指1系统或软件按照设计和预期运行；2确保维持系统和数据的准确性。
 完整性主要确保系统或数据的可靠性和准确性，还有系统或系统处理数据的完整completeness和一致性consistency。
- 完整性的安全控制措施有：输入验证、奇偶校验位检查、CRC、hashing。
- 主要是考虑系统和数据的reliability、accuracy、completeness、consistency方面。

**Availability Requirements**

- 明确可用性要求以确保不会对业务正常运营产生影响。防止对软件系统/数据被破坏。
- 应确定Maximum Tolerable Downtime(MTD)（允许软件不提供服务的最大时间）和Recovery Time Objective(RTO)（系统或软件从故障到恢复正常状态的时间） 在SLA中。
- Recovery Point Objective (RPO) also expressed in units of time is the maximum allowed data or productivity loss when the system becomes disrupted or down.
- 确定可用性需求的方法：1BIA分析软件停机时间的不利影响，2压力和性能测试。
- 实施BIA来判断对业务的不利影响可以是定量的（根据停机单位时间的损失、恢复正常的花费、罚款等），或定性的（损失信誉、信息、品牌声誉等）。
- 通过BIA来准确确定MTD和RTO。
- 应在软件需求文档中明确SLA的可用性需求（百分之多少个9）。
- 不要有单点故障点。负载均衡等都要在需求文档中明确。

**Authentication Requirements**

- Authentication requirements are those that verify and assure the legitimacy and validity of the identity that is presenting entity claims for verification.
- 建议利用已有或已被证明的认证机制和要求。
- 认证需求需要明确在软件需求文档中。
- 通常的认证方式有：
	- Anonymous - 公共可访问，不用凭证
	- [Digest Authentication](https://en.wikipedia.org/wiki/Digest_access_authentication) - 挑战/响应机制，发送凭证的hash，认证时比较hash值。
	- Integrated Authentication - NTML认证，or NT挑战/响应认证。可以单独使用，也可以和Kerberos v5认证结合使用。
    - Client Certificate-Based Authentication - 使用数字证书（ITU X.509 v3），常在Internet/ecommerce中使用。
    - Forms Authentication - 用户提供username和password来进行认证。
    - Token-Based Authentication - 结合Forms认证，如用在SSO。
    - Smart Cards-Based Authentication - 提供用户ownership进行认证，使用嵌入式芯片保存身份凭证。OTP提供最大强度的认证安全。
    - Biometric Authentication - 使用生物特征作为身份凭证。最初登记的生物信息可能后面不再有效会对合法用户导致DoS，另外不能远程访问使用。
    - Type I error/FRR等于Type II error/FAR是CER。CER应比较低。

**Authorization Requirements**

- Authorization requirements are those that confirm that an authenticated entity has the needed rights and privileges to access and perform actions on a requested resource. 
- 确定授权要求，首要的是识别主体/subjects和客体/objects。及主体对客体的行为（CRUD）。
- 访问控制模型有：
	- Discretionary Access Control (DAC) - 基于主体的身份/属于的组决定其权限，主体权限可自主传给其他主体。有基于身份的访问控制和基于角色的访问控制（更好）两种实现方式。[ACL](https://en.wikipedia.org/wiki/Access_control_list)也是常见的DAC实施方式。
	- Non-Discretionary Access Control (NDAC) - 系统安全策略或机制由系统/安全管理员来执行且防篡改，不依赖于主体的控制。
	- Mandatory Access Control (MAC) - 根据主体的clearance levels和匹配的客体的sensitivity labels来进行访问控制。提供多级安全。根据主体和客体来决定是否能访问。rule-based access control是常见的实施示例
	- Role-Based Access Control (RBAC) - 主体访问客体资源基于其被分配的角色。RBAC可以在DAC、NDAC、MAC中实施。但不是基于多级安全需求的。支持最小权限和职责分离。
		- Role Hierarchies
		- Roles and Groups ～ 不同：组是用户集而不是权限集；组中权限可以被分给用户或组；
	- Resource-Based Access Control，可分为：
		- Impersonation and Delegation Model
		- Trusted Subsystem Model

**Accountability Requirements**

- Accountability requirements帮助建立用户行为的历史记录，审计记录（audit trails）可以帮助检测未授权用户的操作或者授权用户的未授权操作。审计要求不仅可帮助取证调查，还可以帮助进行问题定位。
- 日志内容应至少包含这些内容：主体身份（who）、行为（what）、客体（where）、时间（when）。
- 日志中记什么不记什么由业务管理者决定。最佳实践是，所有重要的业务操作（修改商品价格、修改客户账户信息...）和管理操作（身份认证、创建管理员用户、修改软件配置...）应该被识别并进行审计。

#### General Requirements
**会话管理需求**

- 在认证成功后，分配给用户会话标识符/session identifier(ID)，使用此session ID来跟踪用户行为和维护认证状态，直到此会话被抛弃或者认证状态变为非认证状态。

**错误&异常管理需求**

- 错误信息和未处理的异常可能泄露应用内部架构、设计和配置信息。
- 使用简洁的错误信息和结构化的异常处理是个好方法。

**配置参数管理需求**

- 识别和捕获配置设置是非常重要的，确保其在软件设计、开发、部署时候都考虑了安全保护等级。

**Operational Requirements**

**部署环境需求**

- 考虑具体环境情况、合规要求

**Archiving Requirements**

- 数据归档时相关信息（如：时间）要明确。要符合监管规范要求。

**Anti-Piracy Requirements**

- 反盗版保护需求，如：代码混淆、代码签名、防篡改、证书、IP保护等。

#### Other Requirements

**Sequencing and Timing Requirements**

- 此问题可导致race conditions或Time of Check/Time of Use (TOC/TOU) 攻击。

**International Requirements**

- 主要是法律和技术方面：

**Procurement Requirements**

- 采购软件时也要确定要符合的安全需求，将安全需求包含到合同和SLAs中。

### Protection Needs Elicitation (PNE)

- 发现并确定安全需求就是PNE。
- 要使PNE活动有效和准确，和负责人的有效沟通和合作是非常重要的。
- PNE开始从发现需要保护的防止被未授权用户和未授权访问的资产。
- PNE的实施步骤...（来自IATF）
- 实施PNE的几个方法：
	- Brainstorming - 快速但不可信的方式获得安全需求。缺点：易忽略关键点；较强主观性。
	- Surveys (Questionnaires and Interviews) - 收集需求的效果和提的问题有关系，最好是开放问题，开发问题很重要。提问者和回答者的沟通交互也非常重要。
	- Policy Decomposition - 对于组织策略、外部法规、隐私和合规要求等，需要被分解为详细的具体的安全需求。要确保分解过程是客观的。将high-level需求分解为high-level目标，然后将其分解成安全需求。
	- Data Classification - 在软件保障中，数据/信息被认为是组织最重要的资产。
		- Types of Data ~ 数据可以被分为*结构化数据*和*非结构化数据*。
		- Labeling ~ 数据分类是有意地为信息/数据资产分配标签（重要等级），根据其被泄露、更改、破坏时基于CIA的影响。数据分类主要目标是降低数据保护的花费并最大化数据保护的投资回报。使安全控制和相应等级对应。
		- Data Ownership and Roles ~ 由business owner决定谁能访问，访问什么级别内容。他是data owner。
		- Data Lifecycle Management (DLM) ~ DLM是一系列方法、过程、实践构成的策略来保护数据生命周期安全。数据恰当的分类才好采取恰当的控制措施，才能有效确定安全需求。
	- Subject-Object Matrix - 多个角色主体访问系统时，要清楚每个主体允许做什么，建立细粒度的主-客访问关系矩阵。它可以有效的帮助生成misuse cases。
	- Use Case & Misuse Case Modeling ~ use case是预计的操作行为，misuse case就是未计划的或意外的不好的行为（一般针对重要系统）。/用[Secure Quality Requirements Engineering(SQuaRE)](https://www.us-cert.gov/bsi/articles/best-practices/requirements-engineering/square-process)方法来产生安全需求。

### Requirements Traceability Matrix (RTM)

- 将安全需求加入到RTM中。

## Secure Software Design

### The Need for Secure Design

- 早点考虑设计安全，在设计阶段解决安全问题，可大大降低成本。此外，增加软件resilient and recoverable，提升软件质量，减少重新设计的问题、保持软件一致性，降低业务逻辑问题。
- 架构设计缺陷导致的问题是“flaws”；编码/实施导致的问题是“bugs”。逻辑缺陷是架构设计导致。

### Architecting Software with Core Security Concepts

#### Confdentiality Design

- 防泄漏可以使用*加密*和*掩码*技术。掩码可以在数据显示或打印时使用；确保数据传输或存储的保密性时主要使用加密技术。
- 主要加密技术包括：Overt（Encryption、Hashing），Covert（Steganography、Digital Watermarking）。
- 加密保护技术主要目标是确保攻击者破解花费的资源大于其破解后能获得的利益。这是选择加密技术的判断依据。通常这依赖key长度。
- 密钥整个生命周期（generation、exchange、storage、rotation、archiving、destruction）都需要被保护。如HSM，TPM。
- 密钥要定期更换。
- 如果数据以加密格式备份或归档，相应的加密密钥也应被归档处理。
- 对称加密算法，加密和解密使用相同密钥。优势：快速加密大量数据；缺点：密钥交换（out of band，增加攻击面）、可扩展性（密钥管理）、不能防抵赖（不能证明来源）。
- 一些对称加密算法密钥长度及其对应强度。

| Algorithm Name | Strength    | Key Size |
| -------------- | ----------- | -------- |
| DES            | Weak        | 56       |
| Skipjack       | Medium      | 80       |
| IDEA           | Strong      | 128      |
| Blowfsh        | Strong      | 128      |
| 3DES           | Strong      | 168      |
| Twofish        | Very strong | 256      |
| RC6            | Very strong | 256      |
| AES / Rijndael | Very strong | 256      |

- 非对称加密不仅提供了保密性，还能防抵赖。此外还提供access control, authentication, integrity assurance。
- 当前的数字证书标准是X.509 v3。
- 数字证书类型：Personal certifcates，Server certifcates，Extended Validation (EV) certifcates，Software Publisher certifcates。
- 先了解清楚要保护的敏感信息的业务要求，再根据情况选择合适的设计方案。

#### Integrity Design

- 完整性设计是确保没有对软件或数据进行未授权的修改。主要的技术有：hashing，referential integrity，resource locking，code signing. or digital signature。
- HAVAL哈希算法可产生变长的输出(128bits~256bits)；并且可用户指定轮数（3~5）。
- 一般情况下，哈希值越长则越安全。MD5已被认为不安全（SHA1也不安全）。
- 在关系型数据库管理系统（RDBMS）中数据完整性使用referential integrity。它使用主、外键来保证数据完整性。
- resource locking也可来确保数据或信息的完整性，它不允许两个并行操作同一对象。注意防止死锁。
- 设计是确保数据或信息不会被未授权的方式、或未授权的人/进程修改。

#### Availability Design

- 软件设计时的可用性技术有：Replication，Failover，Scalability。
- Replication通常是主从模式。又分为：Active/Active replication，在主、从节点同时更新；Active/Passive replication，先更新主，再更新备。在涉及数据复制时，要特别考虑数据完整性问题。
- 故障转移（Failover）是指从活动的事务性软件、服务器、系统、硬件组件、网络自动切换到备用（或冗余）系统。
- failover是自动的，switchover是手动的。
- 在软件解决方案的设计中，需要解决所有潜在的单点故障。
- 可伸缩性（scalability）是指系统或软件在不降低其功能或性能的情况下处理增加的工作量的能力。有两个针对可伸缩性的设计方法：
	- Vertical scaling/Scaling UP ~ additional resources are added to the existing node
	- Horizontal scaling/Scaling Out ~ additional resources are added to the existing node（注意数据完整性）

#### Authentication Design

- 认证设计时主要考虑多因素认证和单点登录（SSO）。多因素认证更安全；SSO简化凭证管理并提高用户体验，但被攻击可能导致更严重安全后果。

#### Authorization Design
- 根据需求实施授权类型。
- 在权衡决策性能与安全时，应谨慎，考虑安全性高于性能。
- 在授权时使用角色时，设计确保没有绕过职责分离原则的冲突角色。设计确保明确授予用户/资源需要的最小权限。
- RBAC是大多数应用使用的授权方式。
- 许多云应用软件和移动应用的授权设计时使用entitlement management。它是细粒度的访问控制。通过回答“谁有权（授权或允许）在经过身份验证后执行哪些操作？”来实施。
- 它在软件设计中的两种主要方式：1授权作为共享服务被应用调用做授权决策cloud；2授权被内建到组织发布的应用/软件中mobile。
- 授权管理服务（entitlement management）的好处：访问控制决策是集中的，并且策略的更改可以统一、通用并自动的应用到所有应用程序。缺点：服务的安全问题可能导致所有应用出问题。

#### Accountability Design

- Log data should include the ‘who’, ‘what’, ‘where’, and ‘when’ aspects of software operations
- It is advisable to **log by default** and to leverage the existing logging functionality within the software
- 最佳实践：日志只能新增，不能重写；设计时要考虑容量限制和要求；保留、存档和处置日志的设计决策不应与外部法规或内部要求相抵触。
- 敏感数据不能明文记录到日志中。
- 设计还应考虑日志的保护机制，以确保日志在法庭上也可被接受。
- 验证日志的完整性。审计结合其他安全控制是更好的。系统自动记录日志，不由用户定义。

### Architecting Software with Secure Design Principles

- 以下常见的不安全的设计问题：
	- improper implementation of least privilege,
	- software fails insecurely,
	- authentication mechanisms are easily bypassed,
	- security through obscurity,
	- improper error handling, 
	- weak input validation
- 以下是一些安全设计原则。

#### Least Privilege

- 软件设计是考虑最小权限，在发生破坏时能够有效控制破坏后果。need-to-know（eg：多个不同权限管理员代替一个超级管理员）；Modular programming，将整个程序分解成更小的单元或模块，每个模块只执行一个逻辑操作。
- 使用普通账户代替管理员账号（如sa，sysadmin）也可帮助实施最小权限。

#### Separation of Duties

- 职责分离：将完成的软件功能拆分为多个条件，所有这些条件都需要在操作完成之前得到满足。例如：
	- 加密密钥拆分并放在不同位置，提升安全性。设计时不仅考虑存放位置，还有保护机制。
	- 不允许开发人员review自己的代码。开发人员也不应有权限部署代码到生产环境。
- 如何架构正确，职责分离可以减少某人造成的破坏程度。若与审计一起实施，可以阻止内部欺诈。

#### Defense in Depth

- 深度防御，也叫分层防御。他有两方面原因：1软件的单个漏洞不会造成完全的影响；2对攻击者造成威慑。一些例子：
	- 使用输入验证、prepared statements/存储过程、不使用用户输入来进行动态查询，来防止注入攻击。
	- 使用安全域，根据软件或用户被授权的访问级别来决定其访问的域。

#### Fail Secure

- 确保软件在受到攻击时能可靠的（reliably）运行，并且能快速恢复（recoverable）到正常业务和安全状态，即使发生设计或开发失败的情况时。其目标是保持软件的弹性（resiliency）（CIA），以保证其默认是安全的状态。主要在可用性设计是考虑。
- 它支持secure by design, secure by default, and secure by deployment（SD3 initiative）。
- 一些例子：登录失败一定次数后，默认拒绝用户访问，锁定账号；明确处理错误和异常情况，不要使用原始的错误提示信息（错误信息没有敏感内容）。

#### Economy of Mechanisms

- 可用性和安全性的平衡是实施安全的挑战。 增加更多的功能会导致攻击面增加，更容易导致漏洞，这就违反了economy of mechanisms原则。
- 更简单的设计意味着程序容易被理解，降低攻击面，更少的薄弱环节。降低出现安全问题的机率。
- Economy of mechanism用外行的术语也被称为KISS原则（Keep It Simple Stupid），某些情况也被称为unnecessary complexity。modular programming也支持此原则。
- 一些例子：禁用不必要的功能；使用SSO等。

#### Complete Mediation

- 此原则规定对每次请求都要进行检查，以防止在后续请求中绕过权限控制或其他。
- 此原则不仅可以防御认证和保密性威胁，也可以处理完整性方面的威胁。
- 使用统一接口进行访问控制。对所有都进行安全检查。

#### Open Design

- 安全保护措施的实施应独立于设计本身，因此对设计的审查不会损害保护措施所提供的保护。特别是在加密机制中。
- 与此相反的是security through obscurity，其安全性依赖于对安全设计的隐藏，如果了解其安全设计，则其就失去了安全性。比如硬编码密钥，或数据库连接信息等敏感内容；web的隐藏字段。。
- Security through obscurity可以增加被攻击的难度，可提供defense in depth，但它不应单独使用并作为主要的安全机制。
- 使用经过公共审查，被证明、测试过的行业标准方案。

#### Least Common Mechanisms

- 比如，管理员和非管理员不共享使用函数、库等。分开使用各自的。

#### Psychological Acceptability

- 设计软件符合psychological acceptability原则的基本方面是其安全保护机制：1容易使用；2不会影响易用性；3对用户透明。（确保安全机制最大化发挥作用）
- 安全机制的使用不应增加用户额外的使用负担，不应增加用户访问资源的困难度。访问性和可用性应不受影响。

#### Weakest Link

- 设计时确保没有易受攻击的组件。
-  When software is designed with defense in depth, threats arising from weakest links and single points of failure are mitigated.

#### Leveraging Existing Components

...

#### Balancing Secure Design Principles


### Other Design Considerations

- 其他设计需要考虑的有：Interface design、Interconnectivity。

#### Interface Design

- **User Interface** - Clark and Wilson安全模型要求主体对客体的访问必须通过程序进行调解（mediate），不能直接主体-客体的访问。 User Interface (UI)可以作为用户和资源间的调解程序。如UI显示敏感信息，进行模糊化处理；通过数据库视图让用户访问数据等。通过UI可以对执行的重要/特权操作进行审计，增加发现内部威胁和欺诈的可能性。
- **Application Programming Interfaces (API)** - 要确保API的安全。特别是在云和社交应用中。
- **Security Management Interfaces (SMI)** - SMI指配置和管理软件安全的接口（如管理员接口、帐号创建/删除/修改、配置审计日志等）。需要重点对SMI的保护，明确其安全要求。一些推荐的保护措施：1避免远程连接和管理，要求管理员在本地登录；2实施传输保护（如SSL、IPSec）；3对接口有恰当的权限管理控制；4记录和审计对SMI的访问。
- **Out-of-Band Interface** - Out-of-Band管理接口允许管理员连接不活动或关闭状态的计算机。应确保只有授权人员或进程能访问这些接口和服务。
- **Log Interfaces** - 日志接口可配置打开或关闭，也可配置记录什么类型和级别的日志。重要的是设计对日志接口的访问控制以便没有未授权用户对其进行修改配置。另外建议不能对日志重写，只能附加；此外建议避免设计删除日志接口。

#### Interconnectivity


### Design Processes

- 当进行软件安全设计时，这些安全过程需要在软件开发的初始阶段实施：攻击面评估，威胁建模，控制措施识别和优先排序，文档记录。

#### Attack Surface Evaluation

- 软件的每个可访问功能都是攻击者可利用的潜在攻击向量。攻击面评估的目标就是确定软件中能导致弱点被利用和可能面临威胁的入口和出口点。攻击面评估常作为SDLC设计阶段的威胁建模工作的一部分。
- 当安全需求通过misuse-cases和subject-object矩阵确定时，软件的可攻击性或攻击风险的确定可在SDLC的需求阶段开始。在设计阶段，每个misuse-case和subject-object矩阵可被使用作为确定软件可被攻击的入口和出口点的输入。
- 攻击面评估会试图枚举攻击者可能会攻击的所有功能点，根据他们的严重程度对这些潜在攻击点分配权重值，以便识别控制措施和分配优先级。
- relative attack surface quotient (RASQ)  //p198
- 分解攻击表面为三个维度：targets and enablers、channels and protocols、access rights。

#### Threat Modeling

- 针对软件的威胁有很多。
- **Threat Sources/Agents**，可分为human（无知用户、有组织犯罪组织等）和non-human（virus、worm、spyware...）。
- 实施威胁模型的前提条件：1明确定义信息安全策略和标准；2了解监管和合规要求；3清晰定义和成熟的SDLC流程；有实施威胁模型的计划。
- 威胁模型可以根据情况选择执行。建议对遗留系统、应用接口、三方组件进行威胁建模。
- 在进行威胁模型前应确定安全目标（high level goals）。如防止数据泄露、保护知识产权、提供高可用性等。
- 威胁模型过程可分解为如下4个阶段：1Model Application Architecture，2Identify Threats，3Identify, Prioritize and Implement Controls，4Document and Validate。
- Model Application Architecture - 通过识别应用属性创建应用概况图。
	- Identify the Physical Topology，通过物理拓扑图识别应用在哪儿、怎样部署。如只在内部使用，还是在DMZ，或者在云上。
	- Identify the Logical Topology，1确定应用的组件、服务、协议和端口；2确定应用的身份认证方式。如基于表单的，基于证书的，基于令牌的，SSO、多因素等。
	- Identify Human and Non-Human Actors of the System，使用系统的角色类型。
	- Identify Data Elements，如产品信息、客户信息等。
	- Generate a Data Access Control Matrix，确定用户对数据元素的权限。权限包括CRUD。
- Identify Threats - 全面了解软件的架构可以帮助发现相关的威胁和漏洞。识别潜在的和合适的威胁的方法有：
	- Identify Trust Boundaries，边界帮助识别软件允许或不允许的行为活动。确定边界对于设计边界内合适的保护级别很重要。
	- Identify Entry Points，指接收用户输入的地方，每个入口点都可能是潜在的威胁源，因此所有入口点都需要明确识别到并采取保护措施。一般入口点有：搜索页、登录页、注册等。
	- Identify Exit Points，指显示信息的地方，它可能是信息泄露源，也需要同等级的保护。一般出口点有：搜索结果页，产品页等。
	- Identify Data Flows，DFD和sequence diagram帮助理解应用跨不同可信边界时怎样接收、处理数据。
	- Identify Privileged Functionality，识别允许提升特权或执行特权操作的功能是很重要的。所有管理功能和重要业务处理应被识别。
	- Introduce Mis-Actors，human（hacker, administrator..）和non-human（process, malware..）。
	- Determine Potential and Applicable Threats，识别能对资产造成危害的相关威胁。架构、开发、测试、运维、安全等所有人员都应参与。两个识别威胁和漏洞的方法：
		- Think Like an Attacker (Brainstorming和Using Attack Trees)，头脑风暴快速且简单，但不够科学，可能识别威胁不相关或没识别到；因此还需要使用攻击树。
		- Use a categorized threat list， 通常使用STRIDE，他考虑的是攻击者的目标。
- Identify, Prioritize and Implement Controls - 建议使用标准控制措施来缓解风险到可接受水平，否则应重新架构来消除威胁。一个或多个控制措施来缓解某个威胁。优先处理高风险的威胁。以下是确定威胁风险级别的方法：
	- Delphi Ranking，大概估计风险级别。评估标准常依据威胁可能导致的潜在影响。
	- Average Ranking，可使用DREAD框架，*Damage Potential*、*Reproducibility*、*Exploitability*、*Affected Users*、*Discoverability*对这些方面进行评估。计算最终威胁等级（D+R+E+A+D）/5。
	- Probability x Impact (P x I) ranking，**Risk = Probability of Occurrence X Business Impact**。它比其他更科学，结合DREAD框架后，Risk = (R + E + D) X (D + A)。
	- P x I的方法即考虑发生可能性，也考虑业务影响。方便设计人员灵活的考虑设计方案。并可更精确的计算风险值。
- Document and Validate - 由于威胁模型要随着项目周期不断迭代、更新和验证，因此需要对威胁模型有文档记录。通常可以是图标格式或文本格式，建议两者都有。文档中应详细记录威胁的属性、类型、控制措施等内容，建议先建立模板。最后还要对记录的威胁、控制、剩余风险等结果进行验证。

### Architectures

- 由于业务目标和技术随着时间的推移而变化，因此软件架构必须具有*战略性*（有长期的考虑，高内聚低耦合）、*整体性*（考虑IT、业务、干系人等）和*安全性*。
- 以下关于不同类型架构的软件如何进行安全的架构设计。

#### Mainframe Architecture

- 大型机可提供最高EAL5的安全等级。他有自己的网络基础架构，这增强了其固有的核心安全能力。
- 最初大型机在封闭网络的有限人员使用，而现在开放互联访问增加，这增加了其攻击面。另外专业人员减少也可能导致其处于在不安全状态。
- 对于存在的安全挑战，之前提到的安全控制措施建议使用。

#### Distributed Computing

- 趋势是从集中的大型机到远程访问，即分布式计算。他主要分为两类：Client/Server和Peer-to-Peer (P2P)。
- **Client/Server**，互联网是Client/Server的典型例子。普遍的架构是3层架构，表示层、业务逻辑层、数据层。
- **Peer-to-Peer (P2P)**，客户端和服务端是对等关系，管理这些资源在P2P网络中，他没有中心。
- 分布式计算环境的攻击面包括client和server，这些安全设计应重点考虑：
	- Channel Security，保护数据传输信道的安全，措施如：SSL、IPSec。
	- Data Confdentiality and Integrity，数据使用如encryption或hashing来防止泄漏和更改的威胁。
	- Security in the Call Stack/Flow，设计时考虑软件功能所有的调用，确保都有恰当的安全控制。
	- Security Zoning，client和server有安全边界，架构时这些可信级别应确定并恰当的处理。

#### Service Oriented Architecture

- SOA是一种分布式计算架构，他有这些特征：
	- Abstracted Business Functionality
	- Contract-Based Interfaces 
	- Platform Neutrality
	- Modularity and Reusability
	- Discoverability
	- Interoperability
- SOA可以使用这几种技术实现：Remoting using Remote Procedure Call(RPC)、Component Object Model(COM)、Distributed Component Object Model(DCOM)、Common Object Request Broker Architecture(CORBA)、Enterprise Service Bus(ESB)、Web services(WS)和REST。Java中可用Remote Method Invocation(RMI)API，Microsoft的Windows Communication Foundation(WCF)。另外RPC\COM\DCOM\CORBA都比较老了。
- Enterprise Service Bus (ESB)
- Web Services，平台中立，常基于XML，
- WS传输的信息会被拦截和篡改，可以使用WS-Security（XML加密XML签名），TLS。
- 身份、认证、访问控制来对资源进行保护，身份和认证可以使用token-based认证，SOAP authentication header，或transport layer authentication。
- Contract Negotiation/合约协商，使用Web Service Description Language(WSDL)，
- 主要的SOA可信模型：Pairwise Trust Model（两者可信）、Brokered Trust Model（独立三方作中间人）、Federated Trust Model、Proxy Trust Model。
- Representational State Transfer (REST)

#### Rich Internet Applications

- RIA中常用的框架是：AJAX、Abode Flash/Flex/AIR、Microsoft Silverlight、JavaFX。
- RIA中固有的安全控制机制有Same Origin Policy (SOP)和sandboxing。
- 为了预防其安全机制被绕过，设计时确保认证和访问控制的决定不依赖客户端检查；设计时还要考虑数据和服务的实际/真实来源。

#### Pervasive/Ubiquitous Computing

...
- 一些促进普适技术的技术：
	- Wireless networking and communications
	- Radio Frequency Identifcation (RFID)
	- Location Based Services (LBS)
	- Near Field Communications(NFC)
	- Sensor networks

#### Cloud Computing

#### Mobile Applications

#### Integration with Existing Architectures

- 与已有架构系统进行集成，可以减少重复工作，符合leveraging existing components原则。要注意向后兼容和保持安全性的问题，确保集成已有和新的架构不会降低安全保护控制的程度。

### Technologies

- 整体安全，包括人、过程、技术这三个组件。
- 推荐利用已有技术来提供业务功能。它可减少重复工作，且已证明的技术更有安全保证。

#### Authentication

- Security Support Provider Interface(SSPI)是IETF RFCs 2743和2744的实现，一般称着Generic Security Service API (GSSAPI)。 他抽象认证调用接口，开发者可以直接使用而不用理解其细节。他可以通过插件接口的方式与其他认证技术互通。

#### Identity Management

- IDM answers the questions, “Who or what is requesting access?”, “How are they or it authenticated?”, and “What level of access can be granted based on the security policy?”
- IDM生命周期包括：身份的提供（创建数字身份<自动化实现>）、管理(身份重命名，角色增加和删除，权限和角色建立关系..审计等)、取消（终止访问控制(TAC)过程<停用帐号>）。
- 一些IDM使用的常用技术：
	- Directories，目录是身份信息保存的容器，与认证集成，常使用的网络目录LDAP，目录是IDM的基础要求。
	- Metadirectories and Virtual Directories，用户角色和权限随着业务变更其身份和权限信息也睡着变化。通过metadirectories传播和同步身份变化从系统记录（HR、CRM、CD等系统）到管理系统。例子Microsoft Identity Lifecycle Management。
	- + 由于Metadirectories没有可调用的接口，在Identity Services-based架构中，virtual directories可提供调用的服务接口，可来获取身份数据和修改。virtual directories比metadirectories提供更多保证，他可作为gatekeeper来确保数据使用是授权和符合安全策略的。

#### Credential Management

- Credentials还有令牌、证书、指纹、虹膜等。Managing credentials包括其产生、存储、同步、重置、废除。
- Password Management，1密码有一定复杂度；2密码不能硬编码，哈希处理密码；3修改密码时要提供旧密码，密码被复制/同步到其他应用；4密码被恢复或重置时要确保是合法用户（通过回答问题）的请求；5密码有过期时间，只能用一次；5目录服务可用来实施密码策略和管理密码。
- Certifcate Management，[PKI](https://en.wikipedia.org/wiki/Public_key_infrastructure)...。除了使用PKI进行身份认证外，X.509证书还可以提供Privilege Management Infrastructure (PMI)来实现强大的授权功能。
- Single Sign On (SSO)，常与[Kerberos](https://en.wikipedia.org/wiki/Kerberos_(protocol))和[SAML](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language)结合使用。与SSO相关的概念是Federation，主要使用SAML2.0，FIDO。SSO要注意：实体间建立信任，单点问题，DoS，花费。

#### Flow Control

- 信息流相关的几个安全问题：1应用的敏感信息未授权显示给用户，2有恶意payload的网络流量进入网络。对信息或数据流进行恰当控制，可以有效缓解软件的相关威胁。实施安全策略控制信息如何流动；代码级安全保护。Firewalls and Proxies、Middleware、Queuing Infrastructure and Technology可以来控制信息跨信任边界的流动。
- Firewalls and Proxies，主要是网络层防火墙，分隔内外网络或者内部子网络。根据配置的规则或策略来限制网络流量。防火墙分为：packet filtering（无状态，使用ACL预定义的规则判断数据包是否能通过）、proxy（中断连接然后检查数据包）、stateful（可以维护状态和包数据上下文，a state table）、application layer firewall（工作在7层，提供数据流控制）。
- Middleware，中间件方便了软件间的通信流动。它可能成为单点故障点，DoS攻击的目标。
- Queuing Infrastructure and Technology，当发送数据和处理数据速度不一致时，防止网络拥塞。技术产品有：Microsoft Message Queuing (MSMQ)、Oracle Advance Queuing (AQ)、IBM MQ Series。

#### Auditing (Logging)

- 在进行任何处理前，最好在同步日志时钟后合并日志。要对日志进行保护。一些审计技术：
- Application Event Logs，注意确保日志记录一致并符合行业标准。建议所有安全事件都有日志记录。
- Syslog，使用syslog时使用tcp协议。cache servers。使用syslog时要确保使用加密通道（SSL，SSH）传输数据，并且使用哈希函数（SHA）确保完整性。用Syslog-NG。
- Intrusion Detection System (IDS)，检测内部威胁和欺诈活动。有：Signature-based（通过签名来检测威胁）、Anomaly-based（– 监控并比较网络流量与“正常”基线，存在偏差的就是异常的）、 Rule-based（基于程序化的规则检测攻击）。
- Intrusion Prevention System (IPS)，可以主动对异常行为采取阻断行为。

#### Data Loss Prevention (DLP)

- DLP防止敏感数据泄露。DLP brings both mandatory (labeling) and discretionary (based on discretion of the owner) security into effect。DLP常放在网关处。加密保护和访问控制（Chinese Wall）保护机制可以用来在SaaS中的数据泄露。

#### Virtualization

- 确保虚拟化的安全很重要。

#### Digital Rights Management (DRM)

- Rights Expression Language (REL)：Open Digital Rights Language (ODRL) 、eXtensible rights Markup Language (XrML)、Publishing Requirements for Industry Standard Metadata (PRISM) 

#### Trusted Computing

- Trusted Platform Module (TPM)，主要提供加密密钥生存和存储。可能遭受边信道攻击。
- Anti-Malware，

#### Database Security

- 数据库查询各种数据时要仔细设计以被审查、监控和审计。防止推理攻击和聚合攻击。Polyinstantiation、database encryption、normalization、triggers and views是重要的数据保护设计方案。
- Polyinstantiation，防御防止推理攻击和聚合攻击。存在多个数据实列，不同级别用户看到的不同。
- Database Encryption，数据加密可以防御数据泄露和篡改，但也需要确保对加密密钥/key有恰当的认证和访问控制保护机制。加密会影响性能和数据大小。数据库加密有两种方法：1.native DBMS加密 - Transparent Database Encryption (TDE)，对应用影响小；弱点：key保存在DBMS中，依赖DMBS访问控制保护机制的强度，性能影响大。2.外部加密资源加密 – 性能高，key保存在HSM增加了安全性；缺点，应用修改比较多。
- Normalization，组织数据，消除冗余和不一致性。数据库设计符合一定的要求：第一范式（1NF）、第二范式（2NF）、第三范式（3NF）...，确保数据完整性。缺点：影响性能。可以使用denormalizing（允许冗余数据），替代方案是用视图。 
- Triggers，对自动化和改进安全保护机制有用。注意点：过度使用triggers可导致应用复杂，难于维护，增大潜在攻击面。trigger中不能使用commit、rollback。最好不要用cascading triggers。
- Views，做好权限保护，可以隐藏数据库内部结构，并可重命名列名等
- Privilege Management，建议通过角色进行权限管理，

#### Programming Language Environment

- 选最熟悉的，流行的，新的语言。最好是强类型的。程序语言中不推荐自定义数据类型。Managed code，编译为中间语言，由runtime environment管理；unmanaged code，直接编译为机器码，直接在OS上执行。
- Common Language Runtime (CLR)，The managed runtime environment in the .NET Framework is the Common Language Runtime (CLR).
- Java Virtual Machine (JVM)，
- Compiler Switches，如/GS标志、StackGuard technology

#### Operating Systems

- Address Space Layout Randomization (ASLR)，每次程序运行时内存中随机化和移动函数入口地址。Windows和Linux都有。
- Data Execution Prevention (DEP)/Executable Space Protection (ESP)，标记数据段为不可执行，若检测到代码在不允许的地方执行，则中止程序。Windows DEP（硬件、软件技术），Unix or Linux ESP。
- code access security (CAS)，防止不可信源的代码执行特权操作，

#### Embedded Systems

- 注意内存管理（防篡改）、敏感数据保护（传输、存储、显示保护），防边信道攻击、错误注入攻击、逆向，

### Secure Design and Architecture Review

- 软件设计完成后，最后review安全设计和架构，确保都满足安全要求，对发现的问题尽早修复。此审核要考虑安全策略和运行的目标环境。审核应覆盖整个范围，包括主机、网络等层面的保护。特别注意安全设计原则和核心安全概念的情况。此外还应对架构进行逐层分析，以便实施深度防御。
