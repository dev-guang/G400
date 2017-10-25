# G400 EFI

> G400 安装 macOS 的 EFI 文件。

![](https://ws2.sinaimg.cn/large/006tNc79gy1fkpyp60mnuj30ga09ugo2.jpg)

### 基本情况

- [x] 集成显卡 HD4K；
- [x] 屏蔽独立显卡 AMD8570M（DSDT + SSDT-Disable_DGPU）；
- [x] 有线网卡与无线网卡（BCM4322）；
- [x] 声卡驱动（CX20757）+ 麦克风无解（AppleALC）；
- [x] DSDT 与 SSDT（x8,、x13、x18、 x19、 x24）；
- [x] 睡眠唤醒；



### 完善

#### DSDT

1. 添加屏蔽独显的代码段；
2. 添加补丁：DTGP、HD4K GFX、[igpu Brightness fix (HD3000/HD4000)、HDEF、IRQs，注入显卡信息和声卡 ID；

#### SSDT

*使用 ssdtPRGen 生成，并做如下调整：*

```markdown
baseFrequency: 1200 -> 700
frequency: 2400 -> 1700
# (1700 - 700)/10
turboStates: 0 -> 10
Name (APLF, 0x05) -> Name (APLF, 0x01)
# 10 + 1
Name (APSN, Zero) -> Name (APSN, 0x0B)
```



**参考**

- [【教程】 UEFI+GPT+Clover Dual System Guide.](http://bbs.pcbeta.com/forum.php?mod=viewthread&tid=1443155)
- https://github.com/RehabMan/OS-X-Clover-Laptop-Config
- https://github.com/vit9696/AppleALC
- https://github.com/vit9696/Lilu/blob/master/KnownPlugins.md
- https://github.com/Piker-Alpha/ssdtPRGen.sh
- [利用ssdtPRGen.sh生成适合的处理器的变频配置文件](http://bbs.pcbeta.com/viewthread-1585347-1-1.html)
- [IVY CPU 频率只有2档？小二，再加多7档！不支持睿频的可以试下！](http://bbs.pcbeta.com/viewthread-1490196-1-1.html)
- [惠普g4-2216tx 成功dsdt驱动电池和dsdt屏蔽屏蔽ATI独显](http://bbs.pcbeta.com/viewthread-1444322-1-1.html)