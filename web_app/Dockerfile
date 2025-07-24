# node.js  image
FROM node:18-alpine

# Create app directory
WORKDIR /app

# Copy package files and install dependences
COPY package.json ./
COPY package-lock.json ./
RUN npm install

# Copy app code
COPY . .

# Expose port and run app
EXPOSE 3000
CMD ["npm", "start"]

