# PT2887-SS指纹识别器Linux驱动

这是PXAT/PixelAuth PT2887-SS（USB `2f0a:8020`）的libfprint驱动。它把模组接入Linux标准指纹栈；驱动提供注册、验证、识别和删除，并接入fprintd。驱动源码在[libfprint-pt2887](https://github.com/StarsEndX/libfprint-pt2887)。

## 现状

**已经可用。** 驱动已完成注册、验证、识别和删除，fprintd集成可用。

- 实验性；尚未合并上游libfprint
- 未完成：取消、拔插/重启的完整验收
- 不支持：安全会话/UKEYEX
- 非厂商官方项目

## 实现方式

协议来自Windows下USB流量的抓包分析。

通过抓包还原PXAT帧格式、槽位表和注册/验证状态机，驱动实现放在libfprint的下游fork中。驱动采用match-on-device：指纹模板留在模组芯片内，主机只保存槽位与用户/手指的映射，并以独立前缀部署，不替换系统libfprint。

---

# PT2887-SS Fingerprint Reader Linux Driver

This is a libfprint driver for the PXAT/PixelAuth PT2887-SS (USB `2f0a:8020`). It integrates the module with the standard Linux fingerprint stack; the driver supports enrollment, verification, identification, and deletion, and works with fprintd. Source: [libfprint-pt2887](https://github.com/StarsEndX/libfprint-pt2887).

## Status

**Usable.** Enrollment, verification, identification, and deletion are implemented, and fprintd integration works.

- Experimental; not yet merged into upstream libfprint
- Not vendor-official
- Pending: full acceptance for cancellation, replug, and restart
- Unsupported: secure session/UKEYEX

## Implementation

The protocol was recovered by capturing and analyzing USB traffic under Windows.

The capture analysis recovered the PXAT frame format, slot table, and enrollment/verification state machine. The driver lives in a downstream libfprint fork. It uses match-on-device: fingerprint templates stay in the module, and the host stores only the mapping between slots and users/fingers. It is deployed under a private prefix and does not replace the system libfprint.
