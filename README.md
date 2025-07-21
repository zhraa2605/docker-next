# Next.js Docker Development Setup

This project demonstrates how to dockerize a Next.js application for development with hot reloading support.

## Development Setup

### Prerequisites
- Docker and Docker Compose installed on your machine
- Node.js (optional, for local development)

### Quick Start

1. **Clone and setup the project:**
   \`\`\`bash
   git clone <your-repo>
   cd nextjs-docker-app
   \`\`\`

2. **Run with Docker Compose (Recommended for development):**
   \`\`\`bash
   docker-compose up --build
   \`\`\`
   
   Or use the npm script:
   \`\`\`bash
   npm run docker:dev
   \`\`\`

3. **Access your application:**
   Open [http://localhost:3000](http://localhost:3000) in your browser

### Development Features

- **Hot Reloading**: Changes to your code will automatically reload the application
- **Volume Mounting**: Your local files are mounted into the container
- **Node Modules Isolation**: Container's node_modules won't conflict with local ones

### Alternative Docker Commands

**Build and run development container manually:**
\`\`\`bash
docker build -f Dockerfile.dev -t nextjs-dev .
docker run -p 3000:3000 -v $(pwd):/app -v /app/node_modules nextjs-dev
\`\`\`

**Production build:**
\`\`\`bash
npm run docker:prod
npm run docker:run
\`\`\`

### File Structure

- \`Dockerfile.dev\` - Development Docker configuration
- \`Dockerfile\` - Production Docker configuration (multi-stage build)
- \`docker-compose.yml\` - Docker Compose configuration for development
- \`.dockerignore\` - Files to exclude from Docker build context

### Environment Variables

You can add environment variables to the \`docker-compose.yml\` file:

\`\`\`yaml
environment:
  - NODE_ENV=development
  - NEXT_PUBLIC_API_URL=http://localhost:3001
  - DATABASE_URL=postgresql://...
\`\`\`

### Troubleshooting

**Port already in use:**
\`\`\`bash
docker-compose down
# Or change the port in docker-compose.yml
\`\`\`

**Permission issues on Linux:**
\`\`\`bash
sudo chown -R $USER:$USER .
\`\`\`

**Hot reloading not working:**
- Ensure \`WATCHPACK_POLLING=true\` is set in environment variables
- Check that volumes are properly mounted
