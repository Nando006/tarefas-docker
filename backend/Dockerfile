# Esse arquivo coloca na pasta raiz de backend

# usa uma imagem oficial do Node.JS
FROM node:22-alpine

# Define o diretório de trabalho dentro do container
WORKDIR /app

# Copia os arquivos de dependências e instala
COPY package*.json ./
RUN npm install

# Copia o restante do código
COPY . .

# Expõe a porta que a API vai rodar
EXPOSE 3001

# Comando para iniciar o backend
CMD ["npm", "start"]