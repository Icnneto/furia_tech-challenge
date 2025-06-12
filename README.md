# Know Your Fan — Tech Challenge FURIA

## Introdução

Este projeto foi desenvolvido como parte do **Tech Challenge promovido pela FURIA**, com o objetivo de explorar dados fornecidos por fãs de eSports para gerar insights por meio de Inteligência Artificial. Através de formulários, coleta de dados via web scraping e processamento com IA, o projeto visa entregar um dashboard dinâmico com análises comportamentais dos usuários.

## Tecnologias Utilizadas

| Camada      | Tecnologias principais                                        |
|-------------|--------------------------------------------------------------|
| Frontend    | HTML, TailwindCSS, JavaScript Vanilla                        |
| Backend     | Node.js, Express, MongoDB, Mongoose, Puppeteer (Stealth)     |
| Outros      | OpenAI API, Country-State API, Postman, GitHub Pages, Render |

## Estrutura de Pastas

### Backend
```bash
backend/
├── api/
│ ├── controllers/ # Lógica dos endpoints
│ ├── routes/
│ │ ├── app.js # Configuração do app Express
│ │ └── routes.js # Rotas definidas
├── classes/ # Classes de domínio
│ ├── aiProfileAnalysis.js # Classe que representa o perfil analisado
│ ├── userData.js # Classe que representa os dados do usuário
│ └── XScrapedData.js # Classe que representa dados raspados do X
├── database/
│ ├── config/ # Conexão com o MongoDB
│ └── models/ # Schemas do Mongoose
├── services/
│ ├── aiAnalysis.js # Requisição e análise via OpenAI
│ ├── connectAndSendData.js # Integração com banco de dados
│ ├── fetchAllData.js # Requisição de todos os dados salvos
│ ├── scraper.js # Web scraping com Puppeteer (modo stealth)
│ └── watchMongo.js # Observa mudanças no MongoDB
├── .env # Variáveis de ambiente
├── puppeteer.config.cjs # Configurações do Puppeteer Stealth
├── package.json
├── server.js # Inicializa o servidor e rotas
```
### Frontend
```bash
frontend/
├── public/
│ ├── assets/ # Imagens e ícones
│ ├── css/ # Estilizações com Tailwind
│ ├── js/
│ │ ├── dashboard/ # Scripts para renderizar o dashboard
│ │ ├── utils/
│ │ ├── countryState.js # API de países/estados
│ │ ├── erros.js # Exibição de mensagens de erro
│ │ ├── eventos.js # Eventos de formulário
│ │ ├── interesses.js # Interesses do usuário
│ │ ├── sendForm.js # Envia os dados ao backend
│ │ └── upload.js # Lida com upload de arquivos
│ └── pages/
│ ├── dashboard.html # Interface com cards analíticos
│ └── index.html # Página principal com formulário
├── src/ # (Reservado para scripts auxiliares)
├── .env
├── package.json
```
## Rodando o Projeto Localmente

Para clonar e rodar o projeto localmente:

1. Clone o repositório:

   ```bash
   git clone https://github.com/Icnneto/furia_tech-challenge.git
   cd furia_tech_front
   ```

2. Instale as dependências do **frontend**:

   ```bash
   cd frontend
   npm install
   ```

3. Instale as dependências do **backend**:

   ```bash
   cd ../backend
   npm install
   ```

4. Configure o arquivo `.env` no backend com as seguintes variáveis:

   ```env
   OPEN_AI=your_openai_key
   DB_CONNECTION_STRING=your_mongodb_uri
   COUNTRY_STATE_KEY=your_country_state_key
   ```

5. Inicie o servidor localmente:

   ```bash
   npm run dev
   ```

6. ⚠️ **Atenção:** os endpoints usados no frontend estão atualmente apontando para a API publicada na Render. Para rodar localmente, altere as URLs dentro dos arquivos JS no frontend para `http://localhost:PORT`.

## Backend — Detalhes

### API e Estrutura
- `/api/routes.js`: define as rotas.
- `/api/controllers/`: lida com requisições e respostas.
- As rotas são integradas ao Express através de `app.js`.
- A comunicação com o dashboardo foi configurada via `Server-Sent Events`, para atualização em tempo real

### Scraper com Puppeteer
- Utiliza Puppeteer + stealth plugin para contornar bloqueios da rede X (Twitter).
- Arquivo principal: `services/scraper.js`
- Coleta a bio e as últimas postagens, com o intuito de fornecer material para a IA analisar.

### Análise com IA
- Envia dados para a API da OpenAI para gerar uma análise qualitativa.
- Arquivo: `services/aiAnalysis.js`
- A análise é armazenada no MongoDB com o perfil do usuário.
- O perfil é analisado com base nos interesses e eventos preenchidos no formulário, em conjunto com os dados raspados do X.
- A análise retorna:
   - `Relevância para informativos`
   - `Relevância para eventos`
   - `Sinergia com a Furia`
   - `Overview do perfil (textual)`

### Banco de Dados
- MongoDB Atlas
- Mongoose utilizado para criação dos modelos
- Monitoração com `watchMongo.js` para detectar novas inserções.

### Deploy
- **Render.com** para hospedagem do backend (⚠️ Atualmente o projeto na render está desativado - rode localmente)
- Variáveis de ambiente `.env` protegidas (API Key, URI MongoDB, etc.)


## Frontend — Detalhes

### Formulário (index.html)
- Captura dados como nome, email interesses e eventos em que já tomou parte.
- Os campos contam com validação do preenchimento.
- `sendForm.js` envia os dados via `fetch`.

### Dashboard (dashboard.html)
- Faz requisição ao backend para obter dados.
- `dashboard.js` renderiza os cards com dados do MongoDB.
- Visual atrativo com Tailwind.

### Deploy
- GitHub Pages usado para hospedar a interface pública.
- Código fonte disponível no repositório do GitHub.

## Melhorias Futuras

- Dashboard com filtros e gráficos avançados
- Histórico de análises por usuário
- Scraping adaptativo com múltiplas redes sociais
- Suporte multilíngue no frontend

## Conclusão

Este projeto explora o potencial da integração entre scraping, IA e análise de dados para gerar inteligência sobre os fãs de eSports. Com uma arquitetura modular e automações inteligentes, o sistema abre caminho para usos reais em campanhas e estratégias de marketing digital.


