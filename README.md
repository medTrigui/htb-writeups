# HTB Write-ups

[![MkDocs](https://img.shields.io/badge/docs-mkdocs-blue)](https://medTrigui.github.io/htb-writeups/)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)
[![Last Update](https://img.shields.io/badge/last%20update-January%202024-orange)](https://github.com/medTrigui/htb-writeups)

Comprehensive HackTheBox machine writeups with detailed attack methodologies, focusing on manual exploitation techniques and vulnerability analysis.

## What's Inside

- **Detailed Writeups**: Complete attack chains from enumeration to privilege escalation
- **Manual Techniques**: Focus on understanding vulnerabilities rather than automated tools
- **Modern Styling**: Beautiful documentation with dark/light mode support
- **Interactive Features**: Code copying, search functionality, and responsive design
- **Learning Resources**: Methodology guides, tool references, and cheat sheets

## Quick Start

### Viewing the Documentation

Visit the live documentation: [https://medTrigui.github.io/htb-writeups/](https://medTrigui.github.io/htb-writeups/)

### Local Development

1. **Clone the repository**:
   ```bash
   git clone https://github.com/medTrigui/htb-writeups.git
   cd htb-writeups
   ```

2. **Install dependencies**:
   ```bash
   pip install mkdocs-material mkdocs-minify-plugin
   ```

3. **Serve locally**:
   ```bash
   mkdocs serve
   ```

4. **Build for production**:
   ```bash
   mkdocs build
   ```

## Project Structure

```
htb-writeups/
├── docs/                           # Documentation source
│   ├── index.md                   # Homepage
│   ├── Sau/                       # Machine writeups
│   │   ├── Sau.md                # Main writeup
│   │   ├── img/                  # Screenshots
│   │   └── scripts/              # Exploit scripts
│   ├── resources/                 # Learning resources
│   │   ├── methodology.md        # Attack methodology
│   │   ├── tools.md             # Tool references
│   │   └── cheatsheets.md       # Quick reference guides
│   ├── stylesheets/              # Custom CSS
│   │   └── extra.css            # HTB-themed styling
│   └── javascripts/              # Custom JavaScript
│       └── mathjax.js           # Math rendering
├── mkdocs.yml                     # MkDocs configuration
└── site/                          # Generated static site
```

##  Features

### Enhanced User Experience
- **🌙 Dark/Light Mode**: Automatic theme switching based on user preference
- **🔍 Advanced Search**: Intelligent search with syntax highlighting
- **📱 Responsive Design**: Optimized for desktop and mobile viewing
- **⚡ Fast Loading**: Instant navigation and optimized assets

### HTB-Themed Styling
- **🎯 Difficulty Badges**: Color-coded difficulty indicators
- **🛡️ Security Icons**: Material Design icons for better visual organization
- **🔗 Attack Path Visualization**: Clear visual flow of exploitation steps
- **💻 Enhanced Code Blocks**: Syntax highlighting with copy functionality

### Learning Resources
- **📚 Methodology Guide**: Systematic approach to machine exploitation
- **🛠️ Tool References**: Comprehensive tool documentation and usage
- **📋 Cheat Sheets**: Quick reference guides for common tasks
- **🔗 External Links**: Direct links to CVE databases and exploit resources

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

### Adding New Writeups

1. Create a new directory under `docs/` with the machine name
2. Add your markdown writeup following the established format
3. Include screenshots in an `img/` subdirectory
4. Add any exploit scripts to a `scripts/` subdirectory
5. Update the navigation in `mkdocs.yml`
6. Update the machine table in `docs/index.md`

### Writeup Template

Each writeup should follow this structure:

```markdown
# Machine Name <span class="difficulty-badge difficulty-LEVEL">LEVEL</span>

!!! info "Machine Information"
    - **Platform**: HackTheBox  
    - **Difficulty**: Easy/Medium/Hard/Insane
    - **Retired**: Date
    - **OS**: Linux/Windows

<div class="attack-path">
<strong>Path To Root</strong>: Brief description of attack chain
</div>

## :material-information-outline: Synopsis
[Detailed description]

## :material-radar: Enumeration
[Reconnaissance and discovery]

## :material-target: Foothold
[Initial access]

## :material-arrow-up-bold: Privilege Escalation
[Path to administrative access]

## :material-lightbulb: Lessons Learned
[Key takeaways and references]
```

##  License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

##  Disclaimer

This documentation is created for **educational purposes only**. All techniques should only be used in authorized testing environments or personal lab setups. Always obtain proper permission before testing any systems.

##  Contact

- **GitHub**: [@medTrigui](https://github.com/medTrigui)
- **LinkedIn**: [Mohamed Trigui](https://linkedin.com/in/mohamed-trigui)

---

<div align="center">
<em>Happy Hacking! 🔐</em>
</div>