# NxtForm AI 🚀

NxtForm AI is a next-generation, AI-assisted form builder inspired by Typeform. Powered by the MERN stack and leveraging cutting-edge LLM capabilities via Groq, NxtForm AI enables users to generate fully functional, responsive, and beautiful multi-step forms from simple natural language prompts in seconds.

---

## 🌟 Key Features

- **AI Prompt-to-Form Generation**: Input a descriptive prompt (e.g., *"Create a customer feedback form for a coffee shop"*) and watch NxtForm AI compile a complete JSON form schema instantly.
- **Rule-Based Fallback Generator**: Works seamlessly even without configured AI APIs using a deterministic, rule-based fallback schema generator.
- **Multi-Step Form Filling UI**: An elegant, distraction-free, step-by-step form interface optimized for high completion rates.
- **Interactive Response Dashboard**: Track submissions, view response analytics, and review key statistics for your forms.
- **User Authentication**: Secure user registration, login, and token-based session persistence using JWT and Bcrypt.
- **Real-Time Editor**: Edit generated schemas, adjust questions, reorder inputs, and preview changes before publishing.
- **Shareable Public Links**: Generate public slugs for each form, allowing anyone to fill out and submit responses.

---

## 🛠️ Tech Stack

**Frontend:**
- **React** (v18)
- **Vite** (Next-gen frontend tooling)
- **React Router Dom** (Single Page App routing)
- **Vanilla CSS** (Custom theme system with smooth CSS variables, glassmorphism, transitions, and dark/light modes)

**Backend:**
- **Node.js** & **Express**
- **MongoDB** & **Mongoose** (ODM)
- **JSON Web Tokens (JWT)** & **BcryptJS** (Auth & Security)
- **Groq SDK / Chat API** (LLM form schema generation)

**Project Management:**
- **npm Workspaces** (Monorepo structure)
- **Concurrently** (Run client and server simultaneously during development)

---

## 📐 Architecture

NxtForm AI is structured as a monorepo utilizing **npm Workspaces**. 

```
                                  +-------------------+
                                  |    NxtForm AI     |
                                  |   (Root Worksp.)  |
                                  +---------+---------+
                                            |
                    +-----------------------+-----------------------+
                    |                                               |
          +---------v---------+                           +---------v---------+
          |  React Frontend   |                           |  Express Backend  |
          |     (/client)     |                           |     (/server)     |
          +---------+---------+                           +---------+---------+
                    |                                               |
                    | (API Calls / JSON Responses)                  | (Mongoose ODM)
                    +---------------------> <-----------------------+
                                            |
                                  +---------v---------+
                                  |      MongoDB      |
                                  |    (Database)     |
                                  +-------------------+
```

---

## 📂 Folder Structure

```
nxtform/
├── client/                     # Frontend React Application
│   ├── src/
│   │   ├── components/         # Reusable UI Components
│   │   ├── contexts/           # Authentication / Global State Providers
│   │   ├── lib/                # API client & utility logic
│   │   ├── pages/              # SPA route pages (Auth, Builder, Dashboard, PublicForm)
│   │   ├── App.jsx             # Main Application Routing and Wrapper
│   │   └── styles.css          # Core Design System CSS & Theme Variable styling
│   ├── index.html
│   └── vite.config.js
├── server/                     # Backend Express API Server
│   ├── src/
│   │   ├── config/             # Database connection and Groq client configs
│   │   ├── controllers/        # Route handlers/controllers (Auth, Form)
│   │   ├── middleware/         # Authentication/Validation Middlewares
│   │   ├── models/             # Mongoose Schemas (User, Form, Response)
│   │   ├── routes/             # Express routes (Auth routes, Form routes)
│   │   ├── services/           # Form generation & AI integration services
│   │   ├── utils/              # Helper utilities
│   │   └── index.js            # Express server entry point
│   └── package.json
├── package.json                # Root package.json managing workspaces
└── README.md                   # Project documentation
```

---

## 🔑 Environment Variables

To run NxtForm AI, set the following environment variables.

### Backend (`/server/.env`)
Create a `.env` file inside the `server/` directory and populate:
```env
PORT=5001
HOST=127.0.0.1
CLIENT_URL=http://localhost:5173
MONGODB_URI=mongodb+srv://<username>:<password>@cluster.mongodb.net/nxtform
JWT_SECRET=your_super_secret_jwt_key
GROQ_API_KEY=your_groq_api_key_here # Optional: Falling back to deterministic rules if empty
```

### Frontend (`/client/.env`)
Create a `.env` file inside the `client/` directory and populate:
```env
VITE_API_BASE_URL=http://localhost:5001/api
```

---

## 🚀 Getting Started

### Prerequisites
- [Node.js](https://nodejs.org/) (v16+)
- [MongoDB](https://www.mongodb.com/) (Local or MongoDB Atlas cluster)

### Installation

1. **Clone the repository:**
   ```bash
   git clone git@github.com:Deeraj749/NxtForm-AI.git
   cd NxtForm-AI
   ```

2. **Install all dependencies** (runs install in workspace roots automatically):
   ```bash
   npm install
   ```

3. **Configure Environment Variables:**
   Create and update `/server/.env` and `/client/.env` files using the format defined in the Environment Variables section.

### Running the Project

- **Run Client & Server Concurrently (Recommended):**
  From the root directory:
  ```bash
  npm run dev
  ```
  *This command starts the backend on `http://localhost:5001` and the frontend client on `http://localhost:5173` simultaneously using `concurrently`.*

- **Run Server Only:**
  ```bash
  npm run dev --workspace server
  ```

- **Run Client Only:**
  ```bash
  npm run dev --workspace client
  ```

---

## 📡 API Endpoints

### 🔐 Authentication API
| Method | Endpoint | Description | Auth Required |
|:---|:---|:---|:---|
| `POST` | `/api/auth/signup` | Register a new user | No |
| `POST` | `/api/auth/login` | Login user and retrieve JWT token | No |
| `GET` | `/api/auth/me` | Fetch active user credentials and profile | **Yes (JWT)** |

### 📋 Form Management & Responses API
| Method | Endpoint | Description | Auth Required |
|:---|:---|:---|:---|
| `GET` | `/api/forms` | List all forms owned by the authenticated user | **Yes (JWT)** |
| `POST` | `/api/forms/generate` | Generate form schema based on a prompt (AI / Fallback) | **Yes (JWT)** |
| `GET` | `/api/forms/:id` | Get details and schema of a specific form | **Yes (JWT)** |
| `PUT` | `/api/forms/:id` | Update form schema/settings | **Yes (JWT)** |
| `GET` | `/api/forms/:id/dashboard` | Fetch response statistics and dashboard overview | **Yes (JWT)** |
| `GET` | `/api/public/forms/:slug` | Retrieve public-facing form structure via slug | No |
| `POST` | `/api/public/forms/:slug/responses` | Submit filled form answers/responses | No |

---

## 📸 Screenshots

*Below are placeholders for the interface screenshots. Add images as they become available:*

1. **Dashboard & Analytics**
   ![Dashboard Analytics](https://via.placeholder.com/800x450/111b30/ffffff?text=NxtForm+AI+-+Dashboard)
   *Real-time statistics including view count, submissions rate, and recent response logs.*

2. **AI Prompt Form Builder**
   ![AI Prompt Builder](https://via.placeholder.com/800x450/4973ff/ffffff?text=NxtForm+AI+-+Prompt+Builder)
   *Intuitive workspace for typing form descriptions and generating live form schemas.*

3. **Step-by-Step Form Filling UI**
   ![Form Filling View](https://via.placeholder.com/800x450/f5f7fb/172033?text=NxtForm+AI+-+Form+Filling+Interface)
   *Polished, distraction-free filling view optimized across screen sizes.*

---

## 🛠️ Future Enhancements

- [ ] **Rich Answer Formats**: Add support for file uploads, ratings, signatures, and date selectors.
- [ ] **Advanced Analytics & Charts**: Integrate Recharts to map response distribution, user conversion funnels, and survey trends.
- [ ] **Conditional Logic Rules**: Create custom branching paths (e.g., *if question 1 is "Yes", go to question 3*).
- [ ] **Multi-LLM Integration**: Offer options to generate forms using Anthropic Claude, OpenAI GPT-4, and Google Gemini models.
- [ ] **Interactive Theme Builder**: Customize backgrounds, brand color schemes, fonts, and roundness profiles for forms.

---

## 📄 License

Distributed under the MIT License. See [LICENSE](LICENSE) for more information.
