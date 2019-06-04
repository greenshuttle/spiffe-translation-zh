# 适合每个人的安全生产身份框架(SPIFFE)

## 备忘录状态

这个文档为开放社区指定了一个实验性的身份和身份发布标准，并且发起改进讨论和建议。这项工作正在进行中。可以无限制的分发本文档。

## 摘要

分布式设计模式和实践(如微服务、容器编排器和云计算)已经导致生产环境变得越来越动态和异构。传统的安全实践(例如只允许特定IP地址之间通信的网络策略)在这种复杂性下难以扩展。对于组织中的工作负载，需要一个一流的身份框架。

此外，现代开发人员需要理解和参与如何在生产环境中部署和管理应用程序。运维团队则需要对他们管理的应用程序有更大的可见性。随着安全标准的提高，我们必须为两个团队提供更好的工具，以便他们能够在构建安全的分布式应用程序中发挥积极的作用。

SPIFFE标准提供了一个框架规范，该框架能够跨越异构环境和组织边界引导和分发服务身份。

## 目录

1. 介绍
2. SPIFFE ID
3. SPIFFE可验证身份文档
4. 工作负载API
5. 总结

## 1. 介绍

SPIFFE标准包含三个主要组件——标准化身份命名空间，规定发布的身份可能以何种方式呈现和验证的方法，定义一个API端点，通过该API可以检索和或发布标识。这些组件分别称为SPIFFE ID、SPIFFE可验证身份文档(SVID)和Workload API。

虽然每个组件都有一个专用的规范，但是本文档的其余部分也会从较高的层次研究它们，并解释它们是如何组合在一起的。

## 2. SPIFFE ID

SPIFFE ID是一个结构化字符串（URI），用作实体的“名称”。虽然只是一个字符串，但它是构建其他所有内容的组件。它在[SPIFFE ID和可验证身份文档](https://github.com/spiffe/spiffe/blob/master/standards/SPIFFE-ID.md)规范中定义。

## 3. SPIFFE可验证身份文档

SPIFFE可验证身份文档（SVID）是一个携带SPIFFE ID的文档。 它相当于护照一样——文档可以证明持有者的身份。当然，与护照类似，它们必须能够抵抗伪造，并且必须明显该文档属于持有者。为了实现这一点，SVID包含加密属性，其允许 1)被证明是真实的，并且 2)被证明属于持有者。

SVID本身并不是具体文档类型。相反，我们定义 1)SVID所需的属性，以及 2)可以在各种现有文档类型中编码和验证SVID信息的方法。目前，唯一支持的文档类型是X.509证书。

SPIFFE SVID在[SPIFFE ID和可验证身份文档](https://github.com/spiffe/spiffe/blob/master/standards/SPIFFE-ID.md)规范中定义。X.509 SVID规范在[X.509 SPIFFE可验证身份文档中定义](https://github.com/spiffe/spiffe/blob/master/standards/X509-SVID.md)。

## 4. Workload API

SPIFFE Workload API是工作负载或计算进程获取其SVID的方法。它通常在本地公开（例如，通过Unix域套接字），并且明确地不包括来自工作负载的认证握手或认证令牌。实现者可以通过out-of-band方法验证Workload API调用者的真实性，例如检查调用操作系统提供的Unix域套接字的进程的属性。

除了为工作负载提供必要的SVID之外，Workload API还提供工作负载应该外部信任的CA包。这些CA包与发布的SVID之外的信任域相关联，并用于联合验证。

Workload API在[SPIFFE Workload API](https://github.com/spiffe/spiffe/blob/master/standards/SPIFFE_Workload_API.md)规范中定义，请参阅该文档以获取更多信息。

## 5. 总结

本文档从较高层面介绍了构成整个SPIFFE规范的各种组件。这些组件共同解决了现代异构环境中出现的身份验证和流量安全挑战，特别是那些高度动态的环境。有关更多详细信息，请参阅与感兴趣组件相关的规范。

##  附录A. SPIFFE规范清单

- [SPIFFE身份和可验证身份文档](https://github.com/spiffe/spiffe/blob/master/standards/SPIFFE-ID.md)
- [X.509 SPIFFE可验证身份文档](https://github.com/spiffe/spiffe/blob/master/standards/X509-SVID.md)
- [SPIFFE工作负载端点](https://github.com/spiffe/spiffe/blob/master/standards/SPIFFE_Workload_Endpoint.md)
- [SPIFFE Workload API](https://github.com/spiffe/spiffe/blob/master/standards/SPIFFE_Workload_API.md)