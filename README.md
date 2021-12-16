Projeto criado pelo [Create React App](https://github.com/facebook/create-react-app).

## Estrutura de pasta

Após clonar, se projeto será assim:

```
my-app/
  README.md
  node_modules/
  package.json
  public/
    index.html
    favicon.ico
  src/
    App.css
    App.js
    App.test.js
    index.css
    index.js
    logo.svg
```

## Scripts

### `npm start`

Roda o projeto em modo de desenvolvimento.<br>
Abra [http://localhost:3000](http://localhost:3000).

### `npm test`

Roda os testes.

### `npm run build`

Compila o app para produção na pasta `build`.<br>

## Importando o Componente

### `Button.js`

```js
import React, { Component } from 'react';

class Button extends Component {
  render() {
    // ...
  }
}

export default Button; // Don’t forget to use export default!
```

### `DangerButton.js`

```js
import React, { Component } from 'react';
import Button from './Button'; // Import a component from another file

class DangerButton extends Component {
  render() {
    return <Button color="red" />;
  }
}

export default DangerButton;
```

## Code Splitting

Here is an example:

### `moduleA.js`

```js
const moduleA = 'Hello';

export { moduleA };
```

### `App.js`

```js
import React, { Component } from 'react';

class App extends Component {
  handleClick = () => {
    import('./moduleA')
      .then(({ moduleA }) => {
        // Use moduleA
      })
      .catch(err => {
        // Handle failure
      });
  };

  render() {
    return (
      <div>
        <button onClick={this.handleClick}>Load</button>
      </div>
    );
  }
}

export default App;
```

This will make `moduleA.js` and all its unique dependencies as a separate chunk that only loads after the user clicks the 'Load' button.

You can also use it with `async` / `await` syntax if you prefer it.

## Adicionando estilos

### `Button.css`

```css
.Button {
  padding: 20px;
}
```

### `Button.js`

```js
import React, { Component } from 'react';
import './Button.css'; // Tell Webpack that Button.js uses these styles

class Button extends Component {
  render() {
    // You can use them as regular CSS styles
    return <div className="Button" />;
  }
}
```

## Adicionando estilos CSS

### `Button.module.css`

```css
.error {
  background-color: red;
}
```

### `another-stylesheet.css`

```css
.error {
  color: red;
}
```

### `Button.js`

```js
import React, { Component } from 'react';
import styles from './Button.module.css'; // Import css modules stylesheet as styles
import './another-stylesheet.css'; // Import regular stylesheet

class Button extends Component {
  render() {
    // reference as a js object
    return <button className={styles.error}>Error Button</button>;
  }
}
```

### Result

No clashes from other `.error` class names

```html
<!-- This button has red background but not red text -->
<button class="Button_error_ax7yz"></div>
```

## Adicionando estilos SASS

Para usar Sass, primeiro instale `node-sass`:

```bash
$ npm install node-sass --save
$ # or
$ yarn add node-sass
```

Agora é preciso renomear `src/App.css` to `src/App.scss` e `src/App.js` para importar `src/App.scss`.

Para compartilhar variáveis entre arquivos SASS, você poderá usar `@import "./shared.scss";`.

```scss
@import 'styles/_colors.scss'; // assuming a styles directory under src/
@import '~nprogress/nprogress'; // importing a css file from the nprogress node module
```
