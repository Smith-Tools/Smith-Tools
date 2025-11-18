# Smith Tools - Swift Architecture Validation Framework

> **Automated architectural analysis, pattern validation, and agentic guidance for production-ready Swift applications.**

---

## 🎯 What is Smith Tools?

Smith Tools is a comprehensive framework that helps Swift teams:

- **Prevent architectural violations** with automated validation (Rules 1.1-1.5)
- **Extract monolithic features** systematically with effort estimation
- **Improve testability** by detecting closure injection and untestable patterns
- **Validate code patterns** against expert best practices
- **Integrate guidance** directly into Claude Code workflow
- **Access Apple documentation** with WWDC context through sosumi

### The Problem We Solve

Developers waste time on:
- ✗ Deciding when to extract reducers vs. keep state flat
- ✗ Understanding whether their architecture violates composition rules
- ✗ Finding the WWDC session that explained this exact pattern
- ✗ Knowing how much effort refactoring will take
- ✗ Validating code against inconsistent architectural standards

Smith Tools solves this in seconds.

---

## 📦 Core Components

### **smith-skill** - Claude Agentic Skill (v1.2.0)

The main integration point for Claude Code users.

**Features:**
- TCA Composition Validators (4 powerful bash scripts)
- Pattern library (40+ validated patterns)
- Build analysis and monitoring tools
- Decision trees for architectural choices
- Platform-specific guidance (visionOS, iOS, macOS)
- Integrated sosumi routing for Apple documentation

**Installation:**
```bash
git clone https://github.com/Smith-Tools/smith-skill.git
ln -s $(pwd)/smith-skill ~/.claude/skills/smith
```

**Use in Claude:**
```
"Use Smith skill to analyze my TCA reducer"
"Is my reducer violating composition rules?"
"What should I extract from this monolithic feature?"
```

**GitHub:** https://github.com/Smith-Tools/smith-skill

---

### **sosumi-skill** - Apple Documentation + WWDC

Complementary skill providing real-time access to Apple ecosystem.

**Features:**
- Real-time Apple documentation (sosumi.ai on-demand)
- WWDC transcripts (2018-2025, searchable, cached)
- Code examples from Apple's guides
- Seamless integration with smith-skill

**Installation:**
```bash
git clone https://github.com/Smith-Tools/sosumi.git
ln -s $(pwd)/sosumi ~/.claude/skills/sosumi
```

**Use in Claude:**
```bash
/skill sosumi search "playAnimation RealityKit"
/skill sosumi wwdc "RealityComposer Pro"
/skill sosumi fetch realitykit/playAnimation
```

**GitHub:** https://github.com/Smith-Tools/sosumi

**Workflow Integration:**
```
Architecture question  → smith-skill
API question          → sosumi-skill
Both needed?          → Use both (optimal)
```

---

### **TCA Composition Validators** - Four Powerful Scripts

Automated architectural analysis tools:

1. **validate-tca-composition.sh**
   - Detects Rules 1.1-1.5 violations
   - Human-readable or JSON output
   - Strict mode for CI/CD gating
   - Severity levels (HIGH/MEDIUM/LOW)

2. **check-tca-testability.sh**
   - Testability scoring (0-100)
   - Identifies testing blockers
   - Tracks @Dependency usage
   - Provides improvement guidance

3. **recommend-tca-extractions.sh**
   - Feature extraction planning
   - Prioritizes by value (P1/P2/P3)
   - Effort estimation (2h-12h)
   - Sprint planning guidance

4. **analyze-tca-dependency-graph.sh**
   - Maps state dependencies
   - Calculates coupling complexity
   - Identifies problematic patterns
   - Suggests decomposition strategies

**Quick Start:**
```bash
./smith-skill/Scripts/validate-tca-composition.sh Sources/
./smith-skill/Scripts/check-tca-testability.sh Sources/ --threshold 75
./smith-skill/Scripts/recommend-tca-extractions.sh Sources/
./smith-skill/Scripts/analyze-tca-dependency-graph.sh Sources/
```

**Documentation:**
See [smith-skill/Scripts/README-TCA-COMPOSITION.md](./smith-skill/Scripts/README-TCA-COMPOSITION.md)

---

### **smith-core** - Universal Swift Patterns

Applies across any Swift project (not just TCA).

**Covers:**
- Dependency injection (@Dependency patterns)
- Swift concurrency (async/await, @MainActor, Task)
- Modern testing (Swift Testing, @Test)
- Access control and public API boundaries
- Type-safe error handling

---

### **Analysis Tools**

**smith-spmsift** - SPM Package Analysis
- 96% reduction in context vs. verbose output
- Circular dependency detection
- Deep import analysis
- Dependency health scoring

**smith-sbsift** - Swift Build Analysis
- Compilation bottleneck identification
- Build time optimization suggestions
- Progress monitoring
- Resource usage tracking

**smith-xcsift** - Xcode Project Analysis
- Build hang detection
- Index store corruption detection
- Workspace build monitoring
- Schema analysis

---

## 🚀 Quick Start

### For Claude Code Users

```bash
# 1. Install smith-skill
git clone https://github.com/Smith-Tools/smith-skill.git
ln -s $(pwd)/smith-skill ~/.claude/skills/smith

# 2. Install sosumi-skill (optional but recommended)
git clone https://github.com/Smith-Tools/sosumi.git
ln -s $(pwd)/sosumi ~/.claude/skills/sosumi

# 3. Use in Claude
"Use Smith skill to analyze my TCA composition"
```

**Result:** Claude automatically detects your question and provides guidance with optional WWDC context.

### For CLI Users (Direct Validators)

```bash
# Check TCA composition
./smith-skill/Scripts/validate-tca-composition.sh Sources/

# Score testability
./smith-skill/Scripts/check-tca-testability.sh Sources/

# Get extraction recommendations
./smith-skill/Scripts/recommend-tca-extractions.sh Sources/
```

### For CI/CD Integration

```yaml
# GitHub Actions example
- name: Validate TCA Architecture
  run: |
    ./smith-skill/Scripts/validate-tca-composition.sh Sources/ --strict
    ./smith-skill/Scripts/check-tca-testability.sh Sources/ --threshold 75

# Pre-commit hook
./smith-skill/Scripts/validate-tca-composition.sh Sources/ --strict
```

**Full CI/CD Examples:**
See [TCA-COMPOSITION-INTEGRATION.md](./TCA-COMPOSITION-INTEGRATION.md)

---

## 🎓 TCA Composition Rules (1.1-1.5)

Smith enforces five foundational architectural rules:

| Rule | Problem | Trigger | Solution | Effort |
|------|---------|---------|----------|--------|
| **1.1** | Monolithic feature | State > 15 props OR Actions > 40 | Extract child features | 4-8h |
| **1.2** | Untestable closures | `var x: (...) -> Effect` | Use @Dependency | 2h |
| **1.3** | Code duplication | Duplicate handlers | Consolidate | 1h |
| **1.4** | Unclear organization | 5+ vague methods | Better naming | 4-8h |
| **1.5** | Tight coupling | 5+ child features | Reduce nesting | 6-12h |

**Example Analysis:**
```
ReadingLibraryFeature: 20 properties, 42 actions, 3 closures

Violations Detected:
🔴 HIGH: Monolithic feature (Rule 1.1)
🔴 CRITICAL: Closure injection (Rule 1.2) ← Fix immediately
🟠 MEDIUM: Tight coupling (Rule 1.5)

Recommendations:
- Extract SearchFeature (unblock testing, 4-6h) ← P1
- Replace closures with @Dependency (2h each) ← P1
- Extract FilteringFeature (maintainability, 2-4h) ← P2
```

---

## 📚 Documentation

### Organized by User Type

**Claude Code Users:**
1. Install smith-skill
2. Try: `"Use Smith skill for my TCA reducer"`
3. Read: [smith-skill/SKILL.md](./smith-skill/SKILL.md)

**CLI Users:**
1. Run: `./smith-skill/Scripts/validate-tca-composition.sh Sources/`
2. Read: [smith-skill/Scripts/README-TCA-COMPOSITION.md](./smith-skill/Scripts/README-TCA-COMPOSITION.md)
3. Explore: [TCA-COMPOSITION-INTEGRATION.md](./TCA-COMPOSITION-INTEGRATION.md) for CI/CD

**Architecture Reviewers:**
1. Review: [AGENTS-TCA-PATTERNS.md](./smith-skill/AGENTS-TCA-PATTERNS.md)
2. Use: Decision trees in [AGENTS-DECISION-TREES.md](./smith-skill/AGENTS-DECISION-TREES.md)
3. Validate: Metrics from composition validators

### By Topic

| Topic | Documentation |
|-------|---------------|
| **TCA Patterns** | [smith-skill/AGENTS-TCA-PATTERNS.md](./smith-skill/AGENTS-TCA-PATTERNS.md) |
| **Universal Swift** | [smith-skill/AGENTS-AGNOSTIC.md](./smith-skill/AGENTS-AGNOSTIC.md) |
| **Architecture Decisions** | [smith-skill/AGENTS-DECISION-TREES.md](./smith-skill/AGENTS-DECISION-TREES.md) |
| **visionOS Patterns** | [smith-skill/PLATFORM-VISIONOS.md](./smith-skill/PLATFORM-VISIONOS.md) |
| **Validators Reference** | [smith-skill/Scripts/README-TCA-COMPOSITION.md](./smith-skill/Scripts/README-TCA-COMPOSITION.md) |
| **CI/CD Integration** | [TCA-COMPOSITION-INTEGRATION.md](./TCA-COMPOSITION-INTEGRATION.md) |
| **Apple Docs (sosumi)** | [sosumi-skill/SKILL.md](./sosumi-skill/SKILL.md) |
| **Integration Status** | [SOSUMI_INTEGRATION_COMPLETE.md](./SOSUMI_INTEGRATION_COMPLETE.md) |
| **Performance Metrics** | [PERFORMANCE_REPORT.md](./PERFORMANCE_REPORT.md) |

---

## 💡 How It Works Together

### Real Example: RCP Timeline Query

**Your Question:**
"How do I play RCP timelines directly without Behaviors using playAnimation()?"

**Smith Provides:**
- Architecture pattern (Behavior vs direct approaches)
- TCA integration recommendation
- When to use which approach

**Sosumi Provides:**
- `playAnimation()` exact API signature
- Code examples from Apple
- WWDC 2023/2024 session references
- RealityComposer Pro timeline documentation

**Result:** Complete understanding with architecture + implementation + Apple's guidance

---

## 📊 Performance & Efficiency

### Comparison: WebSearch vs Smith Tools

| Query | WebSearch | Smith + Sosumi | Savings |
|-------|-----------|----------------|---------|
| API lookup | 1,500 tokens | 700 tokens | 53% |
| Architecture pattern | 2,000 tokens | 400 tokens | 80% |
| WWDC + API | 3,000 tokens | 1,000 tokens | 67% |
| **Average** | **2,167 tokens** | **700 tokens** | **68%** |

**Additional Benefits:**
- ✅ No network latency (local validators)
- ✅ Cached WWDC context (no repeated searches)
- ✅ Integrated workflow (no context switching)
- ✅ Architectural validation (not just API docs)
- ✅ CI/CD ready (bash scripts)

---

## 🔄 Typical Workflow

### Week 1: Baseline & Planning
```bash
# Analyze current state
./smith-skill/Scripts/validate-tca-composition.sh Sources/
./smith-skill/Scripts/check-tca-testability.sh Sources/

# Create prioritized backlog
./smith-skill/Scripts/recommend-tca-extractions.sh Sources/
```

### Week 2-3: Implementation
1. Fix Priority 1 violations (closure injection) - 2h each
2. Extract Priority 2 features (monolithic) - 4-12h each
3. Improve P3 clarity - 4-8h each

### Week 4+: Monitoring
```bash
# Weekly metrics
./smith-skill/Scripts/validate-tca-composition.sh Sources/ --json > report.json
./smith-skill/Scripts/check-tca-testability.sh Sources/ --json > testability.json
```

---

## ✨ What's New in v1.2.0

**smith-skill:**
- ✅ TCA Composition Validators (4 scripts, tested)
- ✅ Integrated sosumi routing for Apple docs
- ✅ WWDC coverage updated to 2025
- ✅ Enhanced pattern library (40+ patterns)
- ✅ Improved visionOS documentation

**sosumi-skill:**
- ✅ Production-ready implementation
- ✅ Real-time Apple documentation access
- ✅ WWDC transcripts 2018-2025 (searchable)
- ✅ Seamless integration with smith-skill

---

## 🛠️ Installation Options

### Minimal (Just Smith Skill)
```bash
git clone https://github.com/Smith-Tools/smith-skill.git
ln -s $(pwd)/smith-skill ~/.claude/skills/smith
```

### Recommended (Smith + Sosumi)
```bash
git clone https://github.com/Smith-Tools/smith-skill.git
git clone https://github.com/Smith-Tools/sosumi.git
ln -s $(pwd)/smith-skill ~/.claude/skills/smith
ln -s $(pwd)/sosumi ~/.claude/skills/sosumi
```

### With Analysis Tools
```bash
# Install optional tools (for context efficiency)
brew install elkraneo/tap/spmsift
brew install elkraneo/tap/sbsift

# Install skills
ln -s $(pwd)/smith-skill ~/.claude/skills/smith
ln -s $(pwd)/sosumi ~/.claude/skills/sosumi
```

### Verify Installation
```bash
ls ~/.claude/skills/smith/SKILL.md
ls ~/.claude/skills/sosumi/SKILL.md
```

---

## ❓ FAQ

**Q: Is Smith only for TCA projects?**
A: No. TCA composition is emphasized, but Smith covers universal Swift patterns (concurrency, testing, dependencies, access control).

**Q: Do I need sosumi?**
A: No, but it's highly recommended. Smith works independently. Sosumi adds Apple documentation and WWDC context.

**Q: Do I need the analysis tools (spmsift, sbsift)?**
A: No. Smith and sosumi work standalone. Tools make analysis more context-efficient and are optional.

**Q: How often should I run validators?**
A: As part of CI/CD (every PR) + weekly metrics during active development.

**Q: Can I customize the rules?**
A: Currently no. Rules 1.1-1.5 are architectural standards. They reflect best practices from production apps.

**Q: What's the typical refactoring effort?**
A: P1 (critical): 2h | P2 (features): 4-12h | P3 (clarity): 4-8h

**Q: Does this work in CI/CD?**
A: Yes! All validators have CI/CD modes. See [TCA-COMPOSITION-INTEGRATION.md](./TCA-COMPOSITION-INTEGRATION.md).

---

## 📞 Support

**Documentation:**
- Main reference: [smith-skill/SKILL.md](./smith-skill/SKILL.md)
- TCA patterns: [AGENTS-TCA-PATTERNS.md](./smith-skill/AGENTS-TCA-PATTERNS.md)
- Validators: [smith-skill/Scripts/README-TCA-COMPOSITION.md](./smith-skill/Scripts/README-TCA-COMPOSITION.md)
- CI/CD: [TCA-COMPOSITION-INTEGRATION.md](./TCA-COMPOSITION-INTEGRATION.md)

**GitHub:**
- smith-skill: https://github.com/Smith-Tools/smith-skill
- sosumi-skill: https://github.com/Smith-Tools/sosumi
- Organization: https://github.com/Smith-Tools

---

## 🔗 Directory Structure

```
Smith Tools/
├── .github/profile/README.md               ← Organization overview
├── README.md                               ← This file
├── SOSUMI_INTEGRATION_COMPLETE.md          ← Integration status
├── PERFORMANCE_REPORT.md                   ← Metrics & benchmarks
├── TCA-COMPOSITION-INTEGRATION.md          ← CI/CD guide
├── TCA-COMPOSITION-SUMMARY.md              ← Feature summary
│
├── smith-skill/                            ← Main Claude skill
│   ├── SKILL.md                            ← Skill documentation
│   ├── AGENTS-TCA-PATTERNS.md              ← Pattern library
│   ├── AGENTS-AGNOSTIC.md                  ← Universal patterns
│   ├── AGENTS-DECISION-TREES.md            ← Decision guidance
│   ├── PLATFORM-VISIONOS.md                ← visionOS patterns
│   └── Scripts/
│       ├── validate-tca-composition.sh
│       ├── check-tca-testability.sh
│       ├── recommend-tca-extractions.sh
│       ├── analyze-tca-dependency-graph.sh
│       └── README-TCA-COMPOSITION.md
│
├── sosumi-skill/                           ← Apple documentation skill
│   ├── SKILL.md
│   ├── Sources/
│   └── Package.swift
│
├── smith-core/                             ← Universal patterns
├── smith-spmsift/                          ← SPM analysis
├── smith-sbsift/                           ← Swift build analysis
└── smith-xcsift/                           ← Xcode analysis
```

---

## 📈 Versioning

Smith uses **semantic versioning**:

- **Major (X.0.0):** Breaking changes to patterns or rules
- **Minor (X.Y.0):** New features (validators, patterns, tools)
- **Patch (X.Y.Z):** Bug fixes, documentation updates

**Current Version:** **v1.2.0**
- Added: TCA Composition Validators
- Updated: Sosumi integration with WWDC 2025
- Backward compatible: All existing patterns work unchanged

---

## 🤝 Contributing

To contribute patterns or improvements:

1. Discuss new patterns in issues first
2. Add case studies (DISCOVERY-*.md) when patterns emerge
3. Update relevant AGENTS-*.md files
4. Test on real codebases
5. Update version in SKILL.md when merging

---

## ✅ Status

**v1.2.0 - Production Ready**

- ✅ TCA Composition Validators (tested)
- ✅ Sosumi Integration (verified)
- ✅ WWDC Coverage (2018-2025)
- ✅ Documentation (comprehensive)
- ✅ GitHub Synced
- ✅ Ready for Production Use

---

**Smith Tools - Making Swift Architecture Production-Ready**

*Automated validation, expert patterns, agentic guidance - all built for real projects.*

---

Last updated: November 17, 2025
Version: v1.2.0
Status: Production Ready
