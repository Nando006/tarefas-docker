# Guia de Execução Local do Backend (Node.js)

Olá! Este guia foca em como executar **apenas o backend** da aplicação diretamente na sua máquina, sem o uso de Docker.

O objetivo é permitir que você teste a conexão com um banco de dados PostgreSQL que você tenha criado, garantindo que a API funcione corretamente antes de avançar para a etapa de containerização.

## 🛠️ Pré-requisitos

Antes de começar, você precisa ter:

1.  **Node.js**: Versão 22.
2.  **Git**: Para clonar o repositório.
3.  **PostgreSQL**: Um servidor PostgreSQL instalado e em execução na sua máquina ou em um servidor que você tenha acesso. Você também precisará de um cliente de banco de dados como o **DBeaver** ou **pgAdmin** para criar o banco de dados e verificar os dados.

## 👣 Passo a Passo

### Passo 1: Clone o Repositório e Prepare o Ambiente

Se ainda não o fez, clone o projeto e navegue até a pasta correta.

```bash
# Clone o repositório do projeto
git clone <URL_DO_REPOSITORIO>

# Entre na pasta raiz do projeto
cd <NOME_DA_PASTA_DO_PROJETO>

# Navegue até a pasta específica do backend
cd backend
```

### Passo 2: Instale as Dependências

Dentro da pasta `backend`, execute o seguinte comando para instalar todas as bibliotecas que a API precisa para funcionar (Express, pg, etc.):

```bash
npm install
```

### Passo 3: Crie o Banco de Dados

Usando seu cliente de banco de dados preferido (pgAdmin, DBeaver, etc.), conecte-se ao seu servidor PostgreSQL e **crie um novo banco de dados**. Por exemplo, você pode chamá-lo de `tarefasdb`.

A aplicação irá criar a tabela `tarefas` automaticamente na primeira vez que for executada com sucesso.

### Passo 4: Configure as Variáveis de Ambiente (O Passo Mais Importante!)

A API não armazena senhas ou informações de conexão diretamente no código. Em vez disso, ela lê essas informações de um arquivo de ambiente.

1.  Na pasta `backend`, você encontrará um arquivo chamado `.env`.
2.  Abra o novo arquivo `.env` e **preencha com os dados do seu banco de dados PostgreSQL**.

Aqui está um exemplo de como seu arquivo `.env` deve ficar:

```ini
# Arquivo: backend/.env

# --- Configurações do Banco de Dados PostgreSQL ---
# Endereço do seu servidor de banco de dados.
# Se estiver rodando na sua própria máquina, use 'localhost' ou '127.0.0.1'.
DB_HOST=127.0.0.1

# Porta padrão do PostgreSQL. Mantenha 5432, a menos que você tenha alterado.
DB_PORT=5432

# O nome de usuário que você usa para acessar o PostgreSQL.
# O padrão costuma ser 'postgres', mas use o seu.
DB_USER=postgres

# A senha que você DEFINIU para o usuário acima durante a instalação do PostgreSQL.
DB_PASSWORD=123

# O nome exato do banco de dados que você criou no Passo 3.
DB_NAME=tarefasdb

# --- Porta da Aplicação ---
# Porta em que o servidor backend irá rodar.
PORT=3001
```

> ⚠️ **Atenção:** O arquivo `.env` contém informações sensíveis. Ele nunca deve ser enviado para um repositório Git. Já existe uma entrada no arquivo `.gitignore` para ignorá-lo.

### Passo 5: Execute o Servidor

Com tudo configurado, inicie o servidor backend no modo de desenvolvimento:

```bash
npm run dev
```

### Passo 6: Verifique o Funcionamento

Se a conexão com o banco de dados for bem-sucedida, você verá as seguintes mensagens no seu terminal:

```
✅ Conexão com o PostgreSQL bem-sucedida. Usando o banco de dados.
🚀 Backend rodando na porta 3001
```

* **Se você vir a mensagem de sucesso**, parabéns! Sua API está conectada ao banco.
* **Se você vir uma mensagem de aviso** (`⚠️ Falha ao conectar com o PostgreSQL`), verifique novamente todos os dados no seu arquivo `.env` (host, usuário, senha, nome do banco) e garanta que seu serviço do PostgreSQL está realmente em execução.

Para um teste final, abra seu navegador e acesse [http://localhost:3001/db-status](http://localhost:3001/db-status). Você deverá ver uma mensagem JSON confirmando a conexão.

Agora você está pronto para prosseguir com a containerização!