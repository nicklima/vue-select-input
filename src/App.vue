<template>
  <div id="app">
    <div class="fancySelect up" :class="choice1.isActive && 'active'">
      <div class="selectedOption" @click="choice1.isActive = !choice1.isActive">
        <span>
          {{ choice1.value }}
        </span>
      </div>
      <div class="dropdown">
        <ul class="dropdown_list">
          <li
            v-for="(el, idx) in choices"
            :key="`selectOne_${idx}`"
            :class="`Item ${el + 1}` === choice1.value && 'selected'"
          >
            <span @click="changeChoice(choice1, `Item ${el + 1}`)">
              <i class="icon-envelope icon-large"></i>
              {{ `Item ${el + 1}` }}
            </span>
          </li>
        </ul>
      </div>
    </div>
    <div class="fancySelect" :class="choice2.isActive && 'active'">
      <div class="selectedOption" @click="choice2.isActive = !choice2.isActive">
        <span>
          {{ choice2.value }}
        </span>
      </div>
      <div class="dropdown">
        <ul class="dropdown_list">
          <li
            v-for="(el, idx) in choices"
            :key="`selectOne_${idx}`"
            :class="`Item ${el + 1}` === choice2.value && 'selected'"
          >
            <span @click="changeChoice(choice2, `Item ${el + 1}`)">
              <i class="icon-envelope icon-large"></i>
              {{ `Item ${el + 1}` }}
            </span>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      choices: Array.from({ length: 10 }, (v, k) => k),
      choice1: {
        isActive: false,
        value: "Select Option",
      },
      choice2: { isActive: false, value: "Select Option" },
    };
  },
  methods: {
    showDrop(el) {
      el.target.classList.toggle("active");
    },
    changeChoice(target, e) {
      target.value = e;
      target.isActive = !target.isActive;
    },
  },
};
</script>

<style>
*,
*::before,
*::after {
  box-sizing: border-box;
}

body,
ul[class],
ol[class] {
  margin: 0;
}

ul[class],
ol[class] {
  list-style: none;
  padding: 0;
}

body {
  align-items: center;
  display: flex;
  font-family: "Montserrat", sans-serif;
  justify-content: center;
  line-height: 1.5;
  min-height: 100vh;
  scroll-behavior: smooth;
  text-rendering: optimizeSpeed;
}

/* SELECT */
.fancySelect {
  background: #fff;
  border: 1px solid rgba(0, 0, 0, 0.15);
  border-radius: 5px;
  box-shadow: 0 1px 1px rgba(50, 50, 50, 0.1);
  color: #de5bbc;
  cursor: pointer;
  font-weight: bold;
  margin: 0 auto;
  margin-bottom: 30px;
  outline: none;
  position: relative;
  width: 200px;
}

.fancySelect.up {
  z-index: 6;
}

.fancySelect.active .dropdown {
  opacity: 1;
  pointer-events: auto;
}

.selectedOption {
  display: block;
  font-weight: 400;
  padding: 15px 10px;
  position: relative;
}

.selectedOption:after {
  border-color: #de5bbc transparent;
  border-style: solid;
  border-width: 6px 6px 0 6px;
  content: "";
  height: 0;
  margin-top: -3px;
  position: absolute;
  right: 15px;
  top: 50%;
  width: 0;
}

/* DROPDOWN LIST */
.dropdown {
  background: white;
  border: 1px solid rgba(0, 0, 0, 0.17);
  border-radius: inherit;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.1);
  font-weight: normal;
  left: 0;
  list-style: none;
  opacity: 0;
  padding: 5px;
  position: absolute;
  pointer-events: none;
  right: 0;
  top: 140%;
  transition: all 0.5s ease-in;
  z-index: 5;
}

.dropdown:after {
  border-color: #fff transparent;
  border-style: solid;
  border-width: 0 6px 6px 6px;
  content: "";
  height: 0;
  position: absolute;
  bottom: 100%;
  right: 15px;
  width: 0;
}

.dropdown:before {
  border-color: rgba(0, 0, 0, 0.1) transparent;
  border-style: solid;
  border-width: 0 8px 8px 8px;
  bottom: 100%;
  content: "";
  height: 0;
  position: absolute;
  right: 13px;
  width: 0;
}

.dropdown_list {
  max-height: 240px;
  overflow-y: auto;
}

.dropdown_list::-webkit-scrollbar {
  width: 4px;
}

.dropdown_list::-webkit-scrollbar-track {
  background: #f5f5f5;
}

.dropdown_list::-webkit-scrollbar-thumb {
  background-color: #de5bbc;
  border-radius: 20px;
}

.dropdown_list li.selected span {
  background: #f3f8f8;
}

.dropdown_list li {
  margin: 0 5px;
}

.dropdown_list li span {
  border-top: 1px solid #e6e8ea;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 1);
  color: #8aa8bd;
  display: block;
  padding: 12px;
  text-decoration: none;
  transition: all 0.3s ease-out;
}

.dropdown_list li:first-child span {
  border: 0;
}

.dropdown_list li i {
  color: inherit;
  float: right;
}

.dropdown_list li:first-of-type a {
  border-radius: 7px 7px 0 0;
}

.dropdown_list li:last-of-type a {
  border: none;
  border-radius: 0 0 7px 7px;
}

/* HOVER STATE */
.dropdown_list li:hover span {
  background: #f3f8f8;
}
</style>
<!-- Selected Dropdown based on https://tympanus.net/codrops/2012/10/04/custom-drop-down-list-styling/ -->
