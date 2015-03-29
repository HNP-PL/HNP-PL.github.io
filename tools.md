---
layout: page
title: Tools
permalink: /tools/
---

## Heisenberg ##

Most of popular code debuggers introduce modifications into debugged code. For example userland debuggers on Windows system must have their threads and processes (they create new kernel structures also visible in userland), they also often modify structure of segments and heap of loaded modules and TEB structure of analyzed threads (not to mention software breakpoints). Even among most withdrawn frameworks some of operating code is loaded into the debugee (e.g. kdcom.dll - kernel debugger code on target machine connected via COM interface, as used with WinDbg remote debugging sessions). The consequences of this vary from debugger detection to so called heisenbugs. Also, presence of software analysis tools can be detected by their behavior, e.g. using specific API or syscalls or accessing decoy resources.

The goal of Heisenberg project is to create a debugging framework for a whole operating system which will not be affected by these issues. Our base idea is to separate low-level debugging aspects such as physical memory or registers content from higher-level operating system abstraction (virtual memory, processes, etc.). Also, we are aiming at complete separation of debugee from debugger, i.e. debuggee to contain no additional components. The purpose of this approach is to eliminate any changes introduced by the debugger, which will prevent or hinder such events like debugger or virtualization detection, heisenbugs or probe effects from occurring. Finally, in accordance with the unix philosophy, we separate responsibilities of the tools being used. Also, we select open and free software over proprietary in order to conform Honeynet's fundamental rule of openness.

The architecture of Heisenberg framework we propose consists of whole system emulator Qemu which supports gdb_stub interface, attached Gdb debugger and a set of python scripts - Volatility - which will interpret low-level information (e.g. memory regions) into high-level OS objects (e.g. EPROCESS structures).

We decided to choose system emulator over virtualization engines, because this solution reflects our separation principles. We choose Qemu for it's support for wide range of architectures, processors and virtual hardware as well as good support for gdb_stub interface (to our knowledge: earliest and most developed implementation). We also consider Bochs machine as it's being prized for it's accuracy (even at the cost of emulation speed), but lack of support for wider range of architectures (especially mobile platforms) is a significant drawback. Also, Bochs internal debugger doesn't follow the principle of separation of responsibilities (though it's still useful in particular cases).

Source code and documentation is available on Bitbucket:

- [QEMU fork][heisenberg-qemu]
- [Volatility fork][heisenberg-volatility]


## Honeyspider Network ##

HSN is a system for detecting client-side attacks using multiple analyzers. The project was a joint venture between [NASK]/[CERT Polska], [National Cyber Security Center][ncsc.nl] (formerly GOVCERT.NL), and [SURFnet]. The goal was to develop a client honeypot system, based on existing state-of-the-art client honeypot solutions and a novel crawler application specially tailored for the bulk processing of URLs. This system focuses primarily on attacks against, or involving the use of, web browsers.

You can find much more information on the project's official website: [www.honeyspider.net][hsn]


## Honeyspider Network Capture-HPC NG ##

The original [Capture-HPC] was developed by Christian Seifert and Ramon Steenson of the New Zealand Chapter. It was adapted to the requirements of the HSN project, which resulted in about half of the code being rewritten. HSN Capture-HPC NG extends standard Capture-HPC functionality with features like listening for commands on TCP socket, support of [VirtualBox] and [KVM] via specially crafted scripts and extended logging.

Full list of changes:

- major changes to logging format (including flags to mark when urls stop processing)
- ability to work with VirtualBox / KVM (new revert scripts - only GNU/Linux versions)
- support to work with single-image virtual machines (one base-disk immutable image)
- several stability fixes
- removed several bugs (deadlocks, npes, etc.)
- case sensitivity of URLs added
- simplified configuration files
- logging via log4j
- broken zips handling (repairer added)
- uploading URLs both via file and socket
- exclusion lists reloading added (command send via socket)
- uploaded URL may have unique ID (changed format of output.log file to support URL ID)
- log/zip files created with a+r flags
- log directories created with a+rx flags

Source code of the project is available on [GitHub][github-capture].

HSN Capture-HPC NG is shipped with "stock" exclusion lists. To use Capture, the lists need to be modified and tailored to individual needs of a user.

Contributors (in alphabetical order):

- Paweł Jacewicz
- Jarosław Jantura
- Piotr Kijewski
- Paweł Krześniak
- Piotr Lewandowski
- Marcin Mielniczek

[heisenberg-qemu]: https://bitbucket.org/hnppl/heisenberg-qemu/
[heisenberg-volatility]: https://bitbucket.org/hnppl/heisenberg-volatility/
[nask]: http://www.nask.pl/
[cert polska]: http://www.cert.pl/
[ncsc.nl]: http://www.ncsc.nl/
[surfnet]: http://www.surf.nl/
[hsn]: http://www.honeyspider.net/
[capture-hpc]: http://www.honeynet.org/project/Capture-HPC
[virtualbox]: https://www.virtualbox.org/
[kvm]: http://www.linux-kvm.org/
[github-capture]: http://github.com/CERT-Polska/HSN-Capture-HPC-NG

