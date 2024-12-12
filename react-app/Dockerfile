# FROM node:23.3.0-alpine3.20
# RUN addgroup -S appgroup && adduser -S appuser -G appgroup
# USER appuser
# WORKDIR /app
# USER root
# COPY . .
# RUN chown -R appuser:appgroup /app
# USER appuser
# RUN npm install
# ENV API_URL=http://api/myapp.com
# EXPOSE 5173
# CMD [ "npm", "run", "dev" ]

FROM node:23.3.0-alpine3.20

# Create non-root user and group
RUN addgroup -S appgroup && adduser -S appuser -G appgroup

# Switch to the non-root user
USER appuser

# Set the working directory (created as appuser)
WORKDIR /app

# Switch back to root temporarily for the next steps
USER root

# copy dependency files first so in the future if you rebuild the container Docker can use it's cache, if no dependency has changed.
COPY package*.json .

# Copy project files and fix permissions
RUN chown -R appuser:appgroup /app

# Switch back to non-root user
USER appuser

# Install dependencies
RUN npm install

# now copy all the files 
COPY . .

# Set environment variables
ENV API_URL=http://api/myapp.com

# Expose the app port
EXPOSE 3000

# Start the application
CMD ["npm", "run", "dev"]
