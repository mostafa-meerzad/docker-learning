FROM node:23.3.0-alpine3.20
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
USER appuser
WORKDIR /app
USER root
COPY . .
RUN chown -R appuser:appgroup /app
USER appuser
RUN npm install
ENV API_URL=http://api/myapp.com
EXPOSE 5173
CMD [ "npm", "run", "dev" ]