# Use official Playwright image which comes with Node.js, npm, and browsers pre-installed
FROM mcr.microsoft.com/playwright:v1.38.0-focal

# Set working directory
WORKDIR /app

# Copy package.json and package-lock.json (if available)
COPY package*.json ./

# Install npm dependencies
RUN npm install

# Copy the test files and configuration
COPY tests/ ./tests/
COPY playwright.config.ts ./
COPY specs/ ./specs/ 

# Install Playwright browsers (already included in base image, but ensures latest)
RUN npx playwright install

# Run tests by default
CMD ["npm", "test"]