## Redux em REACT

Redux é uma biblioteca que pode ser utilizada com React, Angular, Vue, Ember e JavaScript puro, para dar só alguns exemplos. É muito comum o uso de Redux com React, apesar de serem ferramentas independentes.

 No caso do React, a biblioteca React Redux é quem faz essa conexão e pode ser instalada em sua aplicação através do comando:

`npm install react-redux`

**React Redux** é a biblioteca oficial para realizar a conexão entre React e Redux.

<br>

---

<br>

## **Redux**

### Store

É onde vamos armazenar todos os dados compartilhados da aplicação e é representado por um objeto JavaScript. O State é armazenado no Store do Redux.

<br>

### Action 

É um objeto JavaScript que representa alguma mudança/alteração que precisa acontecer no State.

<br>

### Reducer

É uma função JavaScript que recebe o estado atual (current state) e a ação corrente (current action) e retorna um novo estado (new state). É responsabilidade dessa função decidir o que acontecerá com o estado dada uma ação(action).

<br>

### Dispatch

É uma função que envia uma ação (action) para processamento.

<br>

---

<br>

## Configurando Redux com React

<br>

### Configurando o Redux no React

Primeiro, criamos nossa aplicação React:

`npx create-react-app my-app`

Depois, instalamos as dependências:

`npm install redux`

e também:

`npm install react-redux`

---

### Store no React Redux

Em todos os projetos com React Redux você ira precisar criar um Store.

Primeiro você cria uma pasta para o Store:

\\src\\store\\store.js

```
import { createStore } from 'redux';
import { composeWithDevTools } from 'redux-devtools-extension';
import reducer from './reducer';

const store = createStore(
  reducer,
  composeWithDevTools()
);

export default store;

```

A função createStore sempre receberá como parâmetro um rootReducer. Portanto, deve-se criar um rootReducer no arquivo src/reducers/rootReducer.js.

---

### Redux Dev Tools Extension

_Dica: Para facilitar a utilização do Redux, recomendamos fortemente que você instale a extensão Redux Devtools. E adicione o pacote redux-devtools-extension com o seguinte comando: npm install --save redux-devtools-extension_

---

### Reducer e RootReducer

Como dito anteriormente, a função createStore precisa receber como parâmetro um rootReducer, que por sua vez recebe todos os reducers da aplicação como um objeto no parâmetro da função combineReducers.

#### **Reducer**

//Arquivo reducer.js 
```
const INITIAL_STATE = {
  state: '',
};

function myReducer(state = INITIAL_STATE, action) {
  switch (action.type) {
    case 'NEW_ACTION':
      return { state: action.state };
    default:
      return state;
  }
}

export default myReducer;
```
#### **RootReducer**
O método combineReducers que, como diz seu nome, combina reducers, deve receber um objeto com os reducers criados. Sem ele, só poderíamos usar um reducer em nossa aplicação.

_Dica: Mesmo que tenhamos apenas um reducer é uma boa prática que utilizemos o combineReducers, pois caso nossa aplicação cresça e necessite de mais de um reducer não será necessário alterar sua lógica._

//Arquivo RootReducer
```
import { combineReducers } from 'redux';
import myReducer from './myReducer';

const rootReducer = combineReducers({ myReducer });

export default rootReducer;
```

### Actions e Actions Creators

A action possui sempre uma propriedade type única. Essa propriedade é utilizada pelo Redux para identificar a ação que será realizada, esse conceito recebe o nome de action type.

```
export const newAction = (state) => ({ type: 'NEW_ACTION', state });
```

### Provider

Para utilizarmos o estado compartilhado que o Redux provê, precisamos trabalhar o src/index.js para adicionarmos a configuração do Provider.

```
import React from 'react';
import ReactDOM from 'react-dom';
// o provider é o meio pelo qual disponibilizamos o store
// com os estados de toda a aplicação para todos os demais componentes
import { Provider } from 'react-redux';
import './index.css';
import App from './App';
import store from './store';

ReactDOM.render(
  <Provider store={ store }>
    <App />
  </Provider>,
  document.getElementById('root'),
);
```

---
### mapStateToProps

A função mapStateToProps, auto-descritiva, mapeia as entidades armazenadas nos estados para uma props.

Ao implementar os componentes é preciso conectá-los ao Redux. Primeiramente é preciso importar e adicionar os componentes à página que precisará renderizar os mesmos.

```
const mapStateToProps = state => ({
  myFirstState: state.myReducer.state});
```

### Método Connect ()()

O método connect nos dá acesso a store do Redux. A sua estrutura se dá da seguinte forma: connect()().

Nos primeiros parênteses, devem estar presentes os métodos nativos do Redux. No caso de utilizar somente o mapDispatchToProps, o primeiro parâmetro desses parênteses deverá ser null, já no caso de utilizar somente o mapStateToProps, que veremos logo a frente, o segundo parâmetro desses parênteses deverá ser null. Portanto, no caso de utilizar ambos mapStateToProps e mapDispatchToProps, essa é a sintaxe que o connect apresentará:

No segundo parênteses, colocamos o componente que deverá ser conectado.

```
export default connect(mapStateToProps, mapDispatchToProps)(Component)
```

O método connect()() é utilizado para conectar o componente a store do Redux

### mapDispatchToProps

```
const mapDispatchToProps = (dispatch) => ({
  myFirstDispatch: (state) => dispatch(newAction(state))});
```

## Recapitulando o Redux React

Redux é uma biblioteca JavaScript de código aberto para gerenciar o estado do aplicativo.

Podemos utilizar ela em varias bibliotecas como React ou Angulas para criar interfaces de usuario.

### Passo a Passo Redux React

1. Como vamor trabalhar com React precisamos criar a aplicação com o comando `npx create-react-app nome-aplicacao `.
2. Depois precisamos instalar as bibliotecas para trabalhar com react e redux: `npm react react-redux`
3. Agora precisamos criar uma pasta para o redux `scr/redux`
4. Agora vamos criar as peças para conseguir utilizar o redux dentro do React, que são o Store, Reducer e Actions.
5. Primeiro vamos começar criando o Store, como padrão podemos utilizar o modelo abaixo:

_Como padrão já baixamos a aplicação para gerenciar o estado de redux no console, com o comando `npm install --save redux-devtools-extension` e colocar junto no store, conforme exemplo abaixo_

```
import { createStore } from 'redux';
import { composeWithDevTools } from 'redux-devtools-extension';
import reducer from './reducer';

const store = createStore(
  reducer,
  composeWithDevTools()
);

export default store;
```
6. Agora precisamos criar o Reducer, como padrão vamos utilizar o modelo abaixo.
```
const INITIAL_STATE = {
  state: '',
};

function myReducer(state = INITIAL_STATE, action) {
  switch (action.type) {
    case 'NEW_ACTION':
      return { state: action.state };
    default:
      return state;
  }
}

export default myReducer;
```
_Para projetos maiores, vamos precisar gerenciar varios estados e precisas de varios reducer, um para cada página e funcionalidade, nesses cassos vamos utilizar o rootReducer com o combineReduces, conforme exemplo abaixo:_

```
import { combineReducers } from 'redux';
import myReducer from './myReducer';

const rootReducer = combineReducers({ myReducer, segundoReducer, terceiroReducer });

export default rootReducer;
```

7.Agora precisamos criar uma action para conseguir acessar o dispatcher da aplicação Redux, como padrão vamos utilizar o modelo abaixo:
```
export const newAction = (state) => ({ type: 'NEW_ACTION', state });
```
_Para gerenciar os estados é recomendavél criar uma action para cada tipo de gerenciamento_

8.Agora você so precisa conectar sua aplicação global no Provider do react-redux, conforme modelo abaixo:
```
import React from 'react';
import ReactDOM from 'react-dom';
// o provider é o meio pelo qual disponibilizamos o store
// com os estados de toda a aplicação para todos os demais componentes
import { Provider } from 'react-redux';
import './index.css';
import App from './App';
import store from './store';

ReactDOM.render(
  <Provider store={ store }>
    <App />
  </Provider>,
  document.getElementById('root'),
);
```
**_Pronto!!! Sua aplicação já esta rodando com React-Redux_**

9. Agora temos duas funções para acessar as props(estados no redux) e atualizar, as funções são: 

#### **mapStateToProps**: _Acessa as props no Redux_

```
const mapStateToProps = state => ({
  myFirstState: state.myReducer.state});
```

#### **mapDispatchToProps**: _Atualiza as props no Redux_

```
const mapDispatchToProps = (dispatch) => ({
  myFirstDispatch: (state) => dispatch(newAction(state))});
```

10. Por fim você precisa usar a HOF **connect ()()**:

_Quando você não utilizar o mapStateToProps você precisa substituir a função por null_
```
export default connect(mapStateToProps, mapDispatchToProps)(Component)
```
