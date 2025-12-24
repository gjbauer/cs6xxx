# **Graduate Course Syllabus: Advanced Systems Security - Hardware/Software Co-Design**

**Course Number:** CS 6XXX/7XXX
**Term:** Fall 2024
**Credits:** 3
**Prerequisites:** Operating Systems, Computer Architecture, or instructor consent. Familiarity with C/C++ and assembly required.

---

## **Course Description**

This graduate seminar explores the co-evolution of hardware and software security mechanisms, from foundational memory safety principles to cutting-edge architectural mitigations. We will analyze the historical context of vulnerabilities, examine deployed mitigations, and critically evaluate emerging hardware security features—with particular focus on the ARM64 architecture. The course blends systems security, computer architecture, and practical exploit/mitigation analysis through hands-on labs, paper discussions, and a substantial research or implementation project.

## **Learning Objectives**

Upon successful completion, students will be able to:
1. Analyze the security implications of processor microarchitecture and ISA design choices.
2. Implement and bypass software-based security mitigations (ASLR, CFI, sandboxing).
3. Evaluate hardware security extensions (PAC, MTE, CET, SMAP) in realistic threat models.
4. Design and analyze secure memory management practices for sensitive data.
5. Understand speculative execution attacks and side-channel fundamentals.
6. Conduct original research or implement advanced security mechanisms.

## **Required Texts & Materials**

* **Architecture Manuals:** ARM Architecture Reference Manual for AArch64
* **Research Papers:** Provided weekly via course website
* **Software:** QEMU with ARM64 emulation, GCC/clang with security flags, GDB, custom lab environments

## **Grading**

* Research/Implementation Project: 35%
* Lab Assignments (4): 30%
* Paper Presentations & Participation: 20%
* Final Exam: 15%

---

## **16-Week Schedule**

### **Part I: Foundations & Software Mitigations**

**Week 1: Course Overview & The Memory Safety Crisis**
* Historical context: Morris Worm to modern exploits
* Memory corruption primitives: buffer overflows, use-after-free, double-free
* **Lab 1 released:** Basic stack/heap exploitation on deprecated system

**Week 2: Software Mitigations 1: Spatial Memory Safety**
* Stack canaries, non-executable (NX/XD) memory, ASLR
* Limitations and bypass techniques (info leaks, partial overwrites)
* **Reading:** "On the Effectiveness of Address-Space Randomization"

**Week 3: Software Mitigations 2: Control-Flow Integrity**
* Forward/backward edge protection, shadow stacks
* Software CFI implementations (Clang CFI, Microsoft CFG)
* Performance-security tradeoffs
* **Reading:** "Control-Flow Integrity: Principles, Implementations, and Applications"

**Week 4: Isolation & Sandboxing**
* Principle of least privilege, system call filtering (seccomp, pledge)
* Process/container isolation, microkernels, capability systems
* Web browser sandboxes as case study
* **Lab 1 due; Lab 2 released:** Bypassing ASLR+DEP with ROP/JOP

**Week 5: Secure Memory Management Practices**
* Cryptographic memory wiping: challenges with compilers, caches, swap
* Zeroization standards (NIST, FIPS), `mlock`/`madvise` usage
* Memory allocator hardening (guard pages, randomized freelists)
* **Project proposals due**

### **Part II: Hardware-Assisted Security**

**Week 6: Hardware Security Primitives**
* Trusted Execution Environments (TEEs): SGX, TrustZone, SEV
* Memory Protection Keys, Supervisor Mode Access Prevention (SMAP)
* Hardware vs. software roots of trust

**Week 7: x86 Hardware Mitigations**
* Control-flow Enforcement Technology (CET): shadow stacks, IBT
* Supervisor Mode Execution Protection (SMEP)
* Architectural limitations and adoption challenges
* **Lab 2 due; Lab 3 released:** Implementing a minimal seccomp sandbox

**Week 8: ARM64 Security Architecture I - Pointer Authentication**
* PAC fundamentals: signing/verification, QARMA algorithm
* ARMv8.3-A PAuth: instruction-pointer/data-pointer authentication
* Integration with OS (APIAKey, APIBKey), compiler support (-msign-return-address)
* **Reading:** ARM whitepaper "Pointer Authentication on ARMv8.3"

**Week 9: ARM64 Security Architecture II - Memory Tagging**
* MTE fundamentals: tag allocation, checking, fault handling
* Synchronous vs. asynchronous modes
* Use cases: probabilistic memory safety, bug detection
* **Reading:** "An Architectural Safe Mode for Complex Systems" (ARM research)

**Week 10: Security Implications of ISA Design**
* **Fixed vs. variable-length instruction sets debate**
* Security impact: gadget availability, decoding complexity
* RISC vs. CISC from security perspective
* Side-channel implications of microarchitectural differences
* **Lab 3 due**

### **Part III: Microarchitectural Attacks & Defenses**

**Week 11: Speculative Execution Attacks Fundamentals**
* Out-of-order execution, speculative execution, branch prediction
* Meltdown, Spectre (V1, V2), Foreshadow
* Microarchitectural state and transient instructions

**Week 12: Side-Channel Attacks**
* Cache timing attacks (Prime+Probe, Flush+Reload)
* Branch prediction side channels
* DRAM-based attacks (Rowhammer, RAMBleed)
* **Lab 4 released:** Demonstrating a simple cache side channel

**Week 13: Mitigations for Microarchitectural Attacks**
* Software mitigations: retpolines, speculation barriers
* Hardware mitigations: site-specific barriers, prediction hardening
* ARM64 speculation barriers (CSDB, SSBS)
* The performance cost of speculation controls

### **Part IV: Synthesis & Future Directions**

**Week 14: Putting It All Together: Case Studies**
* Chrome's multi-layered security: site isolation, V8 sandbox, MTE rollout
* iOS security: APRR, PPL, MTE adoption timeline
* Kernel hardening: Linux kernel self-protection project
* **Lab 4 due**

**Week 15: Research Frontiers & Student Presentations**
* CHERI capabilities: architectural memory safety
* Hardware-assisted fuzzing, sanitizers in silicon
* Formal verification of hardware security features
* **Student project presentations (Days 1-2)**

**Week 16: Course Synthesis & Final Exam**
* The future of hardware/software co-design
* Economics of security: deployment, performance, complexity
* **Final exam (comprehensive, emphasis on analysis)**

---

## **Labs Overview**

1. **Memory Corruption Fundamentals:** Exploit simple buffer overflow on system without protections. Introduction to debuggers and exploit tooling.
2. **Bypassing Modern Software Mitigations:** Chain information leak with ROP to bypass ASLR+DEP on x86_64.
3. **Sandbox Implementation:** Implement a minimal sandbox using seccomp-bpf and namespaces, then attempt to escape it.
4. **Hardware Security Features:** Use QEMU to emulate ARM64 with MTE/PAC, demonstrate bug detection/prevention, measure overhead.

## **Project Ideas**

Students select either a research survey or implementation project:
* **Research Track:** Survey paper on emerging hardware security feature (e.g., Intel LAM, AMD SNP, RISC-V security extensions) with critical analysis.
* **Implementation Track:** Implement a security mechanism (e.g., LLVM pass for sanitization, kernel module using PAC, MTE-aware memory allocator) with evaluation.

## **Academic Integrity & Collaboration**

Labs are individual efforts. Projects may be pairs with permission. All code and written work must be your own, with proper citation of references. Discussion of concepts is encouraged; copying solutions is prohibited.

---

## **Instructor Notes**

* **Tooling Setup:** Provide prepared VM/container images with toolchains for Week 1 to avoid environment issues.
* **Paper Discussions:** Assign 2 students per week to lead discussion of required reading.
* **Guest Lectures:** Consider inviting researchers from industry (ARM, Google Project Zero, Microsoft Security Response) for Weeks 8-10.
* **Flexibility:** The schedule may adapt based on student background and current events (new vulnerabilities/mitigations).

This syllabus provides rigorous graduate-level coverage while maintaining practical hands-on experience with cutting-edge security mechanisms. The progression from software to hardware, culminating in speculative execution attacks, creates a coherent narrative about the ongoing arms race between attackers and defenders across the computing stack.
