
# Hi, I'm Vipul! 👋

# React Typescript Setup

Setup you React App from scratch without using  ``` create-react-app ``` so, We can learn background working and Depandancy. In this Tutorial we will setup React App using two methods one from scratch and another using Vit template.

## Methods
- React from scratch (Typescript,Webpack and Babel).
- Vite Template.

## React from scratch (Typescript,Webpack and Babel).
- **Step 1:** Install Node js in your System. [Download Link](https://nodejs.org/en/download) If you already install nodejs in you system Kindly skip this Step.
- **Step 2:** Use any Code editor as per your requirement. I prefer VS code. [Download Link](https://code.visualstudio.com/download).
- **Step 3:** Create a folder and named as your application and open it in Vscode.
- **Step 4:** initialized Nodejs use command ```npm init --y``` this command create ```package.json``` file which will store all the information regarding of dependancy in you application.
    > **Note** If you don't know how to open Command line in vs code use Key ```ctrl + ` ```
- **Step 5:** Create two folder named as ```src``,```public```  and ```build```.
- **Step 6:** Inside ```public``` folder create a file name ```index.html``` and use html Boilerplate code show below:

    ```
    //index.html
    
    <!DOCTYPE html>
    <html lang="en">
      <head>
          <meta charset="UTF-8" />
          <meta http-equiv="X-UA-Compatible" content="IE=edge" />
          <meta name="viewport" content="width=device-width, initial-scale=1.0" />
          <title>Document</title>
      </head>
      <body>
          <div id="root"></div>
      </body>
    </html>
    ```
- **Step 7:** Inside ```src``` folder create 2 folder named as ```index.tsx``` and ```App.tsx``` write following code:
   ```
   // index.tsx
   
   import * as ReactDOM from "react-dom";
   import App from "./App";

   ReactDOM.render(<App />, document.getElementById("root"));
   ```
   
   ```
   // App.tsx
   import "./style.css";
   export default function App() {
        return <div className="test">React Typescript From Scratch</div>;
    }
    ```
- **Step 8:** Install **React** library use following command
  ```
  npm install react react-dom
  ```
- **Step 9:** Install **Babel** library use folllowing command
  ```
  npm install @babel/core @babel/cli @babel/preset-env @babel/preset-react @babel/preset-typescript babel-loader
  ```
  - Create a file name ```.babelrc``` copy following command:
    ```
        {
      "presets": [
        "@babel/preset-env",
        [
          "@babel/preset-react",
          {
            "runtime": "automatic"
          }
        ],
        "@babel/preset-typescript"
      ],
      "plugins": [
        [
          "@babel/plugin-transform-runtime",
          {
            "regenerator": true
          }
        ]
      ]
    }

    ```
  - If we want additional support for async/awaits, we will need to add two additional libraries.
   ```
    npm install  @babel/runtime  @babel/plugin-transform-runtime
   ```
  > **Note** For More details refer [Babel Document](https://babeljs.io/docs/)
- **Step 10:**  Install **Webpack** Library using following command: 
  ```
  npm install webpack webpack-cli webpack-dev-server html-webpack-plugin clan-webpack-plugin
  ```
  - Create a file name ```webpack.config.js``` copy the following code.
    ```
        const path = require("path");
    const HtmlWebpackPlugin = require("html-webpack-plugin");
    const { CleanWebpackPlugin } = require("clean-webpack-plugin");

    module.exports = {
      entry: path.resolve(__dirname, "src", "index.tsx"),
      output: {
        path: path.resolve(__dirname, "build"),
        filename: "bundle.js",
      },
      mode: "development",
      module: {
        rules: [
          {
            test: /\.[jt]sx?$/,
            use: ["babel-loader"],
            exclude: /node_modules/,
          },
          {
            test: /\.css$/,
            use: ["style-loader", "css-loader"],
          },
          {
            test: /\.scss$/,
            use: ["style-loader", "css-loader", "sass-loader"],
          },
          {
            test: /\.(?:ico|gif|png|jpg|jpeg)$/i,
            type: "asset/resource",
          },
          {
            test: /\.(woff(2)?|eot|ttf|otf|svg|)$/,
            type: "asset/inline",
          },
        ],
      },
      resolve: {
        extensions: [".tsx", ".ts", ".js", ".jsx"],
      },
      plugins: [
        new HtmlWebpackPlugin({
          template: path.resolve(__dirname, "./public/index.html"),
        }),
        new CleanWebpackPlugin(),
      ],
      devServer: {
        static: path.join(__dirname, "./src"),
        port: 3001,
        hot: "only",
        compress: true,
        open: true,
      },
    };

    ```
   > **Note** To Know more about above code refer [Webpack Document](https://webpack.js.org/concepts/)

- **Step 11:** Install **Typescript** Follow below instruction:
   - First install typescript in your local system. If already install typescript in your system skip first command below. 
   ```
   npm install -g typescript
   ```
   - use command to install required library ```npm install @types/react @types/react-dom```
   - To setup Config file for typescript can be done using two methods 
      1. using command line use command ```tsc --init``` this command create a file ```tsconfig.json``` file which you can edit.
      2. Manualy copy the following code and create file ```tsconfig.json```.
      ```
            {
        "compilerOptions": {
          "target": "ES5" /* Specify ECMAScript target version: 'ES3' (default), 'ES5', 'ES2015', 'ES2016', 'ES2017', 'ES2018', 'ES2019', 'ES2020', or 'ESNEXT'. */,
          "module": "ESNext" /* Specify module code generation: 'none', 'commonjs', 'amd', 'system', 'umd', 'es2015', 'es2020', or 'ESNext'. */,
          "moduleResolution": "node" /* Specify module resolution strategy: 'node' (Node.js) or 'classic' (TypeScript pre-1.6). */ /* Type declaration files to be included in compilation. */,
          "lib": [
            "DOM",
            "ESNext"
          ] /* Specify library files to be included in the compilation. */,
          "jsx": "react-jsx" /* Specify JSX code generation: 'preserve', 'react-native', 'react' or 'react-jsx'. */,
          "noEmit": true /* Do not emit outputs. */,
          "isolatedModules": true /* Transpile each file as a separate module (similar to 'ts.transpileModule'). */,
          "esModuleInterop": true /* Enables emit interoperability between CommonJS and ES Modules via creation of namespace objects for all imports. Implies 'allowSyntheticDefaultImports'. */,
          "strict": true /* Enable all strict type-checking options. */,
          "skipLibCheck": true /* Skip type checking of declaration files. */,
          "forceConsistentCasingInFileNames": true /* Disallow inconsistently-cased references to the same file. */,
          "resolveJsonModule": true,
          "allowJs": true /* Allow javascript files to be compiled. Useful when migrating JS to TS */,
          "checkJs": true /* Report errors in .js files. Works in tandem with allowJs. */
        },
        "include": ["src/**/*"],
        "exclude": ["node_modules", "build"] // *** The files to not type check ***
      }
     ``` 
        
    > **Warning** <br>Don't forgot to build typescript config after edit for that use key ``` ctrl + shift + b ``` and click enter.
    <br> For more details refer [Typescript Documentation](https://www.typescriptlang.org/tsconfig).

- **Step 12:** Add Script in ```package.json``` inside you will find an attribute name ```scripts`` inside paste following code:
  ```
  "start": "webpack serve --config webpack.config.js --env env=development",
  "build": "webpack --config webpack.config.js --env env=prod --mode production ",
  ```
 - **Step 13:** Install loader for style and css use command ```npm install style-loader css-loader```.
 - **Step 14:** Now you can run your react application using command ```npm start```
 
 ## Vite Template
 
- **Step 1:** Install Node js in your System. [Download Link](https://nodejs.org/en/download) If you already install nodejs in you system Kindly skip this Step.
- **Step 2:** Use any Code editor as per your requirement. I prefer VS code. [Download Link](https://code.visualstudio.com/download).
- **Step 3:** Create a folder and named as your application and open it in Vscode.
    > **Note** If you don't know how to open Command line in vs code use Key ```ctrl + ` ```
- **Step 4:** To setup react typescript using vite use following command:
  ```
  npm create vite@latest my-vue-app -- --template react-ts
  ```
  > **Note** Specified you application name instead of ```my-react-app```

- **Step 5:** After runing above code it will create folder as you application name open that folder using vs code and write following command one by one:
  ```
  npm install 
  npm run dev
  ```
 > **Note** Refer document for more Detail  [Vite Documentation](https://vitejs.dev/guide/).
