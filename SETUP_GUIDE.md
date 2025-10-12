# 🚀 Portfolio Setup Guide

Complete step-by-step guide to get your portfolio up and running.

## 📋 Prerequisites

Before you begin, ensure you have the following installed:
- **Node.js** (v18 or higher) - [Download](https://nodejs.org/)
- **npm** or **yarn** or **pnpm**
- **Git** - [Download](https://git-scm.com/)
- **Docker** (optional, for containerized development) - [Download](https://www.docker.com/)

## 🛠️ Installation Steps

### 1. Clone or Create Project

```bash
# Create project directory
mkdir reactjs-portfolio
cd reactjs-portfolio

# Initialize git repository
git init
```

### 2. Create Project Structure

Create the following folder structure:

```
reactjs-portfolio/
├── .github/
│   └── workflows/
│       ├── ci.yml
│       └── cd.yml
├── public/
├── src/
│   ├── components/
│   │   ├── layout/
│   │   │   ├── Header.tsx
│   │   │   └── Footer.tsx
│   │   └── sections/
│   │       ├── Hero.tsx
│   │       ├── About.tsx
│   │       ├── Skills.tsx
│   │       ├── Projects.tsx
│   │       ├── Experience.tsx
│   │       └── Contact.tsx
│   ├── contexts/
│   │   └── ThemeContext.tsx
│   ├── data/
│   │   ├── profile.ts
│   │   ├── skills.ts
│   │   ├── projects.ts
│   │   └── experience.ts
│   ├── types/
│   │   └── index.ts
│   ├── App.tsx
│   ├── main.tsx
│   └── index.css
├── .eslintrc.json
├── .prettierrc
├── .gitignore
├── .env.example
├── Dockerfile
├── Dockerfile.dev
├── docker-compose.yml
├── nginx.conf
├── package.json
├── tsconfig.json
├── tsconfig.node.json
├── vite.config.ts
├── tailwind.config.js
├── jest.config.js
└── README.md
```

### 3. Copy All Configuration Files

Copy all the files from the artifacts I created into their respective locations in your project.

### 4. Install Dependencies

```bash
npm install
```

### 5. Set Up Environment Variables

```bash
# Copy the example env file
cp .env.example .env.local

# Edit .env.local with your actual values
nano .env.local  # or use your preferred editor
```

### 6. Customize Your Portfolio

#### Update Profile Information
Edit `src/data/profile.ts`:
```typescript
export const profile = {
  name: "Your Name",
  title: "Your Title",
  email: "your.email@example.com",
  // ... update other fields
};
```

#### Update Skills
Edit `src/data/skills.ts` to match your skill set.

#### Update Projects
Edit `src/data/projects.ts` with your actual projects.

#### Update Experience
Edit `src/data/experience.ts` with your work history.

### 7. Run Development Server

```bash
# Start the development server
npm run dev

# Open browser at http://localhost:5173
```

## 🧪 Testing

```bash
# Run tests
npm run test

# Run tests in watch mode
npm run test:watch

# Generate coverage report
npm run test:coverage

# Run linter
npm run lint

# Fix linting issues
npm run lint:fix

# Format code
npm run format

# Type check
npm run type-check
```

## 🐳 Docker Development

### Option 1: Using Docker Compose (Recommended)

```bash
# Start development environment
docker-compose up dev

# Access at http://localhost:5173
```

### Option 2: Using Docker Directly

```bash
# Build development image
docker build -t portfolio:dev -f Dockerfile.dev .

# Run container
docker run -p 5173:5173 -v $(pwd):/app portfolio:dev
```

## 📦 Building for Production

```bash
# Create production build
npm run build

# Preview production build locally
npm run preview
```

## 🚀 Deployment Options

### Option 1: Vercel (Recommended for React)

1. Install Vercel CLI:
```bash
npm install -g vercel
```

2. Deploy:
```bash
vercel --prod
```

### Option 2: Netlify

1. Install Netlify CLI:
```bash
npm install -g netlify-cli
```

2. Deploy:
```bash
netlify deploy --prod
```

### Option 3: GitHub Pages

1. Add to `package.json`:
```json
{
  "homepage": "https://yourusername.github.io/repository-name"
}
```

2. Install gh-pages:
```bash
npm install --save-dev gh-pages
```

3. Add deploy script to `package.json`:
```json
{
  "scripts": {
    "predeploy": "npm run build",
    "deploy": "gh-pages -d dist"
  }
}
```

4. Deploy:
```bash
npm run deploy
```

### Option 4: Docker Production

```bash
# Build production image
docker build -t portfolio:prod .

# Run container
docker run -p 80:80 portfolio:prod

# Or use docker-compose
docker-compose up prod
```

### Option 5: AWS S3 + CloudFront

1. Build the project:
```bash
npm run build
```

2. Install AWS CLI and configure:
```bash
aws configure
```

3. Upload to S3:
```bash
aws s3 sync dist/ s3://your-bucket-name --delete
```

4. Invalidate CloudFront cache:
```bash
aws cloudfront create-invalidation --distribution-id YOUR_DIST_ID --paths "/*"
```

## 🔧 CI/CD Setup

### GitHub Actions

The project includes pre-configured GitHub Actions workflows:

1. **CI Pipeline** (`.github/workflows/ci.yml`):
   - Runs on every push and PR
   - Lints code
   - Runs tests
   - Builds application

2. **CD Pipeline** (`.github/workflows/cd.yml`):
   - Runs on push to main branch
   - Deploys to production

#### Setup GitHub Secrets

Go to your repository Settings → Secrets and add:

For Vercel:
- `VERCEL_TOKEN`
- `VERCEL_ORG_ID`
- `VERCEL_PROJECT_ID`

For Netlify:
- `NETLIFY_AUTH_TOKEN`
- `NETLIFY_SITE_ID`

For Snyk (security scanning):
- `SNYK_TOKEN`

## 🎨 Customization

### Changing Colors

Edit `tailwind.config.js`:
```javascript
theme: {
  extend: {
    colors: {
      primary: {
        // Your custom colors
      }
    }
  }
}
```

### Adding New Sections

1. Create component in `src/components/sections/`
2. Import and add to `App.tsx`
3. Update navigation in `Header.tsx`

### Modifying Animations

Framer Motion is used for animations. Edit animation properties in components:
```tsx
<motion.div
  initial={{ opacity: 0 }}
  animate={{ opacity: 1 }}
  transition={{ duration: 0.6 }}
>
```

## 📝 Best Practices

1. **Keep data separated**: All content is in `src/data/` for easy updates
2. **Use TypeScript**: Leverage types for better development experience
3. **Test your changes**: Run tests before committing
4. **Commit conventions**: Follow conventional commits (feat, fix, docs, etc.)
5. **Environment variables**: Never commit `.env` files
6. **Optimize images**: Use WebP format and lazy loading
7. **Accessibility**: Test with screen readers and keyboard navigation

## 🐛 Troubleshooting

### Port already in use
```bash
# Kill process on port 5173
lsof -ti:5173 | xargs kill -9

# Or use different port
npm run dev -- --port 3000
```

### Module not found
```bash
# Clear node_modules and reinstall
rm -rf node_modules package-lock.json
npm install
```

### Build fails
```bash
# Clear cache and rebuild
rm -rf dist .vite
npm run build
```

### Docker issues
```bash
# Rebuild without cache
docker-compose build --no-cache

# Remove all containers and volumes
docker-compose down -v
```

## 📚 Additional Resources

- [React Documentation](https://react.dev/)
- [TypeScript Handbook](https://www.typescriptlang.org/docs/)
- [Vite Guide](https://vitejs.dev/guide/)
- [Tailwind CSS](https://tailwindcss.com/docs)
- [Framer Motion](https://www.framer.com/motion/)

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'feat: add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📧 Support

If you encounter any issues:
1. Check this guide first
2. Search existing GitHub issues
3. Create a new issue with detailed description

## ✅ Checklist

Before deploying to production:

- [ ] Updated all personal information in `src/data/`
- [ ] Replaced placeholder images with actual project images
- [ ] Tested all links (GitHub, LinkedIn, etc.)
- [ ] Verified contact form works
- [ ] Tested on mobile devices
- [ ] Checked accessibility (WCAG compliance)
- [ ] Optimized images and assets
- [ ] Set up analytics (Google Analytics, etc.)
- [ ] Configured custom domain (if applicable)
- [ ] Set up SSL certificate
- [ ] Tested in multiple browsers
- [ ] Run lighthouse audit (90+ score)
- [ ] Set up error monitoring (Sentry, etc.)

---

**🎉 Congratulations! Your portfolio is ready to showcase your work!**