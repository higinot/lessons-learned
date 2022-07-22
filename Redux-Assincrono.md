# Redux Assincrono (Redux-thunk)

Tal pacote provê uma interface simples para dar suporte a action creators que geram actions assíncronas, e é ele que você aprenderá para tornar sua aplicação mais completa.

Primeiramente você precisa installar a biblioteca do redux-thunk

`npm install redux-thunk`

_Dica: Para usar o redux-thunk junto com o Redux Devtools é preciso passar o applyMiddleware(thunk) como parâmetro para a função composeWithDevTools, como no exemplo a seguir:_

### Store

```
import { createStore, applyMiddleware } from 'redux';
import { composeWithDevTools } from 'redux-devtools-extension';
import reducer from './reducer';
import thunk from 'redux-thunk'

const store = createStore(
  reducer,
  composeWithDevTools(applyMiddleware(thunk))
);

export default store;
```
---

### Action Assincrona

Para ser devidamente usada pelo redux-thunk a action creator precisa retornar uma função, que pode fazer uso de dispatch e getState da store como parâmetros. Segue um exemplo de uma action creator definida em conformidade com tal contrato:

```
export const REQUEST_MOVIES = 'REQUEST_MOVIES';
export const RECEIVE_MOVIES = 'RECEIVE_MOVIES';

// action creator que retorna um objeto, que você tem feito até então
const requestMovies = () => ({
  type: REQUEST_MOVIES});

// outro action creator que retorna um objeto, que você tem feito até então
const receiveMovies = (movies) => ({
  type: RECEIVE_MOVIES,
  movies});

// action creator que retorna uma função, possível por conta do pacote redux-thunk
export function fetchMovies() {
  return (dispatch) => { // thunk declarado
    dispatch(requestMovies());
    return fetch('alguma-api-qualquer.com')
      .then((response) => response.json())
      .then((movies) => dispatch(receiveMovies(movies)));
  };
}

// componente onde você usaria a action creator fetchMovies assíncrona como uma outra qualquer
...
class MyConectedAppToRedux extends Component {
  ...
  componentDidMount() {
    const { dispatch, fetchMovies } = this.props;
    dispatch(fetchMovies()); // enviando a action fetchMovies
  }
  ...
}
...
```

Em síntese, um thunk nada mais é do que uma action que, quando despachada, faz uma requisição assíncrona e aguarda o resultado da requisição, podendo disparar uma ação em caso de sucesso (tratando as informações recebidas) ou disparando outra ação em caso de falha para buscar a informação.

<img src="https://assets.app.betrybe.com/front-end/redux/react-with-redux-part-2/fluxo-de-dados-redux-thunk-503390ec7a1e1f2b3205c45ea9d4cbfa.gif" style="width: 50%s;"> 

## Criando Action Assincrona

Primeiro precisamos criar uma action para o JSON:

`export const actionJson = (json) => ({ type: 'JSON_ACTION', payload: json.message });`

Depois precisamos criar uma action para a requisição

`export const actionRequest = () => ({ type: 'REQUEST_IMAGE'})`

Por ultima uma action para caso ocorra um erro:

`export const actionFailed = () => ({
  type: "FAILED_REQUEST",
});
`

Para concluir a chamada de uma API no Redux, precisamos criar uma função para implementar a logíca.

```
export function fetchAction() {
  return (dispatch) => {
    dispatch(actionRequest());
    return fetch("https://dog.ceo/api/breeds/image/random")
      .then((response) => response.json())
      .then((json) => dispatch(actionJson(json)))
      .catch((error) => dispatch(actionFailed(error)));
  };
}
```

## Pastas 

### Redux\store.js

```
import { createStore, applyMiddleware } from 'redux';
import { composeWithDevTools } from 'redux-devtools-extension';
import myReducer from './reducer';
import thunk from 'redux-thunk'

const store = createStore(
  myReducer,
  composeWithDevTools(applyMiddleware(thunk))
);

export default store;
```

### Redux\reducer.js

```
const INITIAL_STATE = {
  isFetching: false,
  imagePath: "",
  error: "",
};

function myReducer(state = INITIAL_STATE, action) {
  switch (action.type) {
    case "REQUEST_ACTION":
      return { ...state, isFetching: true };
    case "JSON_ACTION":
      return { ...state, imagePath: action.payload, isFetching: false };
    case "FAILED_ACTION":
      return { ...state, error: action.payload, isFetching: false };
    default:
      return state;
  }
}

export default myReducer;
```

### Redux\action.js

```
export const actionJson = (json) => ({
  type: "JSON_ACTION",
  payload: json.message,
});

export const actionRequest = () => ({ type: "REQUEST_ACTION" });

export const actionFailed = () => ({
  type: "FAILED_ACTION",
});

export function fetchAction() {
  return (dispatch) => {
    dispatch(actionRequest());
    return fetch("https://dog.ceo/api/breeds/image/random")
      .then((response) => response.json())
      .then((json) => dispatch(actionJson(json)))
      .catch((error) => dispatch(actionFailed(error)));
  };
}
```