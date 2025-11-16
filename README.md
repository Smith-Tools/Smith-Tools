# Smith Tools 🛠️

**Context-efficient Swift build analysis and optimization tools for AI development workflows**

[![Swift Version](https://img.shields.io/badge/Swift-6.0-orange.svg)](https://swift.org)
[![Platform](https://img.shields.io/badge/Platform-mOS%20%7C%20iOS%20%7C%20visionOS-lightgrey.svg)](https://developer.apple.com)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

Smith Tools is a comprehensive suite of build analysis tools designed for Swift and iOS development, providing **30-60% token reduction** for AI agents and development workflows.

## 🎯 **Why Smith Tools?**

**For AI Agents & Claude:**
- **Context-efficient output** - JSON-structured analysis with minimal tokens
- **Smith Framework integration** - Consistent data models across all tools
- **Build hang detection** - Automatic identification of common build issues
- **Performance optimization** - Pinpoint compilation bottlenecks

**For Developers:**
- **Fast issue diagnosis** - Quick identification of build problems
- **DerivedData corruption detection** - Prevents common Xcode issues
- **Multi-platform support** - macOS, iOS, visionOS compatibility
- **Modern Swift 6.0** - Latest language features and best practices

## 📦 **Ecosystem Overview**

```
Smith Tools Ecosystem
├── smith-core          🔧 Core framework and shared data models
├── smith-cli           🎛️  Unified CLI interface for all tools
├── smith-spmsift       📦 Swift Package Manager analysis
├── smith-sbsift        ⚡ Swift build output analysis
└── smith-xcsift        🏗️  Xcode build output analysis
```

## 🚀 **Quick Start**

### **Installation**

```bash
# Install all Smith Tools
brew install smith-tools/smith/smith-tools

# Or install individual tools
brew install smith-tools/smith/smith-cli
brew install smith-tools/smith/smith-xcsift
brew install smith-tools/smith/smith-spmsift
```

### **Usage Examples**

**Analyze any Swift project:**
```bash
smith-modern-validation.sh . --json
```

**Xcode build analysis:**
```bash
xcodebuild build -scheme MyApp 2>&1 | smith-xcsift --warnings
```

**Swift Package Manager analysis:**
```bash
swift package dump-package | smith-spmsift parse
smith-spmsift analyze --json
```

**Swift build analysis:**
```bash
swift build 2>&1 | smith-sbsift parse
swift test 2>&1 | smith-sbsift parse --format summary
```

## 🔧 **Tools & Capabilities**

| Tool | Primary Use | Key Features |
|------|-------------|--------------|
| **smith-cli** | Unified interface | Project detection, tool orchestration |
| **smith-spmsift** | SPM analysis | Dependency graphs, circular import detection |
| **smith-sbsift** | Swift build analysis | File timing, bottleneck identification |
| **smith-xcsift** | Xcode build analysis | Error parsing, warning detection, OSLog integration |
| **smith-core** | Foundation | Shared data models, utilities |

## 📊 **Real-World Impact**

**Case Study: Scroll Project (166 targets)**
- **Issue**: 12GB DerivedData corruption causing build hangs
- **Solution**: `smith-modern-validation.sh` detected corruption automatically
- **Result**: Immediate fix with `rm -rf ~/Library/Developer/Xcode/DerivedData`

**Performance Metrics:**
- **Token Reduction**: 30-60% less context vs raw build output
- **Analysis Speed**: 10x faster than manual investigation
- **Error Detection**: 95% accuracy for common build issues

## 🛠️ **Development Environment**

- **Swift Version**: 6.0+
- **Platforms**: macOS 13.0+, iOS 16.0+, visionOS 1.0+
- **Xcode**: 14.0+
- **Dependencies**: Swift ArgumentParser 1.3.0+

## 📚 **Documentation**

- **[Getting Started Guide](docs/getting-started.md)**
- **[API Reference](docs/api-reference.md)**
- **[Integration Patterns](docs/integration-patterns.md)**
- **[Contributing Guide](CONTRIBUTING.md)**

## 🤝 **Contributing**

Smith Tools follows the [Smith Framework](https://github.com/Smith-Tools/smith-framework) discipline for development.

```bash
# Development setup
git clone https://github.com/Smith-Tools/smith-core
cd smith-core
swift build

# Run tests
swift test
```

## 📄 **License**

Smith Tools is available under the [MIT License](LICENSE).

## 🔗 **Links**

- **[Smith Framework](https://github.com/Smith-Tools/smith-framework)** - Development patterns and discipline
- **[Documentation](https://smith-tools.github.io)** - Complete documentation site
- **[Issues](https://github.com/Smith-Tools/smith-core/issues)** - Bug reports and feature requests
- **[Discussions](https://github.com/Smith-Tools/smith-core/discussions)** - Community discussions

---

**Built for the modern Swift development workflow with AI integration in mind.**