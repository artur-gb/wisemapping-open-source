FROM node:18.12.1-buster-slim AS builder

# Install git
RUN apt-get update && apt-get install -y git && rm -rf /var/lib/apt/lists/*

# Set working directory
WORKDIR /app

# Clone the correct frontend repository
RUN git clone https://github.com/NickSuomi/wisemapping-frontend.git .

# Move to the webapp package (correct path!)
WORKDIR /app/packages/webapp

# Install dependencies and build the app
RUN yarn install && PUBLIC_URL=/ yarn build

# Final Nginx stage
FROM nginx:alpine

# Copy build output from builder
COPY --from=builder /app/packages/webapp/dist /usr/share/nginx/html

# Use custom nginx config (optional)
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]