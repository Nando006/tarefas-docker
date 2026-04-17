# Cliente-Servidor com Docker 

## 👥 Integrantes do Grupo
- Fernando Sérgio Ribeiro da Silva - 2310254
- Vinicius Santos Pereira - 2310071
- Rachel Vieira Ramos Alves - 2310775
- Clara Luz Lopes Dias da Cruz - 2310133
- Yuri

## 🚀 Como Rodar o Projeto (Passo a Passo)
Siga os comandos abaixo na ordem exata para preparar o ambiente e subir a aplicação

1. Colocar os arquivos Dockerfile em suas respectivas pastas frontend e backend vou deixar comentado na linha 1 qual arquivo é de qual pasta.

> Atenção: Verifique se suas credenciais nos .env do backend está correta com essas credenciais:
- DB_HOST=127.0.0.1
- DB_PORT=5432
- DB_USER=postgres
- DB_PASSWORD=123
- DB_NAME=tarefasdb
- PORT=3001  

> Observação: Não esqueça de configurar o postres da sua máquina e criar o banco de dados tarefasdb, quando você inicializar o projeto pela primeira vez a tabela tarefas será criada automaticamente.

> Atenção: Caso esteja configurado com alguma credencial diferente, mude para a correta para dar certo

2. Verifique se o seu terminal está na raiz do projeto tarefas-docker, para funcionar você tem que executar os comandos nesse local

> Observação: Garanta que seu docker desktop esteja ativo e funcionando

> Atenção: É muito importante que seja executado nessa ordem os comandos!

3. O primeiro comando vamos criar a rede do projeto que vai ser a "ponte" virtual para que os containers consigam conversar entre si pelo nome.
<pre> docker network create rede-tarefas </pre>

4. Agora vamos transformar o código das pastas frontend e backend em imagens prontas para rodar.

- Backend:
<pre> docker build -t imagem-backend ./backend </pre>

- Frontend:
<pre> docker build -t imagem-frontend ./frontend </pre>

> Atenção: É muito importante que o banco de dados seja executa primeiro em seguida o backend e depois o frontend

7. Iniciando o Banco de Dados (postgres) - Subimos o banco de dados oficial do PostgreSQL com as credenciais necessárias para a API funcionar
<pre> docker run -d --name postgres --network rede-tarefas -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=123 -e POSTGRES_DB=tarefasdb -p 5432:5432 postgres:alpine </pre>

8. Iniciando o backend (backend) - Rodamos a APi (Node.JS) conectada ao banco. Ela utiliza a porta 3001
<pre> docker run -d --name backend --network rede-tarefas -e DB_HOST=postgres -e DB_USER=postgres -e DB_PASSWORD=123 -e DB_NAME=tarefasdb -p 3001:3001 imagem-backend </pre>

> Atenção: Se alguma credencial do comando for diferente das que tá como padrão, altere para dar certo.

9. Iniciando o frontend (frontend) - Rodamos o front que será acessado na porta 5173
<pre> docker run -d --name frontend --network rede-tarefas -p 5173:5173 imagem-frontend </pre>

> Observação: Caso rode o backend antes do banco de dados executar o comando: 
<pre> docker restart backend </pre>

## 🖥️ Feito isso, Acesse:
- Interface: Abra no navegador http://localhost:5173
- Status do Banco: Acesse http://localhost:3001/db-status para confirmar a conexão.




