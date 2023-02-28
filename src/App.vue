<template>
  <div v-move class="box">
    <div class="header"></div>
    <div class="head"></div>
    <div>内容</div>
  </div>
</template>

<script setup lang="ts">
import { ref, reactive, watch, Directive, DirectiveBinding } from "vue";
const vMove: Directive<any, void> = (
  el: HTMLElement,
  binding: DirectiveBinding
) => {
  console.log(el, binding);
  let moveElement: HTMLElement = el.firstElementChild as HTMLElement;
  console.log(moveElement);

  const mouseDown = (e: MouseEvent) => {
    let X = e.clientX - el.offsetLeft;
    let Y = e.clientY - el.offsetTop;
    const move = (e: MouseEvent) => {
      el.style.left = e.clientX - X + "px";
      el.style.top = e.clientY - Y + "px";
      console.log(el.style.left, el.style.top);
    };
    document.addEventListener("mousemove", move);
    document.addEventListener("mouseup", () => {
      document.removeEventListener("mousemove", move);
    });
  };
  moveElement.addEventListener("mousedown", mouseDown);
};
</script>

<style scoped>
.box {
  position: fixed;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  height: 200px;
  width: 200px;
  border: 3px solid black;
}
.header {
  height: 20px;
  width: 100%;
  background: black;
}
.head {
  height: 20px;
  width: 100%;
  background: pink;
}
</style>
