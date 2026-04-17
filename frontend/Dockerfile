# Build dos arquivos estáticos
FROM node:18-alpine AS builder

# Define o diretório de trabalho dentro do container
WORKDIR /app

# Copia os arquivos de dependências
COPY package*.json ./

# Instala
RUN npm install

# Copia o restante do código
COPY . .

# Faz o build
RUN npm run build

# Usa Nginx para servir arquivos estáticos
FROM nginx:alpine

# Copia os arquivos do frontend para a pasta pública do Nginx
COPY --from=builder /app/dist /usr/share/nginx/html

# Expõe a porta padrão do Nginx
EXPOSE 80

# Inicia o servidor
CMD ["nginx", "-g", "daemon off;"]