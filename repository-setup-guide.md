# Repository Setup and Maintenance Guide

**Purpose:** Documentation for setting up and maintaining this React knowledge base  
**Last Updated:** July 15, 2025  
**Maintainer:** [Pawan Pawar]  

#### **Cross-Platform (Node.js Script)**
---
Firstly I was confused which folder & file structure should I follow in order to store all of my notes. Then I asked claude to help me out in generating the folder & file structure and which naming convection should I follow. Then it gave me all the information I wanted and from that info I understood which convention I need to follow. And after that I used the below node.js file to generate everything in one go.

Firstly Create `generate-structure.js` and run `node generate-structure.js`:

```javascript
const fs = require('fs');
const path = require('path');

const structure = {
  'README.md': '# React Knowledge Base\n\n> Generated structure - see setup-guide.md for details\n',
  '01-fundamentals': {
    'README.md': '# Fundamentals\n\nCore React concepts and basics.\n',
    'what-is-react.md': '',
    'jsx-explained.md': '',
    'components-basics.md': '',
    'virtual-dom-explained.md': '',
    'react-capabilities.md': ''
  },
  '02-core-concepts': {
    'README.md': '# Core Concepts\n\nEssential React patterns and APIs.\n',
    'state-management.md': '',
    'props-and-data-flow.md': '',
    'lifecycle-methods.md': '',
    'hooks-overview.md': '',
    'usestate-explained.md': '',
    'useeffect-explained.md': ''
  },
  '03-advanced-concepts': {
    'README.md': '# Advanced Concepts\n\nDeep dives into React internals.\n',
    'context-api.md': '',
    'performance-optimization.md': '',
    'error-boundaries.md': '',
    'reconciliation-fiber.md': '',
    'how-react-works.md': '' 
  },
  '04-ecosystem': {
    'README.md': '# React Ecosystem\n\nLibraries and tools that work with React.\n',
    'react-router.md': '',
    'state-libraries.md': '',
    'testing-react.md': '',
    'popular-libraries.md': ''
  },
  '05-development-tools': {
    'README.md': '# Development Tools\n\nSetup, build tools, and development workflow.\n',
    'development-environment.md': '',
    'build-tools.md': '',
    'debugging-tools.md': '',
    'npm-commands-explained.md': ''
  },
  '06-best-practices': {
    'README.md': '# Best Practices\n\nCode organization and optimization techniques.\n',
    'code-organization.md': '',
    'naming-conventions.md': '',
    'performance-tips.md': '',
    'accessibility.md': ''
  },
  '07-patterns-and-techniques': {
    'README.md': '# Patterns and Techniques\n\nAdvanced React patterns and architectural approaches.\n',
    'component-patterns.md': '',
    'custom-hooks.md': '',
    'render-props.md': '',
    'hoc-patterns.md': ''
  },
  '08-real-world-examples': {
    'README.md': '# Real World Examples\n\nPractical implementations and case studies.\n',
    'todo-app-breakdown.md': '',
    'authentication-flow.md': '',
    'data-fetching-patterns.md': ''
  },
  '09-resources-and-references': {
    'README.md': '# Resources and References\n\nExternal learning materials and documentation.\n',
    'recommended-resources.md': '',
    'useful-libraries.md': '',
    'community-resources.md': ''
  },
  '10-quick-discoveries': {
    'README.md': '# Quick Discoveries\n\nTIL (Today I Learned) entries and quick insights.\n',
    'til-npm-commands.md': '',
    'til-react-quirks.md': '',
    'interesting-react-facts.md': ''
  },
  'assets': {
    'images': {},
    'diagrams': {},
    'code-examples': {}
  }
};

function createStructure(obj, currentPath = '.') {
  Object.keys(obj).forEach(key => {
    const fullPath = path.join(currentPath, key);
    
    if (typeof obj[key] === 'object' && obj[key] !== null) {
      if (!fs.existsSync(fullPath)) {
        fs.mkdirSync(fullPath, { recursive: true });
        console.log(`📁 Created directory: ${fullPath}`);
      }
      createStructure(obj[key], fullPath);
    } else {
      if (!fs.existsSync(fullPath)) {
        fs.writeFileSync(fullPath, obj[key]);
        console.log(`📄 Created file: ${fullPath}`);
      }
    }
  });
}

createStructure(structure);
console.log('\n✅ React knowledge base structure created successfully!');
```

## 📁 File Structure Convention

### **Folder Naming Convention**
```
[XX]-[category-name]/
├── README.md              # Section overview and navigation
├── [topic-name].md        # Individual topic files
└── [subtopic-name].md     # Related subtopic files
```

**Rules:**
- **Numbered prefixes** (01-, 02-, etc.) for logical ordering
- **kebab-case** for all folder and file names
- **Descriptive but concise** names
- **README.md** in every folder for navigation

### **File Naming Patterns**
- `what-is-[topic].md` - Introductory explanations
- `[topic]-explained.md` - Deep dive explanations  
- `[topic]-patterns.md` - Pattern collections
- `til-[discovery].md` - Today I Learned entries
- `[topic]-vs-[topic].md` - Comparison articles

### **Content Structure Template**
Every knowledge file should follow this structure:

```markdown
# [Topic Name]

---
**Tags:** [tag1, tag2, tag3]
**Difficulty:** [beginner/intermediate/advanced]
**Last Updated:** [date]
**Section:** [folder-name]
---

## 🎯 What is [Topic]?
Brief introduction and definition

## 🚀 Why is [Topic] Important?
Importance and use cases

## 🔧 How to Use [Topic]
Practical implementation

## 💡 Examples
Code examples and demonstrations

## ⚠️ Common Pitfalls
Common mistakes and solutions

## 🔗 Related Topics
Links to related files

## 📚 Additional Resources
External links and references
```

## 🔧 Maintenance Workflow

### **Adding New Content**
1. **Choose the right folder** based on complexity and topic
2. **Create the file** using kebab-case naming
3. **Use the content template** for consistency
4. **Update the folder's README.md** with navigation link
5. **Add cross-references** to related topics

### **Updating Navigation**
After adding content, update these files:
- **Main README.md** - Add to table of contents
- **Section README.md** - Add to section navigation
- **Related files** - Add cross-references

## 🎨 Visual Consistency

### **Emoji System**
Use these emojis consistently across all files:
- 🎯 **What/Definition** - Core concepts
- 🚀 **Why/Importance** - Benefits and use cases
- 🔧 **How/Implementation** - Practical usage
- 💡 **Examples** - Code samples
- ⚠️ **Pitfalls** - Common mistakes
- 🔗 **Related** - Cross-references
- 📚 **Resources** - External links
- 🧪 **Testing** - Testing examples
- 🎨 **Advanced** - Advanced patterns

### **Code Block Consistency**
- Use **language tags** for syntax highlighting
- Add **comments** to explain complex parts
- Use **consistent indentation** (2 spaces)
- Include **both correct and incorrect** examples when showing pitfalls

## 📊 Repository Statistics

### **Current Structure Overview**
```
react-knowledge-base/
├── 📁 01-fundamentals/          # 5 topics
├── 📁 02-core-concepts/         # 7 topics  
├── 📁 03-advanced-concepts/     # 5 topics
├── 📁 04-ecosystem/             # 4 topics
├── 📁 05-development-tools/     # 4 topics
├── 📁 06-best-practices/        # 4 topics
├── 📁 07-patterns-techniques/   # 4 topics
├── 📁 08-real-world-examples/   # 3 topics
├── 📁 09-resources-references/  # 3 topics
├── 📁 10-quick-discoveries/     # 3 topics
└── 📁 assets/                   # Images, diagrams, code
```

**Total Files:** ~42 knowledge files + navigation files
