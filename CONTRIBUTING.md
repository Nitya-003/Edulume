# Contributing to Edulume

<div align="center">

[![SWOC 2026](https://img.shields.io/badge/SWOC-2026-orange?style=for-the-badge)](https://swoc.tech)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=for-the-badge)](../../pulls)
[![Contributors](https://img.shields.io/github/contributors/tarinagarwal/edulume?style=for-the-badge)](https://github.com/tarinagarwal/edulume/graphs/contributors)

**Thank you for your interest in contributing to Edulume!**

</div>

---

## 🎉 SWOC 2026 Contributors

Welcome, SWOC 2026 participants! We're thrilled to have you here. This guide will help you get started with contributing to Edulume.

### Quick Links for SWOC Participants

- 🏷️ [Good First Issues](https://github.com/tarinagarwal/edulume/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22)
- 🆘 [Help Wanted](https://github.com/tarinagarwal/edulume/issues?q=is%3Aissue+is%3Aopen+label%3A%22help+wanted%22)
- 📝 [Documentation Issues](https://github.com/tarinagarwal/edulume/issues?q=is%3Aissue+is%3Aopen+label%3Adocumentation)
- 🐛 [Bug Fixes](https://github.com/tarinagarwal/edulume/issues?q=is%3Aissue+is%3Aopen+label%3Abug)

---

## 📋 Table of Contents

- [Code of Conduct](#-code-of-conduct)
- [Getting Started](#-getting-started)
- [Development Workflow](#-development-workflow)
- [Code Style Guidelines](#-code-style-guidelines)
- [Commit Messages](#-commit-messages)
- [Pull Request Process](#-pull-request-process)
- [Issue Guidelines](#-issue-guidelines)
- [Project Structure](#-project-structure)
- [Getting Help](#-getting-help)

---

## 📜 Code of Conduct

- Be respectful and inclusive
- Provide constructive feedback
- Focus on the code, not the person
- Help others learn and grow
- No harassment, discrimination, or inappropriate behavior

---

## 🚀 Getting Started

### 1. Fork & Clone

```bash
# Fork the repository on GitHub, then:
git clone https://github.com/YOUR_USERNAME/edulume.git
cd edulume
git remote add upstream https://github.com/tarinagarwal/edulume.git
```

### 2. Set Up Development Environment

Follow the complete setup guide in [INSTALLATION.md](INSTALLATION.md)

### 3. Create a Branch

```bash
git checkout -b feature/your-feature-name
# or
git checkout -b fix/bug-description
```

### 4. Make Your Changes

- Write clean, documented code
- Follow the code style guidelines
- Test your changes locally

### 5. Submit a Pull Request

- Push your branch and create a PR
- Fill out the PR template completely
- Wait for review and address feedback

---

## 💻 Development Workflow

### Before You Start

1. Check existing issues and PRs to avoid duplicates
2. For major changes, open an issue first to discuss
3. Ensure your local environment is set up correctly

### Running the Project

```bash
# Terminal 1: Frontend
cd client && npm run dev

# Terminal 2: Backend
cd server && npm run dev

# Terminal 3: Python Backend
cd python-backend && source venv/bin/activate && uvicorn main:app --reload
```

### Testing Your Changes

```bash
# Frontend linting
cd client && npm run lint

# Build check
cd client && npm run build

# Backend
cd server && npm run lint
```

---

## 🎨 Code Style Guidelines

### Frontend (React/TypeScript)

```typescript
// ✅ Good: Typed functional component
interface UserCardProps {
  id: string;
  name: string;
  onUpdate: (id: string) => void;
}

const UserCard: React.FC<UserCardProps> = ({ id, name, onUpdate }) => {
  return (
    <div className="p-4 border rounded-lg hover:shadow-md transition-shadow">
      <h3 className="font-semibold">{name}</h3>
      <button
        onClick={() => onUpdate(id)}
        className="mt-2 px-4 py-2 bg-blue-500 text-white rounded"
      >
        Update
      </button>
    </div>
  );
};
```

**Guidelines:**

- Use functional components with hooks
- Use TypeScript for type safety
- Use Tailwind CSS for styling
- Keep components small and focused
- Use meaningful variable names

### Backend (Express/JavaScript)

```javascript
// ✅ Good: Async handler with error handling
router.post("/items", authenticateToken, async (req, res) => {
  try {
    const { name, description } = req.body;

    if (!name) {
      return res.status(400).json({ error: "Name is required" });
    }

    const item = await prisma.item.create({
      data: { name, description, userId: req.user.id },
    });

    console.log("✅ Item created:", item.id);
    res.status(201).json(item);
  } catch (error) {
    console.error("❌ Error creating item:", error);
    res.status(500).json({ error: "Failed to create item" });
  }
});
```

**Guidelines:**

- Use async/await for asynchronous operations
- Add proper error handling with try/catch
- Use emoji indicators in console logs (✅ ❌ ⚠️)
- Follow REST API conventions
- Validate all user inputs

### Python Backend (FastAPI)

```python
# ✅ Good: Typed function with docstring
async def process_pdf(file_path: str, session_id: str) -> dict:
    """
    Process a PDF file and store embeddings in Pinecone.

    Args:
        file_path: Path to the PDF file
        session_id: Session ID for tracking

    Returns:
        Dictionary with processing results
    """
    try:
        logger.info(f"Processing PDF: {file_path}")
        # Implementation
        return {"status": "success", "chunks": 100}
    except Exception as e:
        logger.error(f"Error processing PDF: {str(e)}")
        raise
```

**Guidelines:**

- Use type hints for all functions
- Add docstrings to functions
- Use async functions where appropriate
- Follow PEP 8 style guide
- Add proper logging

---

## 📝 Commit Messages

Use conventional commit format:

```
<type>: <subject>

[optional body]

[optional footer]
```

### Types

| Type       | Description                           |
| ---------- | ------------------------------------- |
| `feat`     | New feature                           |
| `fix`      | Bug fix                               |
| `docs`     | Documentation changes                 |
| `style`    | Code style changes (formatting, etc.) |
| `refactor` | Code refactoring                      |
| `test`     | Adding or updating tests              |
| `chore`    | Maintenance tasks                     |
| `perf`     | Performance improvements              |

### Examples

```bash
feat: add user profile page with avatar upload
fix: resolve discussion voting bug on mobile
docs: update API documentation for courses endpoint
style: format code with prettier
refactor: simplify authentication middleware
chore: update dependencies to latest versions
```

---

## 🔄 Pull Request Process

### Before Submitting

1. **Sync with upstream**

   ```bash
   git fetch upstream
   git rebase upstream/main
   ```

2. **Run checks**

   ```bash
   npm run lint
   npm run build
   ```

3. **Test thoroughly**
   - Test on different browsers
   - Test on mobile devices
   - Check for console errors

### PR Template

When creating a PR, include:

```markdown
## Description

Brief description of changes

## Type of Change

- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## Related Issues

Closes #123

## Testing

- [ ] Tested locally
- [ ] No new warnings/errors
- [ ] Tested on mobile

## Screenshots (if applicable)

Add screenshots for UI changes

## Checklist

- [ ] Code follows style guidelines
- [ ] Self-reviewed my code
- [ ] Added comments for complex logic
- [ ] Documentation updated (if needed)
```

### Review Process

1. Maintainers will review your PR
2. Address any feedback or requested changes
3. Re-request review after making changes
4. PR will be merged once approved

---

## 🐛 Issue Guidelines

### Bug Reports

Include:

- Clear description of the bug
- Steps to reproduce
- Expected vs actual behavior
- Screenshots/videos if applicable
- Browser/OS information
- Console error messages

### Feature Requests

Include:

- Clear description of the feature
- Use case and benefits
- Proposed implementation (optional)
- Mockups/examples (if applicable)

---

## 📁 Project Structure

```
edulume/
├── client/                 # React frontend
│   ├── src/
│   │   ├── components/     # React components
│   │   │   ├── auth/       # Authentication components
│   │   │   ├── courses/    # Course-related components
│   │   │   ├── discussions/# Discussion forum components
│   │   │   ├── layout/     # Layout components (Navbar, Footer)
│   │   │   ├── roadmaps/   # Roadmap components
│   │   │   ├── resources/  # PDF/Ebook components
│   │   │   └── ui/         # Reusable UI components
│   │   ├── hooks/          # Custom React hooks
│   │   ├── utils/          # Utility functions
│   │   ├── types/          # TypeScript type definitions
│   │   └── App.tsx         # Main app component
│   └── public/             # Static assets
│
├── server/                 # Express.js backend
│   ├── routes/             # API route handlers
│   │   ├── auth.js         # Authentication routes
│   │   ├── courses.js      # Course routes
│   │   ├── discussions.js  # Discussion routes
│   │   ├── roadmaps.js     # Roadmap routes
│   │   └── ...
│   ├── middleware/         # Express middleware
│   ├── config/             # Configuration (passport, etc.)
│   ├── socket/             # Socket.io handlers
│   ├── prisma/             # Prisma schema and migrations
│   ├── utils/              # Utility functions
│   └── index.js            # Server entry point
│
└── python-backend/         # FastAPI AI backend
    ├── fileUpload/         # PDF upload handlers
    ├── RAGresponse/        # RAG implementation
    ├── sessionCleanup/     # Session cleanup utilities
    └── main.py             # FastAPI entry point
```

---

## 🎯 Areas for Contribution

### 🟢 Good First Issues (Beginner Friendly)

- UI improvements and bug fixes
- Documentation updates
- Adding comments to code
- Writing tests
- Accessibility improvements

### 🟡 Intermediate

- New API endpoints
- Frontend features
- Performance optimizations
- Database model additions

### 🔴 Advanced

- AI/ML improvements
- Architecture changes
- Security enhancements
- Infrastructure updates

---

## 🆘 Getting Help

- 📖 Check [INSTALLATION.md](INSTALLATION.md) for setup issues
- 💬 Comment on the issue you're working on
- 🔍 Search existing issues and discussions
- 📧 Reach out to maintainers

---

## 🏆 Recognition

Contributors will be recognized in:

- README.md contributors section
- Release notes
- GitHub contributors page

---

## 📄 License

By contributing, you agree that your contributions will be licensed under the MIT License.

---

<div align="center">

**Thank you for contributing to Edulume! 🎉**

Your contributions help make education more accessible for everyone.

</div>
