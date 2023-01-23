# CalculadoraReact.
Calculadora básica creada con React.

//App.js.
import './App.css';
import Boton from './componentes/boton';
import Pantalla from './componentes/pantalla';
import BotonClear from './componentes/boton-clear';
import { useState } from 'react';
import { evaluate } from 'mathjs';

function App() {

  const [input, setInput] = useState(''); 

  const agregarInput = val => {
    setInput(input+val);
  };

  const calcularResultado = () => {
    if (input) {
      setInput(evaluate(input))
    } else {
      alert ("Por favor ingrese valores para realizar los cálculos.");
    }
  };

  return (
    <div className="App">
      <div className='contenedor-calculadora'>
        <Pantalla input = {input} />
        <div className='fila'>
          <Boton manejarClic = {agregarInput}>1</Boton>
          <Boton manejarClic = {agregarInput}>2</Boton>
          <Boton manejarClic = {agregarInput}>3</Boton>
          <Boton manejarClic = {agregarInput}>+</Boton>
        </div>
        <div className='fila'>
          <Boton manejarClic = {agregarInput}>4</Boton>
          <Boton manejarClic = {agregarInput}>5</Boton>
          <Boton manejarClic = {agregarInput}>6</Boton>
          <Boton manejarClic = {agregarInput}>-</Boton>
        </div>
        <div className='fila'>
          <Boton manejarClic = {agregarInput}>7</Boton>
          <Boton manejarClic = {agregarInput}>8</Boton>
          <Boton manejarClic = {agregarInput}>9</Boton>
          <Boton manejarClic = {agregarInput}>*</Boton>
        </div>
        <div className='fila'>
          <Boton manejarClic = {calcularResultado }>=</Boton>
          <Boton manejarClic = {agregarInput}>0</Boton>
          <Boton manejarClic = {agregarInput}>.</Boton>
          <Boton manejarClic = {agregarInput}>/</Boton>
        </div>
        <div className='fila'>
          <BotonClear manejarClear = {() => setInput('')}>
            Borrar
          </BotonClear>
        </div>
      </div>
    </div>
  );
}

export default App; 

/*App.css*/
.App{
  height: 100vh;
  padding-top: 15px;
  font-family: Arial, Helvetica, sans-serif;
  background-color: black;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.contenedor-calculadora{
  width: 400px;
  height: 600px;
  padding: 14px;
  background-color: #99c9ff;
  border-radius: 20px;
  border: 5px solid white;
  margin-bottom: 15px;
}

.fila{
  margin: 4px;
  display: flex;
  align-items: center;
  justify-content: center;
}

@media(max-width: 700px) {
  .App{
    height: 100vh;
    padding-top: 15px;
    font-family: Arial, Helvetica, sans-serif;
    background-color: blue;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    text-align: center;
  }
}

@media(max-width: 400px) {
  .App{
    width: 360px;
    height: 270px;
    padding-top: 10px;
    font-family: Arial, Helvetica, sans-serif;
    background-color: red;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    text-align: center;
  }
}

//Boton.js
import React from 'react';
import '../estilos/boton.css';

function Boton(props) {

  const esOperador = valor => {
    return isNaN(valor) && (valor !== '.') && (valor !== '=');
  };

  return(
    <div
      className={`boton-contenedor ${esOperador(props.children) ? 'operador' : ''}`.trimEnd()}
      onClick = {() => props.manejarClic (props.children)}>
      {props.children}
    </div>
  );
}

export default Boton;  

/*Boton.css*/
.boton-contenedor{
  height: 83px;
  flex: 1 1; /*Se expande según los componentes cercanos.*/
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 38px;
  background-color: #1b1b32;
  font-weight: bold;
  color: white;
  border-radius: 25px;
  border: 2px solid white;
  margin: 4px;
  cursor: pointer;
  user-select: none;
}

.boton-contenedor:hover{
  background-color: aqua;
}

.operador{
  background-color: #00471b;
}

.operador:hover{
  background-color: yellowgreen;
}

// Boton-clear.js.
import React from 'react';
import '../estilos/boton-clear.css';

const BotonClear = (props) => ( 
  <div className='boton-clear' onClick = {props.manejarClear}>
    {props.children}
  </div>
);

export default BotonClear;  

/*Boton-clear.css*/
.boton-clear{
  height: 80px;
  font-size: 1.6em;
  display: flex;
  flex: 1;
  background-color: #ac0246;
  margin-top: 8px;
  justify-content: center;
  align-items: center;
  font-weight: bold;
  color: white;
  border: 2px solid white;
  border-radius: 45px;
  cursor: pointer;
}

.boton-clear:hover{
  background-color: yellowgreen;
}

//Pantalla.js
import React from 'react';
import '../estilos/pantalla.css';

const Pantalla = ({ input }) => {
  return(
    <div className='input'>
      {input}
    </div>
  )
};

export default Pantalla;

/*Pantalla.css*/
.input{
    height: 75px;
    border-radius: 50px;
    margin-bottom: 20px;
    display: flex;
    justify-content: flex-end;
    align-items: center;
    font-weight: bold;font-size: 30px;
    background-color: #0a0a23;
    color: white;
    padding: 11px 30px 11px 11px;
    margin: 1px solid #888;
    box-shadow: -1px 4px 1px 1px white;
}

//Index.js
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);

//Package.json
{
  "name": "calculadora",
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "@testing-library/jest-dom": "^5.16.5",
    "@testing-library/react": "^13.4.0",
    "@testing-library/user-event": "^13.5.0",
    "mathjs": "^11.5.0",
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-scripts": "5.0.1",
    "web-vitals": "^2.1.4"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },
  "eslintConfig": {
    "extends": [
      "react-app",
      "react-app/jest"
    ]
  },
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  }
}
