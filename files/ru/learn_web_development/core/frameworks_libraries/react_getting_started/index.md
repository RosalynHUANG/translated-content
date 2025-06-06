---
title: Начало работы с React
slug: Learn_web_development/Core/Frameworks_libraries/React_getting_started
---

{{LearnSidebar}}{{PreviousMenuNext("Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Main_features","Learn/Tools_and_testing/Client-side_JavaScript_frameworks/React_todo_list_beginning", "Learn/Tools_and_testing/Client-side_JavaScript_frameworks")}}

В этой статье мы скажем привет React. Мы узнаем немного подробностей о его происхождении и сценариях использования, настроим базовый набор инструментов на нашем локальном компьютере, а также создадим и поиграем с простым приложением для начинающих, и в процессе узнаем немного о том, как React работает .

| Что нужно знать: | [HTML](/ru/docs/Learn_web_development/Core/Structuring_content), [CSS](/ru/docs/Learn/CSS), и [JavaScript](/ru/docs/Learn/JavaScript), быть знакомым с [терминалом/командной строкой](/ru/docs/Learn/Tools_and_testing/Understanding_client-side_tools/Command_line).React использует синтаксис HTML-in-JavaScript под названием JSX (JavaScript и XML). Знание HTML и JavaScript поможет вам изучить JSX и лучше определить, связаны ли ошибки в вашем приложении с JavaScript или с более специфической областью React. |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Задача:          | Настроить локальную среду разработки React, создать стартовое приложение и понять основы его работы.                                                                                                                                                                                                                                                                                                                                                                                                                      |

## Привет React

Как гласит официальный слоган, [React](https://ru.reactjs.org/) - это библиотека для создания пользовательских интерфейсов. React не является фреймворком – он даже не рассчитан исключительно для web. Он используется для визуализации и в связке с другими библиотеками. Например, [React Native](https://reactnative.dev/) можно использовать для создания мобильных приложений; [React 360](https://facebook.github.io/react-360/) можно использовать для создания приложений виртуальной реальности; помимо того есть и другие [варианты](https://github.com/chentsulin/awesome-react-renderer).

Для создания веб-приложений разработчики используют React в тандеме с [ReactDOM](https://reactjs.org/docs/react-dom.html). React and ReactDOM часто обсуждаются в том же пространстве и используются для решения тех же проблем, что и другие настоящие фреймворки для веб-разработки. Когда мы ссылаемся на React как на «фреймворк», мы подразумеваем это разговорное понимание.

Основная цель React - минимизировать ошибки, возникающие при разработке пользовательских интерфейсов. Это достигается за счёт использования компонентов - автономных логических фрагментов кода, которые описывают часть пользовательского интерфейса. А уже эти компоненты объединяются для создания полноценного пользовательского интерфейса. React абстрагирует большую часть работы по визуализации, оставляя вам возможность сосредоточиться на дизайне.

## Когда использовать

В отличие от других платформ, рассматриваемых в этом модуле, React не обязывает к строгим правилам в отношении соглашений о коде или организации файлов. Это позволяет командам договариваться, что для них более подходит, и структурировать React проект соответствующим образом. React может отвечать за одну кнопку, несколько частей или же весь пользовательский интерфейс приложения.

Хотя React _можно_ использовать для [небольших частей интерфейса](https://ru.reactjs.org/docs/add-react-to-a-website.html), «зайти» в него не так просто, как, к примеру, в jQuery, или даже во Vue. Куда легче это сделать создав всё приложение с помощью React.

Кроме того, такие преимущества React-приложения, как написание интерфейсов с помощью JSX, требуют процесса компиляции. Добавление на сайт компилятора Babel приводит к более медленному выполнению кода, поэтому такие инструменты обычно настраиваются для процесса сборки. Да, возможно, у React есть серьёзные требования к инструментарию, но его можно освоить.

В этой статье основное внимание будет уделено использованию React для создания всего пользовательского интерфейса с помощью [create-react-app](https://create-react-app.dev/), предоставляемого Facebook.

## Как React использует JavaScript?

React utilizes features of modern JavaScript for many of its patterns. Its biggest departure from JavaScript comes with the use of [JSX](https://reactjs.org/docs/introducing-jsx.html) syntax. JSX extends JavaScript's syntax so that HTML-like code can live alongside it. For example:

```js
const heading = <h1>Mozilla Developer Network</h1>;
```

This heading constant is known as a **JSX expression**. React can use it to render that [`<h1>`](/ru/docs/Web/HTML/Reference/Elements/Heading_Elements) tag in our app.

Suppose we wanted to wrap our heading in a [`<header>`](/ru/docs/Web/HTML/Reference/Elements/header) tag, for semantic reasons? The JSX approach allows us to nest our elements within each other, just like we do with HTML:

```js
const header = (
  <header>
    <h1>Mozilla Developer Network</h1>
  </header>
);
```

> [!NOTE]
> The parentheses in the previous snippet aren't unique to JSX, and don't have any effect on your application. They're a signal to you (and your computer) that the multiple lines of code inside are part of the same expression. You could just as well write the header expression like this:
>
> ```jsx
> const header = (
>   <header>
>     <h1>Mozilla Developer Network</h1>
>   </header>
> );
> ```
>
> However, this looks kind of awkward, because the [`<header>`](/ru/docs/Web/HTML/Reference/Elements/header) tag that starts the expression is not indented to the same position as its corresponding closing tag.

Of course, your browser can't read JSX without help. When compiled (using a tool like [Babel](https://babeljs.io/) or [Parcel](https://parceljs.org/)), our header expression would look like this:

```js
const header = React.createElement(
  "header",
  null,
  React.createElement("h1", null, "Mozilla Developer Network"),
);
```

It's _possible_ to skip the compilation step and use [`React.createElement()`](https://reactjs.org/docs/react-api.html#createelement) to write your UI yourself. In doing this, however, you lose the declarative benefit of JSX, and your code becomes harder to read. Compilation is an extra step in the development process, but many developers in the React community think that the readability of JSX is worthwhile. Plus, popular tooling makes JSX-to-JavaScript compilation part of its setup process. You don't have to configure compilation yourself unless you want to.

Because JSX is a blend of HTML and JavaScript, some developers find it intuitive. Others say that its blended nature makes it confusing. Once you're comfortable with it, however, it will allow you build user interfaces more quickly and intuitively, and allow others to better understand your code base at a glance.

To read more about JSX, check out the React team's [JSX In Depth](https://reactjs.org/docs/jsx-in-depth.html) article.

## Настройка вашего первого React приложения

There are many ways to use React, but we're going to use the command-line interface (CLI) tool create-react-app, as mentioned earlier, which expedites the process of developing a React application by installing some packages and creating some files for you, handling the tooling described above.

It's possible to [add React to a website without create-react-app](https://reactjs.org/docs/add-react-to-a-website.html) by copying some [`<script>`](/ru/docs/Web/HTML/Reference/Elements/script) elements into an HTML file, but the create-react-app CLI is a common starting point for React applications. Using it will allow you spend more time building your app, and less time fussing with setup.

### Requirements

In order to use create-react-app, you need to have [Node.js](https://nodejs.org/en/) installed. It's recommended that you use the long-term support (LTS) version. Node includes npm (the node package manager), and npx (the node package runner).

You may also use the Yarn package manager as an alternative, but we'll assume you are using npm in this set of tutorials. See [Package management basics](/ru/docs/Learn/Tools_and_testing/Understanding_client-side_tools/Package_management) for more information on npm and yarn.

If you're using Windows, you will need to install some software to give you parity with Unix/macOS terminal in order to use the terminal commands mentioned in this tutorial. **Gitbash** (which comes as part of the [git for Windows toolset](https://gitforwindows.org/)) or **[Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/about)** (**WSL**) are both suitable. See [Command line crash course](/ru/docs/Learn/Tools_and_testing/Understanding_client-side_tools/Command_line) for more information on these, and on terminal commands in general.

Also bear in mind that React and ReactDOM produce apps that only work on a fairly modern set of browsers — IE9+ by way of some polyfills. It is recommended that you use a modern browser like Firefox, Safari, or Chrome when working through these tutorials.

Also see the following for more information:

- ["What is npm" on nodejs.org](https://nodejs.org/en/knowledge/getting-started/npm/what-is-npm/)
- ["Introducing npx" on the npm blog](https://blog.npmjs.org/post/162869356040/introducing-npx-an-npm-package-runner)
- [The create-react-app documentation](https://create-react-app.dev/)

### Initializing your app

create-react-app takes one argument: the name you'd like to give your app. create-react-app uses this name to make a new directory, then creates the necessary files inside it. Make sure you `cd` to the place you'd like your app to live on your hard drive, then run the following in your terminal:

```bash
npx create-react-app moz-todo-react
```

This creates a `moz-todo-react` directory, and does several things inside it:

- Installs some npm packages essential to the functionality of the app.
- Writes scripts for starting and serving the application.
- Creates a structure of files and directories that define the basic app architecture.
- Initializes the directory as a git repository, if you have git installed on your computer.

> [!NOTE]
> If you have the yarn package manager installed, create-react-app will default to using it instead of npm. If you have both package managers installed and explicitly want to use NPM, you can add the flag `--use-npm` when you run create-react-app:
>
> ```bash
> npx create-react-app moz-todo-react --use-npm
> ```

create-react-app will display a number of messages in your terminal while it works; this is normal! This might take a few minutes, so now might be a good time to go make a cup of tea.

When the process is complete, `cd` into the `moz-todo-react` directory and run the command `npm start`. The scripts installed by create-react-app will start being served at a local server at localhost:3000, and open the app in a new browser tab. Your browser will display something like this:

![Screenshot of Firefox MacOS, open to localhost:3000, showing the default create-react-app application](default-create-react-app.png)

### Application structure

create-react-app gives us everything we need to develop a React application. Its initial file structure looks like this:

```
moz-todo-react
├── README.md
├── node_modules
├── package.json
├── package-lock.json
├── .gitignore
├── public
│   ├── favicon.ico
│   ├── index.html
│   └── manifest.json
└── src
    ├── App.css
    ├── App.js
    ├── App.test.js
    ├── index.css
    ├── index.js
    ├── logo.svg
    └── serviceWorker.js
```

The **`src`** directory is where we'll spend most of our time, as it's where the source code for our application lives.

The **`public`** directory contains files that will be read by your browser while you're developing the app; the most important of these is `index.html`. React injects your code into this file so that your browser can run it. There's some other markup that helps create-react-app function, so take care not to edit it unless you know what you're doing. You very much should change the text inside the [`<title>`](/ru/docs/Web/HTML/Reference/Elements/title) element in this file to reflect the title of your application. Accurate page titles are important for accessibility!

The `public` directory will also be published when you build and deploy a production version of your app. We won't cover deployment in this tutorial, but you should be able to use a similar solution to that described in our [Deploying our app](/ru/docs/Learn/Tools_and_testing/Understanding_client-side_tools/Deployment) tutorial.

The `package.json` file contains information about our project that Node.js/npm uses to keep it organized. This file is not unique to React applications; create-react-app merely populates it. You don't need to understand this file at all to complete this tutorial, however, if you'd like to learn more about it, you can read [What is the file `package.json`? on NodeJS.org](https://nodejs.org/en/knowledge/getting-started/npm/what-is-the-file-package-json/); we also talk about it in our [Package management basics](/ru/docs/Learn/Tools_and_testing/Understanding_client-side_tools/Package_management) tutorial.

## Изучаем наш первый React компонент — `<App/>`

In React, a **component** is a reusable module that renders a part of our app. These parts can be big or small, but they are usually clearly defined: they serve a single, obvious purpose.

Let's open `src/App.js`, since our browser is prompting us to edit it. This file contains our first component, `App`, and a few other lines of code:

```jsx
import React from "react";
import logo from "./logo.svg";
import "./App.css";

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer">
          Learn React
        </a>
      </header>
    </div>
  );
}
export default App;
```

The `App.js` file consists of three main parts: some [`import`](/ru/docs/Web/JavaScript/Reference/Statements/import) statements at the top, the `App` component in the middle, and an [`export`](/ru/docs/Web/JavaScript/Reference/Statements/export) statement at the bottom. Most React components follow this pattern.

### Import statements

The `import` statements at the top of the file allow `App.js` to use code that has been defined elsewhere. Let's look at these statements more closely.

```js
import React from "react";
import logo from "./logo.svg";
import "./App.css";
```

The first statement imports the React library itself. Because React turns the JSX we write into `React.createElement()`, all React components must import the `React` module. If you skip this step, your application will produce an error.

The second statement imports a logo from `'./logo.svg'`. Note the `./` at the beginning of the path, and the `.svg` extension at the end — these tell us that the file is local and that it is not a JavaScript file. Indeed, the `logo.svg` file lives in our source directory.

We don't write a path or extension when importing the `React` module — this is not a local file; instead, it is listed as a dependency in our `package.json` file. Be careful of this distinction as you work through this lesson!

The third statement imports the CSS related to our App component. Note that there is no variable name and no `from` directive. This particular import syntax is not native to JavaScript module syntax – it comes from Webpack, the tool create-react-app uses to bundle all our JavaScript files together and serve them to the browser.

### The `App` component

After the imports, we have a function named `App`. Whereas most of the JavaScript community prefers camel-case names like `helloWorld`, React components use pascal-case variable names, like `HelloWorld`, to make it clear that a given JSX element is a React component, and not a regular HTML tag. If you were to rename the `App` function to `app`, your browser would show you an error.

Let's look at App more closely.

```jsx
function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer">
          Learn React
        </a>
      </header>
    </div>
  );
}
```

The `App` function returns a JSX expression. This expression defines what your browser ultimately renders to the DOM.

Some elements in the expression have attributes, which are written just like in HTML, following a pattern of `attribute="value"`. On line 3, the opening [`<div>`](/ru/docs/Web/HTML/Reference/Elements/div) tag has a `className` attribute. This the same as the [`class`](/ru/docs/Web/HTML/Reference/Global_attributes/class) attribute in HTML, but because JSX is JavaScript, we can't use the word `class` – it's reserved, meaning JavaScript already uses it for a specific purpose and it would cause problems here in our code. A few other HTML attributes are written differently in JSX than they are in HTML too, for the same kind of reason. We'll cover them as we encounter them.

Take a moment to change the [`<p>`](/ru/docs/Web/HTML/Reference/Elements/p) tag on line 6 so that it reads "Hello, world!", then save your file. You'll notice that this change is immediately rendered in the development server running at `http://localhost:3000` in your browser. Now delete the [`<a>`](/ru/docs/Web/HTML/Reference/Elements/a) tag and save; the "Learn React" link will be gone.

Your `App` component should now look like this:

```jsx
function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>Hello, World!</p>
      </header>
    </div>
  );
}
```

### Export statements

At the very bottom of the `App.js` file, the statement `export default App` makes our `App` component available to other modules.

## Interrogating the index

Let's open `src/index.js`, because that's where the `App` component is being used. This file is the entry point for our app, and it initially looks like this:

```jsx
import React from "react";
import ReactDOM from "react-dom";
import "./index.css";
import App from "./App";
import * as serviceWorker from "./serviceWorker";

ReactDOM.render(<App />, document.getElementById("root"));

// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: https://bit.ly/CRA-PWA
serviceWorker.unregister();
```

As with `App.js`, the file starts by importing all the JS modules and other assets it needs to run. `src/index.css` holds global styles that are applied to our whole app. We can also see our `App` component imported here; it is made available for import thanks to the `export` statement at the bottom of `App.js`.

Line 7 calls React's `ReactDOM.render()` function with two arguments:

- The component we want to render, `<App />` in this case.
- The DOM element inside which we want the component to be rendered, in this case the element with an ID of `root`. If you look inside `public/index.html`, you'll see that this is a `<div>` element just inside the `<body>`.

All of this tells React that we want to render our React application with the `App` component as the root, or first component.

> [!NOTE]
> In JSX, React components and HTML elements must have closing slashes. Writing just `<App>` or just `<img>` will cause an error.

[Service workers](/ru/docs/Web/API/Service_Worker_API/Using_Service_Workers) are interesting pieces of code that help application performance and allow features of your web applications to work offline, but they're not in scope for this article. You can delete line 5, as well as lines 9 through 12.

Your final `index.js` file should look like this:

```jsx
import React from "react";
import ReactDOM from "react-dom";
import "./index.css";
import App from "./App";

ReactDOM.render(<App />, document.getElementById("root"));
```

## Переменные и свойства

Next, we'll use a few of our JavaScript skills to get a bit more comfortable editing components and working with data in React. We'll talk about how variables are used inside JSX, and introduce props, which are a way of passing data into a component (which can then be accessed using variables).

### Variables in JSX

Back in `App.js`, let's focus on line 9:

```js
<img src={logo} className="App-logo" alt="logo" />
```

Here, the `<img />` tag's `src` attribute value is in curly braces. This is how JSX recognizes variables. React will see `{logo}`, know you are referring to the logo import on line 2 of our app, then retrieve the logo file and render it.

Let's try making a variable of our own. Before the return statement of `App`, add `const subject = 'React';`. Your `App` component should now look like this:

```jsx
function App() {
  const subject = "React";
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>Hello, World!</p>
      </header>
    </div>
  );
}
```

Change line 8 to use our `subject` variable instead of the word "world", like this:

```jsx
function App() {
  const subject = "React";
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>Hello, {subject}!</p>
      </header>
    </div>
  );
}
```

When you save, your browser should display "Hello, React!" instead of "Hello, world!"

Variables are convenient, but the one we've just set doesn't make great use of React's features. That's where props come in.

### Component props

A **prop** is any data passed into a React component. Props are written inside component calls, and use the same syntax as HTML attributes — `prop="value"`. Let's open `index.js` and give our `<App/>` call its first prop.

Add a prop of `subject` to the `<App/>` component call, with a value of `Clarice`. When you are done, your code should look something like this:

```jsx
ReactDOM.render(<App subject="Clarice" />, document.getElementById("root"));
```

Back in `App.js`, let's revisit the App function itself, which reads like this (with the `return` statement shortened for brevity):

```js
function App() {
  const subject = "React";
  return (
    // return statement
  );
}
```

Change the signature of the `App` function so that it accepts `props` as a parameter. Just like any other parameter, you can put `props` in a `console.log()` to read it out to your browser's console. Go ahead and do that after your `subject` constant but before the `return` statement, like so:

```js
function App(props) {
  const subject = "React";
  console.log(props);
  return (
    // return statement
  );
}
```

Save your file and check your browser's JavaScript console. You should see something like this logged:

```js
Object { subject: "Clarice" }
```

The object property `subject` corresponds to the `subject` prop we added to our `<App />` component call, and the string `Clarice` corresponds to its value. Component props in React are always collected into objects in this fashion.

Now that `subject` is one of our props, let's utilize it in `App.js`. Change the `subject` constant so that, instead of defining it as the string `React`, you are reading the value of `props.subject`. You can also delete your `console.log()` if you want.

```js
function App(props) {
  const subject = props.subject;
  return (
    // return statement
  );
}
```

When you save, the the app should now greet you with "Hello, Clarice!". If you return to `index.js`, edit the value of `subject`, and save, your text will change.

## Резюме

This brings us to the end of our initial look at React, including how to install it locally, creating a starter app, and how the basics work. In the next article we'll start building our first proper application — a todo list. Before we do that, however, let's recap some of the things we've learned.

In React:

- Components can import modules they need, and must export themselves at the bottom of their files.
- Component functions are named with `PascalCase`.
- You can read JSX variables by putting them between curly braces, like `{so}`.
- Some JSX attributes are different to HTML attributes, so that they don't conflict with JavaScript reserved words. For example, `class` in HTML translates to `className` in JSX. Note that multi-word attributes are camel-cased.
- Props are written just like attributes inside component calls, and are passed into components.

{{PreviousMenuNext("Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Main_features","Learn/Tools_and_testing/Client-side_JavaScript_frameworks/React_todo_list_beginning", "Learn/Tools_and_testing/Client-side_JavaScript_frameworks")}}
