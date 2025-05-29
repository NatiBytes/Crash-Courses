# How to build the docker image

- `docker build -t react-docker .` Note: the dot at the end indicated you are running this from the same dir as the docker

# How to run Docker the image in Docker Container

Note the port needs to be expose to our:
- Host machine
- And Vite because we are using Vite in out app

1. Update package.json 
  - From -> "dev": "vite",
  - To ->     "dev": "vite --host",

2.  Then run only one of the following command:   
  - `docker run -p 5173:5173 react-docker` With "5173:5173" we are mapping the container port to the port on our host machine
  - `docker run -p 5173:5173 -v "$(pwd):/app" react-docker` If you want any changes you make loaclly to sync. This tells docker to mount the current working directory where we run the docker run command into the app dir inside the container. This means our local code is linked to the container and any changes we make localy will be reflected inside the running container. $(pwd) - represents the current working dir and executes on run time to provide the currecnt dir path. and -v stands for volume, this is beacause we are creating a volume that will keep track of the changes
  - `docker run -p 5173:5173 -v "$(pwd):/app" -v /app/node_modules react-docker` Create a new volume mount for the modules dir with in the container. We do this to ensure when we plan to make changes to the dpendencies, this will insure those changes are avilable to our container from our local modules.
  

It is possible to run into issues where the chnges are not being reflected when using bind mount E.g. `docker run -p 5173:5173 -v "$(pwd):/app" react-docker`
- Possible fix - if running on windows make sure to use cmd or power shell. You're likely running this from Git Bash on Windows, which mangles volume paths when passed to Docker. This is a known issue and you can inspect the running container to see if the path is correct under "Mounts".
- On Powershell `docker run -it --rm -p 5173:5173 -v ${PWD}:/app react-docker`
- On cmd `docker run -it --rm -p 5173:5173 -v %cd%:/app react-docker `

# React + TypeScript + Vite

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react) uses [Babel](https://babeljs.io/) for Fast Refresh
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react-swc) uses [SWC](https://swc.rs/) for Fast Refresh

## Expanding the ESLint configuration

If you are developing a production application, we recommend updating the configuration to enable type-aware lint rules:

```js
export default tseslint.config({
  extends: [
    // Remove ...tseslint.configs.recommended and replace with this
    ...tseslint.configs.recommendedTypeChecked,
    // Alternatively, use this for stricter rules
    ...tseslint.configs.strictTypeChecked,
    // Optionally, add this for stylistic rules
    ...tseslint.configs.stylisticTypeChecked,
  ],
  languageOptions: {
    // other options...
    parserOptions: {
      project: ['./tsconfig.node.json', './tsconfig.app.json'],
      tsconfigRootDir: import.meta.dirname,
    },
  },
})
```

You can also install [eslint-plugin-react-x](https://github.com/Rel1cx/eslint-react/tree/main/packages/plugins/eslint-plugin-react-x) and [eslint-plugin-react-dom](https://github.com/Rel1cx/eslint-react/tree/main/packages/plugins/eslint-plugin-react-dom) for React-specific lint rules:

```js
// eslint.config.js
import reactX from 'eslint-plugin-react-x'
import reactDom from 'eslint-plugin-react-dom'

export default tseslint.config({
  plugins: {
    // Add the react-x and react-dom plugins
    'react-x': reactX,
    'react-dom': reactDom,
  },
  rules: {
    // other rules...
    // Enable its recommended typescript rules
    ...reactX.configs['recommended-typescript'].rules,
    ...reactDom.configs.recommended.rules,
  },
})
```
