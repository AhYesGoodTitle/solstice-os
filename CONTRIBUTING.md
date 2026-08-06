<div align='center'>
<h1>Contributing to the Solstice OS Project!</h1>
</div>  


<h3>1. Making an Overlay (the primary way people contribute)</h3>
The whole point of Solstice is that overlays are decentralized. You make one, you share it, people use it. <b><i>No gatekeeping, no approval process</i></b>.


<h4>1a. Create Your Overlay</h4>

Create a git repository. That's it. 
Structure it like this:

```
your-overlay/
├── recipes/
│   ├── package1.sh
│   ├── package2.sh
│   └── ...
├── README.md
└── metadata.yml (optional)
```


<h3>1b. Test it Locally</h3>

Before you share your overlay, test it in Solstice:

```bash
solpm add-overlay /local-path/to/your-overlay
solpm install package1
```
Does it work? Cool, you're good to go.<br><br>  

<h3>1c. Share Your Overlay With the World</h3>

Push to GitHub (or your preferred git host) and get people to add your overlay to their Solstice machines: 

```bash
# Users will have to add your overlay manually
# GitHub example:
solpm add-overlay https://github.com/yourname/your-overlay
```

<b>People can now use your overlay. That's it. You're done.</b><br><br>


<h2>2. Annual Awards</h2>

<b>Every year the community gets the chance to vote on the best overlays.  
Winners get: </b>
<i>
- featured on solstice-os.org
- mentioned in the release notes
- community recognition
</i>

This is not intended to gate-keep winners, just celebrating people who made cool stuff. And yes, you still manually add them. <b><i>We're not forcing anyone to use an overlay.</b></i>

<h2>3. Contributing to Core Recipes</h2>

Want to improve the core distro itself? Yep, we take pull requests!
<i>
- Found a bug? File an issue
- Made a fix? Send a pull request
- Improved our documentation? We'll merge it
- <b>You will get credited.</b>
</i>


## Lastly, Just be Cool About it
<i>
- Be nice to people<br>
- Don't be a gatekeeper<br>  
- Credit the people who help you<br>  
- Help new users and developers learn<br>  
- <b>Solstice is open source. We're all here because we love free and open source software ❤️</b>
</i><br><br>
<div align='center'>
<h3>That's it. Build cool overlays, contribute when you feel like it, or hang out in the awesome community. We're all learning together.</h3>
</div>

<h2>Shoutouts</h2>
- <b>NEOAPPS</b> — Early collaborator, distro developer, helping with package manager architecture<br>  
- <b>AhYesGoodTitle</b> — Making the documentation beautiful 🤩<br>
- <b>Linux From Scratch</b> — The inspiration for how we approach bootstrapping [https://www.linuxfromscratch.org/]
