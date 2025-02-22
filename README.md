# Portfolio Application

A modern portfolio application built with secure DevOps practices and deployed using AWS infrastructure.

## 🚀 Features

- Modern web application architecture
- Secure container deployment
- CI/CD integration
- Automated security scanning
- Performance monitoring
- Automated dependency updates

## 🛠️ Tech Stack

- Node.js
- Docker
- GitHub Actions
- SonarQube
- AWS ECS (Fargate)
- AWS CloudWatch

## 🔐 Security Features

- Automated dependency scanning (Dependabot)
- Code quality analysis (SonarQube)
- Container security best practices
- HTTPS enforcement
- Regular security updates
- Non-root container user

## 📋 Prerequisites

- Node.js >= 14
- Docker
- AWS CLI
- Git

## 🏗️ Local Development

1. Install dependencies:
```bash
npm install
```

2. Set up environment variables:
```bash
cp .env.example .env
# Edit .env with your configuration
```

3. Start development server:
```bash
npm run dev
```

## 🐳 Docker Build

Build the container:
```bash
docker build -t portfolio-app .
```

Run locally:
```bash
docker run -p 3000:3000 portfolio-app
```

## 🔄 CI/CD Pipeline

The application uses GitHub Actions for CI/CD:

1. **Continuous Integration** (`app-ci.yml`)
   - Dependency installation
   - Code linting
   - Unit tests
   - SonarQube analysis
   - Docker build
   - Security scanning

2. **Automated Updates**
   - Dependabot configuration for:
     - npm packages
     - GitHub Actions
   - Weekly security updates
   - Automated PR creation

## 📊 Quality Gates

- SonarQube analysis must pass
- All tests must pass
- Security scan must pass
- Docker build must succeed
- Code coverage >= 80%

## 📁 Project Structure

```
portfolio-app/
├── src/               # Application source code
├── tests/             # Test files
├── public/            # Static assets
├── .github/
│   ├── workflows/     # GitHub Actions workflows
│   └── dependabot.yml # Dependency update config
├── Dockerfile         # Container configuration
├── .dockerignore      # Docker ignore file
├── sonar-project.properties  # SonarQube configuration
└── package.json       # Project dependencies
```

## 🧪 Testing

Run tests:
```bash
npm test
```

Run coverage:
```bash
npm run coverage
```

## 📝 Environment Variables

| Variable | Description                           | Required           |
|----------|---------------------------------------|--------------------|
| NODE_ENV | Environment (development/production)  | Yes                |
| PORT     | Application port                      | No (default: 3000) |
| API_URL  | Backend API URL                       | Yes                |

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 👥 Contact

- Developer: Isaac Tanddoh
- Email: thekloudwiz@gmail.com

## 🙏 Acknowledgments

- JOMACS IT INC.
- Node.js community
- GitHub Actions
- AWS
- DevSecOps community

## 📝 Notes

- Ensure all environment variables are properly set before deployment
- Follow the security guidelines in the documentation
- Keep dependencies updated
- Run security scans regularly 