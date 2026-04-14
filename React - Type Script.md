# REACT TypeScript Application

## Initialisation du projet

``` Bash
    npm create vite@latest <project name directory> -- --template react-ts
```

Exemples : 
pour créer l'application dans le répertoire courant
``` Bash
    npm create vite@latest . -- --template react-ts
```
ou
pour créer l'application dans le sous répertoire 'My-React-Project'
``` Bash
    npm create vite@latest My-React-Project -- --template react-ts
```

## Configure VS Code

Ajouter les extensions suivantes :
- ES7 + React/Redux/React-Native snippets (fourni des snippet pour générés les éléments REACT)
- ESLint (Ajoute une configuration supplémentaire à la compilation)
- PostCSS Language Support (Utilisé pour le postcss de tailwind)
- Tailwind CSS IntelliSense (pour l'auto completion dans VS Code lors de l'utilisation de Tailwind CSS)

## Ajouter Tailwind

La configuration peut changer attention [TailwindCss](https://tailwindcss.com/docs/installation/using-vite)

1. Installer le packager npm
``` bash
    npm install tailwindcss @tailwindcss/vite
```

2. Modifier le fichier vite.config.ts
``` TypeScript
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import tailwindcss from '@tailwindcss/vite'; //<-- ajoouter cette ligne

// https://vite.dev/config/
export default defineConfig({
  plugins: [
    react(),
    tailwindcss() //<-- ajoouter cette ligne
  ],
});
```

3. Modifier le fichier index.css en ajoutant ceci en première ligne
``` css
@import "tailwindcss";
```

4. Modifier le fichier App.tsx pour tester l'installation
``` TypeScript
const App = () => {
  return (
    <h1 className="text-3xl font-bold underline text-black">App</h1>
  );
};

export default App;
```

Résultat attendu :

![image](./Assets/Tailwind-css.png)

## Install DevExtreme

1. Installer [DevExtreme](https://js.devexpress.com/React/Documentation/Guide/React_Components/Add_DevExtreme_to_a_React_Application/)
``` bash
npm install devextreme@24.2 devextreme-react@24.2 --save --save-exact
```

2. importer le css dans main.tsx
``` TypeScript
import { StrictMode } from 'react';
import { createRoot } from 'react-dom/client';
import './index.css';
import 'devextreme/dist/css/dx.fluent.blue.light.css'; //<-- Cette ligne
import App from './App.tsx';

createRoot(document.getElementById('root')!).render(
  <StrictMode>
    <App />
  </StrictMode>,
)
```

3. Tester l'installation avec app.tsx
``` TypeScript
import Button from 'devextreme-react/button';

const App = () => {
    const sayHelloWorld = () => {
        alert('Hello world!');
    };

  return (
    <>
      <h1 className="text-3xl font-bold underline text-black">App</h1>
      <Button text="Click me" onClick={sayHelloWorld} />
    </>
  )
}

export default App
```
Resultat attendu :

![Resultat](./Assets/DevExtreme.png)

## Installer le React-Router-Dom

1. Installer le package via npm :
``` bash
npm install react-router-dom
```

2. Configurer les routes dans main.tsx
``` TypeScript
import { StrictMode } from 'react';
import { createRoot } from 'react-dom/client';
import './index.css';
import 'devextreme/dist/css/dx.fluent.blue.light.css';
import App from './App.tsx';
import { createBrowserRouter, RouterProvider } from 'react-router-dom';
import { HomeLayout } from './pages/index.ts';

const router = createBrowserRouter([ 
    { path: '/', element: <HomeLayout />},
    { path: '/test', element: <App />}
  ]);

createRoot(document.getElementById('root')!).render(
  <StrictMode>
    <RouterProvider router={router} />
  </StrictMode>,
);
```

Contenu de index.ts
``` TypeScript
export { default as  HomeLayout } from "./HomeLayout";
```
Contenu de HomeLayout.tsx
``` TypeScript
const HomeLayout = () => {
  return (
    <div>HomeLayout</div>
  );
};

export default HomeLayout;
```