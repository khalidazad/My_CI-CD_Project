# ---- Build Stage ----
FROM node:22 AS build

WORKDIR /app

COPY package.json package-lock.json ./
RUN npm install

COPY . .
RUN npm run build


# ---- Production Stage (Nginx) ----
FROM nginx:alpine

# Copy build output from Vite
COPY --from=build /app/dist /usr/share/nginx/html

# Optional: SPA routing support
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
