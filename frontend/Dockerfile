# Step 1: Use a Node.js base image (Bun can be installed on top of it)
FROM node:18 AS build

# Install Bun
RUN curl -fsSL https://bun.sh/install | bash

# Add Bun to the PATH
ENV PATH="/root/.bun/bin:${PATH}"

# Set the working directory
WORKDIR /app

# Copy package.json and bun.lockb to install dependencies
COPY package.json bun.lock /app/

# Install dependencies using Bun
RUN bun install

EXPOSE 5173

# Step 2: Run the Bun development server
CMD ["bun","run", "dev", "--host", "0.0.0.0"]
