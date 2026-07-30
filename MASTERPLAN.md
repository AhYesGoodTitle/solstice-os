<div align='center'>
<h1>Solstice OS Masterplan 😈</h1>
</div>
<div align='center'>
<h4>This is the technical stuff: The choices I made and why, the defaults, the architecture, and the philosophy. Basically everything that makes Solstice, well, Solstice.</h4>
</div>


<h2>Big Technical Decisions</h2>

<b>Here's what I have locked in:</b>

- <b>Libc:</b> Glibc (<i>for NVIDIA driver support, and broader software compatibility in general</i>)
- <b>Init:</b> Systemd (<i>it's modern, it's standard, everyone uses it</i>)
- <b>Display:</b> x11 by default (<i>Wayland is coming, but it's not ready yet</i>)
- <b>Shell:</b> Bash (<i>it's what people know</i>)
- <b>CPU Architecture:</b> x86_64 only for now (<i>someone else can do arm later as an overlay</i>)
- <b>Package Manager:</b> Bash-based for Phase 1, rewrite in Go for Phase 2

Yeah, I could write the package manager in Python or Rust or whatever. But honestly, bash is simpler, lighter, and I understand every line of it. Phase 1 is about getting bootstrap working. During phase 2 when Solstice gets complex, we'll switch to Go for better structure and fewer dependencies.


<h2>How the Package Manager Works</h2>

<b>I'm calling it `solpm`.</b> It's pretty straightforward:

```bash
solpm install <package>              # Install a package
solpm search <query>                 # Find a package/overlay
solpm remove <package>               # Remove a package/overlay
solpm upgrade                        # Update everything
solpm add-overlay <url>              # Add a new overlay repository
solpm list-overlays                  # See what overlay repositories you have
```

If two overlays have the same package, you get to pick which version you want. <b><i>Simple as that</i>.</b>

<b>Per-Package Options:</b> Each recipe has its own options (menuconfig, no_modules, no_headers, etc). When you install a package, you pick which options you want, <i>or just use the defaults</i>. This is more intuitive than Gentoo's global USE flag system — no need to understand a global config. <i>Each package is self-contained</i>.


<h2>How Many Packages are Maintained Upstream?</h2>

- <b>50 essential</b> — The bootstrap stuff (<i>e.g. the kernel, libc, gcc, make, bash, coreutils</i>)
- <b>100 expanded</b> — Desktop basics so you can actually use Solstice (<i>e.g. x11, systemd, utilities</i>)
- <b>200+ total</b> — By the 1.0 release
- <b>Everything else</b> — Lives in decentralized overlays that the community makes

I'm not trying to mimic Gentoo's thousands of packages. That's exhausting. Overlays handle the rest.


<h2>Folder Structure</h2>

```
solstice-os/
├── recipes/              # The core recipes
│   ├── gcc/
│   ├── glibc/
│   ├── firefox/
│   └── ...
├── scripts/              # Automation stuff for building packages
├── docs/                 # Documentation
├── solpm                 # The package manager itself
└── README.md
```


<h2>The Order to Build Packages</h2>

This is important because of dependencies:

1. The Kernel
2. Glibc
3. Binutils
4. Gcc (stage 1, the bootstrap version)
5. Make, bash, coreutils
6. Everything else
   
<!--- TODO: add specific page on Linux From Scratch that contains info about the host compiler stuff --->
The whole circular dependency thing with gcc is solved by using your host compiler first. Linux From Scratch [https://www.linuxfromscratch.org/] has a whole section on this for further reading.


<h2>Challenges, and How I'll Overcome Them</h2>

- <b>Gcc needs gcc to compile</b> → Use the host compiler to build a bootstrap gcc first. Then use that to build the real one. LFS taught me this.
- <b>Dependency resolution</b> → Just a topological sort of the package graph. Not super fancy, but it works.
- <b>Testing everything</b> → I can't test on every possible system, so crowdsourcing is key.
- <b>Maintenance burden</b> → Overlays will distribute burdern. Core is my job, everything else is handled by the community.

<h2>Projected Goals</h2>

- Stolstice Alpha ships on September 2026 (6 months from the June start)
- 10+ community overlays by the end of the year
- 100+ people actually using Solstice by year 2
- I'm only maintaining like 20% of total packages (the rest is handled by the community)

If that happens, we're golden.

<h2>Shoutouts</h2>
- <b>NEOAPPS</b> — Early collaborator, distro developer, helping with package manager architecture<br>  
- <b>AhYesGoodTitle</b> — Making the documentation beautiful 🤩<br>
- <b>Linux From Scratch</b> — The inspiration for how we approach bootstrapping [https://www.linuxfromscratch.org/]
