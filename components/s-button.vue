<script lang="ts" setup></script>

<template>
  <div class="hs-wrapper classic">
    <a class="hs-button classic">
      <span class="hs-border classic">
        <span class="hs-text classic">
          <slot>Text</slot>
        </span>
      </span>
    </a>
  </div>
</template>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Fondamento:ital@0;1&display=swap");

.hs-wrapper {
  cursor: pointer;
  width: 200px;
  padding: 0 2px;
  border-right: none;
  border-left: none;
  box-shadow: 0 1px 20px 0 rgba(0, 0, 0, 0.35);
  border-radius: 5px;
}

.hs-button {
  display: block;
  text-align: center;
  border-radius: 2px;
  border: solid 3px #795548;
}

.hs-text {
  display: table-cell;
  width: 100%;
  vertical-align: middle;
  padding: 0.6rem 1.5rem;
  text-transform: uppercase;
  font-weight: 700;
  text-shadow: 0 0 4px #000, 0 0 8px #000;
  font-size: 1.25rem;
  letter-spacing: 2px;
  font-family: "Fondamento", cursive;
}

.hs-border {
  display: table;
  padding: 3px;
  border-radius: 2px;
  height: 35px;
  min-height: 35px;
  width: calc(100% - 6px);
  text-transform: uppercase;
  color: #fff;
  text-decoration: none;
  text-shadow: 1px 1px #000;
  font-size: 17px;
  text-align: center;
}

.hs-wrapper.classic {
  background: linear-gradient(
    to bottom,
    #c1b3b0,
    #c1b3b0 9%,
    #4a3424 93%,
    #1c140d
  );
  border-top: 2px solid #ad9a90;
  border-bottom: 2px solid #1c140d;
}

.hs-button.classic {
  background: linear-gradient(to bottom, #6f5742, #81615d);
}

.hs-text.classic {
  background: radial-gradient(circle, #bc22c7 25%, #7c1693 75%, #5c1096);
}

.hs-border.classic {
  box-shadow: 0 2px 6px 0 #331e0b;
  background: linear-gradient(
    to bottom,
    #f756fe,
    #c84bd6 5%,
    #7305ae 59%,
    #661f91
  );
}

.hs-border:hover .hs-text.classic {
  background: radial-gradient(circle, #e235ee 22%, #981cb4);
}
</style>
