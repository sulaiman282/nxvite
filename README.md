# My Broker Cloud Nx Monorepo

## 🏗 Project Structure

```
my-nx-workspace/
├── .github/                    # CI/CD and GitHub specific configurations
│   └── workflows/              # GitHub Actions workflow definitions
│
├── apps/                       # Application-specific projects
│   ├── client/                 # Client-facing web application
│   └── admin/                  # Admin management web application
│
├── libs/                       # Shared libraries and components
│   ├── ui/                     # Reusable UI components
│   ├── core/                   # Core business logic and services
│   ├── utils/                  # Utility functions and helpers
│   └── styles/                 # Shared styling and design system
│
├── tools/                      # Development and build tools
│   └── scripts/                # Utility scripts for development
│
└── config/                     # Environment and configuration files
```

## 📦 Project Overview

This monorepo is a Vue.js-based web application ecosystem using Nx for workspace management. It consists of two primary applications:
- **Client Application**: Customer-facing interface
- **Admin Application**: Administrative management portal

## 🚀 Getting Started

### Prerequisites
- Node.js (v18+)
- npm (v9+)
- Nx CLI (`npm install -g nx`)

### Installation
```bash
# Clone the repository
git clone <repository-url>

# Install dependencies
npm install

# Install Nx CLI globally
npm install -g nx
```

## 🔧 Workspace Commands

### Running Applications
```bash
# Run Client Application
nx serve client

# Run Admin Application
nx serve admin

# Run both applications in parallel
nx run-many -t serve
```

### Building Applications
```bash
# Build Client Application
nx build client

# Build Admin Application
nx build admin

# Build all applications
nx run-many -t build
```

### Testing
```bash
# Run unit tests for a specific app
nx test client

# Run unit tests for a specific library
nx test ui

# Run all tests
nx run-many -t test
```

## 👥 Team Workflow Guidelines

### Development Workflow
1. **Branch Strategy**
   - `main`: Production-ready code
   - `develop`: Integration branch
   - Feature branches: `feature/your-feature-name`
   - Hotfix branches: `hotfix/issue-description`

2. **Code Review Process**
   - All changes must be submitted via Pull Requests
   - Minimum of 1 code review required
   - CI checks must pass before merging
   - Use conventional commits

3. **Shared Library Contributions**
   - All shared components go into `libs/`
   - Use TypeScript for type safety
   - Write unit tests for new components/utilities

### Team Collaboration Standards

#### Client Team
- Work primarily in `apps/client/`
- Utilize shared libraries from `libs/`
- Follow atomic design principles in component creation
- Use Vue Composition API

#### Admin Team
- Work primarily in `apps/admin/`
- Reuse components from `libs/ui/`
- Maintain consistent design language
- Implement role-based access control

## 🔍 Library Usage Guidelines

### UI Library (`libs/ui/`)
- Contains atomic design components
- Use for consistent design across applications
- Example:
  ```typescript
  import { BaseButton } from '@my-broker-cloud/ui'
  ```

### Core Library (`libs/core/`)
- Shared business logic
- Authentication services
- API clients
- Example:
  ```typescript
  import { AuthService } from '@my-broker-cloud/core'
  ```

### Utilities Library (`libs/utils/`)
- Helper functions
- Date manipulation
- Formatting utilities
- Example:
  ```typescript
  import { formatDate } from '@my-broker-cloud/utils'
  ```

## 🛠 Development Tools

- **Nx**: Monorepo and task orchestration
- **Vue 3**: Frontend framework
- **Vite**: Build tool
- **TypeScript**: Primary language
- **Pinia**: State management
- **Vitest**: Unit testing
- **ESLint**: Code linting
- **Prettier**: Code formatting

## 📝 Commit Message Convention

Use [Conventional Commits](https://www.conventionalcommits.org/)

```
<type>[optional scope]: <description>

Examples:
feat(client): add login page
fix(admin): resolve permission bug
docs: update README
```

## 🚧 Deployment

- Automatic deployments via GitHub Actions
- Staging and production environments configured
- Environment-specific configurations in `config/`

## 📋 Best Practices

1. Keep shared logic in libraries
2. Write comprehensive unit tests
3. Follow SOLID principles
4. Use TypeScript for type safety
5. Keep components small and focused

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## 📄 License

[Your License Here]
