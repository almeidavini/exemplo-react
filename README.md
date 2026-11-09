# Tutorial: Construindo sua Primeira Aplicação React

Este guia passo a passo ajudará você a criar um projeto React do zero usando o Vite, criar rotas de navegação e entender a estrutura básica dos arquivos.

> **💡 Dica de Estudo:** Para aproveitar ao máximo este tutorial e realmente fixar a sintaxe do React, **evite copiar e colar**. Digite os comandos e os códigos manualmente no seu editor.

---

## 1. Criando o Projeto

No terminal do seu VS Code, navegue até a pasta onde deseja salvar o projeto e execute o comando abaixo. Ele cria a estrutura inicial já configurada pelo Vite:

*(Digite o comando abaixo no seu terminal)*
```bash
npm create vite@latest meu-projeto-react -- --template react
```

Em seguida, entre na pasta recém-criada e instale as dependências padrão:

*(Digite no terminal)*
```bash
cd meu-projeto-react
npm install
```

---

## 2. Entendendo os Arquivos Gerados

O Vite cria uma estrutura moderna e enxuta. Aqui estão as principais partes que você verá no painel lateral do seu editor:

* **`node_modules/`**: Pasta onde ficam as bibliotecas de terceiros (o código que o npm baixa). Nunca altere nada aqui.
* **`public/`**: Arquivos estáticos puros, como imagens básicas e o ícone da aba do navegador (favicon).
* **`index.html`**: A única página HTML real do projeto. Nela, existe uma `<div id="root"></div>` onde o React vai "injetar" toda a interface.
* **`package.json`**: O "documento de identidade" do projeto. Lista as dependências e comandos do terminal.
* **`vite.config.js`**: Configurações da ferramenta de build (Vite).
* **`src/main.jsx`**: O ponto de partida do código React. Ele pega o componente principal e o renderiza no HTML.
* **`src/App.jsx`**: O componente raiz. É aqui que vamos organizar as nossas rotas.

---

## 3. Instalando o Gerenciador de Rotas

Para criar o efeito de troca de telas (Login para Home) sem recarregar o navegador inteiro (comportamento de Single Page Application), usaremos a biblioteca padrão da comunidade, o **React Router**:

*(Digite no terminal)*
```bash
npm install react-router-dom
```

---

## 4. Criando as Telas (Componentes)

Dentro da pasta `src`, crie uma nova subpasta chamada `pages`. Vamos criar nossos dois arquivos de tela lá dentro.

### Arquivo 1: `src/pages/Login.jsx`

Esta tela simula um formulário de entrada. Quando o botão é clicado, o `useNavigate` nos redireciona para a página seguinte.

*(Crie o arquivo e digite o código abaixo)*
```jsx
import { useNavigate } from 'react-router-dom';

export default function Login() {
  const navigate = useNavigate();

  const handleLogin = (e) => {
    e.preventDefault(); // Evita o recarregamento padrão do formulário
    navigate('/home'); // Navega para a rota da Home
  };

  return (
    <div style={{ padding: '20px', textAlign: 'center' }}>
      <h1>Tela de Login</h1>
      <form onSubmit={handleLogin}>
        <div>
          <input type="text" placeholder="Usuário" style={{ margin: '10px', padding: '5px' }} />
        </div>
        <div>
          <input type="password" placeholder="Senha" style={{ margin: '10px', padding: '5px' }} />
        </div>
        <button type="submit" style={{ padding: '10px 20px', cursor: 'pointer' }}>
          Entrar
        </button>
      </form>
    </div>
  );
}
```

### Arquivo 2: `src/pages/Home.jsx`

A tela que será exibida após o login. Ela possui um botão simples para retornar à tela inicial.

*(Crie o arquivo e digite o código abaixo)*
```jsx
import { useNavigate } from 'react-router-dom';

export default function Home() {
  const navigate = useNavigate();

  const handleLogout = () => {
    navigate('/'); // Retorna para a raiz (Login)
  };

  return (
    <div style={{ padding: '20px', textAlign: 'center' }}>
      <h1>Bem-vindo à Home!</h1>
      <p>Você conseguiu acessar o sistema.</p>
      <button onClick={handleLogout} style={{ padding: '10px 20px', cursor: 'pointer' }}>
        Sair
      </button>
    </div>
  );
}
```

---

## 5. Configurando o Roteamento no App

Para finalizar a lógica, o React precisa saber qual componente exibir dependendo da URL do navegador. Substitua todo o conteúdo original do seu `src/App.jsx` por este código:

*(Edite o arquivo e digite o código abaixo)*
```jsx
import { BrowserRouter, Routes, Route } from 'react-router-dom';
import Login from './pages/Login';
import Home from './pages/Home';

function App() {
  return (
    <BrowserRouter>
      <Routes>
        {/* Quando a URL for apenas "/", exibe o Login */}
        <Route path="/" element={<Login />} />
        
        {/* Quando a URL for "/home", exibe a Home */}
        <Route path="/home" element={<Home />} />
      </Routes>
    </BrowserRouter>
  );
}

export default App;
```

---

## 6. Executando o Projeto

Com tudo configurado e salvo, inicie o servidor de desenvolvimento no terminal do VS Code:

*(Digite no terminal)*
```bash
npm run dev
```

O terminal exibirá um link local (geralmente `http://localhost:5173`). 
Segure a tecla **Ctrl** e clique no link para abri-lo no navegador. 

Teste preencher qualquer coisa no login e clicar em "Entrar". Você verá a transição imediata para a tela Home, totalmente gerenciada pelo React no frontend!
