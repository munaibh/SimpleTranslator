<template>
  <div id="app">
    <translate-input></translate-input>
    <translate-output></translate-output>
  </div>
</template>

<script>
import TranslateInput from './components/TranslateInput.vue'
import TranslateOutput from './components/TranslateOutput.vue'

export default {
  name: 'app',
  components: {
    TranslateOutput,
    TranslateInput
  }
}
</script>

<style>
:root {
  font-size: 16px;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Roboto';
  font-size: 1rem;
  overflow: hidden;
}

section {
  width: 100vw;
  height: 50vh;
  transition: height 0.5s ease;
  will-change: height;
}
section.large {
  height: 100vh;
}
section [class*='__inner'] {
  width: 90%;
  height: 100%;
  margin: 0 auto;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.input {
  background: #0497ea;
}

.output {
  background: white;
}

form {
  max-width: 800px;
  width: 100%;
}
form input {
  width: 100%;
  line-height: 2.571em;
  background: transparent;
  border: 0;
  color: white;
  font-size: 2.188rem;
  border-bottom: 0.05714em solid #bbc7ce;
  outline: 0;
  font-family: 'Roboto';
  font-weight: 300;
  transition: all 0.3s ease;
  margin-bottom: 1.571em;
}
form input:focus {
  border-color: white;
}
form input::placeholder {
  color: #015788;
}
form button {
  display: none;
}

.filter__active {
  font-weight: 300;
  font-size: 1.25rem;
  text-decoration: none;
  color: white;
  display: block;
  position: relative;
  padding-right: 1.25em;
  line-height: 1.5em;
}
.filter__active:hover:after {
  transform: rotate(180deg);
}
.filter__active::after {
  content: '';
  width: 0;
  border-left: 0.25em solid transparent;
  border-right: 0.25em solid transparent;
  border-top: 0.25em solid white;
  top: 50%;
  position: absolute;
  right: 0;
  transition: transform 0.35s ease;
}
.filter__btn {
  color: white;
  background: none;
  margin: 0 1.875rem;
  border: 0;
  cursor: pointer;
}
.filter__btn svg {
  width: 1.563rem;
  float: left;
  fill: #00466e;
}
.filter__item {
  position: relative;
  display: inline-block;
}
.filter__submenu {
  display: none;
  position: absolute;
  top: 100%;
  font-size: 1rem;
  list-style: none;
  padding: 0.625em 0;
  background: white;
  max-height: 300px;
  z-index: 19;
  overflow: auto;
  border: 1px solid #ccc;
}
.filter__link {
  display: block;
  word-wrap: normal;
  white-space: nowrap;
  padding: 0 0.9375em;
  color: black;
  text-decoration: none;
  line-height: 1.8rem;
}
.filter__link:hover {
  background: #1e90ff;
  color: white;
}

.filter__item:hover .filter__submenu {
  display: block;
}

.actions {
  margin-top: 1.5rem;
}

.btn {
  position: relative;
  text-decoration: none;
  border: 0;
  background: 0;
  font-family: 'Roboto', sans-serif;
  font-size: 1rem;
  cursor: pointer;
  padding: 0 10px;
  display: inline-block;
}
.btn svg {
  width: 25px;
  display: block;
  fill: #747474;
  pointer-events: none;
}
.btn:before {
  content: attr(data-tooltip);
  position: absolute;
  z-index: 2;
  font-size: 1em;
  font-weight: 300;
  top: -0.4125em;
  pointer-events: none;
  opacity: 0;
  left: 50%;
  transform: translate(-50%, -100%);
  display: block;
  background: red;
  transition: opacity 0.35s ease;
  padding: 0.5em 1em;
  border-radius: 0.2em;
  background: black;
  color: white;
}
.btn:after {
  content: '';
  width: 0;
  position: absolute;
  border-left: 0.3125em solid transparent;
  border-right: 0.3125em solid transparent;
  border-top: 0.3125em solid black;
  top: -0.1em;
  pointer-events: none;
  opacity: 0;
  left: 50%;
  transition: opacity 0.35s ease;
  transform: translate(-50%, -100%);
}
.btn:hover:before, .btn:hover:after {
  opacity: 1;
}

.result {
  font-size: 3.125rem;
  font-family: Roboto;
  font-weight: 400;
  text-align: center;
  word-break: break-all;
}

.result.loading {
  color: #b4b4b4
}

textarea {
  position: absolute;
  top: -100%;
  left: -100%;
}

.loader {
  width: 5rem;
  height: 5rem;
  background: rgba(255, 0, 0, 0);
  border: .5em solid #e1e1e1;
  border-top: .5em solid #0497ea;
  border-radius: 50%;
  animation: spin 1s ease-in-out infinite;
}

@keyframes spin {
  0% { transform: rotate(0deg);}
  100% { transform: rotate(360deg);}
}

@media screen and (max-width: 380px) {
  :root {
    font-size: 14px;
  }

  .filter__item {
    position: static;
  }

  .filter__submenu {
    left: 0;
    right: 0;
    top: 50%;
    width: 100%;
    border: 0;
    max-height: 50%;
    text-align: center;
    background: #015788;
    color: white;
    min-height: 50%;
  }
  .filter__submenu .filter__link {
    color: white;
    line-height: 3rem;
  }
}

</style>
