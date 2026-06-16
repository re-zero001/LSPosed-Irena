# LSPosed Framework

[![Build](https://img.shields.io/github/actions/workflow/status/re-zero001/LSPosed-Irena/core.yml?branch=dev&event=push&logo=github&label=Build)](https://github.com/re-zero001/LSPosed-Irena/actions/workflows/core.yml?query=event%3Apush+branch%3Adev+is%3Acompleted) [![Channel](https://img.shields.io/badge/Follow-Telegram-blue.svg?logo=telegram)](https://t.me/lsposed-irena) [![Download](https://img.shields.io/github/v/release/LSPosed/LSPosed?color=orange&logoColor=orange&label=Download&logo=DocuSign)](https://github.com/re-zero001/LSPosed-Irena/releases/latest) [![Total](https://shields.io/github/downloads/LSPosed/LSPosed/total?logo=Bookmeter&label=Counts&logoColor=yellow&color=yellow)](https://github.com/LSPosed/LSPosed/releases)

## Introduction 

A Zygisk module trying to provide an ART hooking framework which delivers consistent APIs with the OG Xposed, leveraging LSPlant hooking framework.

> Xposed is a framework for modules that can change the behavior of the system and apps without touching any APKs. That's great because it means that modules can work for different versions and even ROMs without any changes (as long as the original code was not changed too much). It's also easy to undo. As all changes are done in the memory, you just need to deactivate the module and reboot to get your original system back. There are many other advantages, but here is just one more: multiple modules can do changes to the same part of the system or app. With modified APKs, you have to choose one. No way to combine them, unless the author builds multiple APKs with different combinations.

## Supported Versions

Android 8.1 ~ 16

## Install

1. Install Magisk v26+
2. Install [ZygiskNext](https://github.com/Dr-TSNG/ZygiskNext/releases)
> Or enable zygisk in magisk, we recommend use ZygiskNext.
3. [Download](#download) and install LSPosed in Magisk app
4. Reboot
5. Open LSPosed manager from notification
> Or install manager.apk in zip file.
6. Have fun :)

## Download

- Go to telegram: [@lsposed-irena](https://t.me/s/lsposed_irena)
- For canary build, please check [Github Actions](https://github.com/re-zero001/LSPosed-Irena/actions/workflows/core.yml?query=branch%3Adev)

## Get Help

**Only bug reports from **THE LATEST DEBUG BUILD** will be accepted.**
- GitHub issues: [Issues](https://github.com/re-zero001/LSPosed-Irena/issues/)
- (For Chinese speakers) 本项目只接受英语**标题**的issue。如果您不懂英语，请使用[翻译工具](https://www.deepl.com/zh/translator)

## For Developers

Developers are welcome to write Xposed modules with hooks based on LSPosed Framework. A module based on LSPosed framework is fully compatible with the original Xposed Framework, and vice versa, a Xposed Framework-based module will work well with LSPosed framework too.

- [Xposed Framework API](https://api.xposed.info/)

We use our own module repository. We welcome developers to submit modules to our repository, and then modules can be downloaded in LSPosed.

- [LSPosed Module Repository](https://github.com/Xposed-Modules-Repo)

## Community Discussion

This fork won't have.

## Credits 

- [Magisk](https://github.com/topjohnwu/Magisk/): makes all these possible
- [ZygiskNext](https://github.com/Dr-TSNG/ZygiskNext): provides a way to inject code into zygote process
- [XposedBridge](https://github.com/rovo89/XposedBridge): the OG Xposed framework APIs
- [Dobby](https://github.com/re-zero001/Dobby): used for inline hooking
- [LSPlant](https://github.com/LSPosed/LSPlant): the core ART hooking framework
- [LSPosed](https://github.com/LSPosed/LSPosed): fork source
- [EdXposed](https://github.com/ElderDrivers/EdXposed): LSPosed fork source
- [xz_embedded](https://github.com/tukaani-project/xz-embedded):decompress debug_info section into stripped libraries
- [system_properties](https://github.com/topjohnwu/system_properties):switch properties access within LSPosed
- [riscv64-inline-hook](https://github.com/eirv/riscv64-inline-hook): inline hooker for `RISC-V 64`
- ~[SandHook](https://github.com/ganyao114/SandHook/): ART hooking framework for SandHook variant~
- ~[YAHFA](https://github.com/rk700/YAHFA): previous ART hooking framework~
- ~[dexmaker](https://github.com/linkedin/dexmaker) and [dalvikdx](https://github.com/JakeWharton/dalvik-dx): to dynamically generate YAHFA hooker classes~
- ~[DexBuilder](https://github.com/LSPosed/DexBuilder): to dynamically generate YAHFA hooker classes~

## License

LSPosed is licensed under the **GNU General Public License v3 (GPL-3)** (http://www.gnu.org/copyleft/gpl.html).
