<script setup>
import { ref, onMounted, onBeforeUnmount } from "vue";

const aberto = ref(false);
const menuX = ref("50%");
const menuY = ref("50%");

const links = ["Início", "Sobre", "Projetos", "Time", "Contato"];

function toggle(e) {
  if (!aberto.value) {
    const rect = e.currentTarget.getBoundingClientRect();
    menuX.value = rect.left + rect.width / 2 + "px";
    menuY.value = rect.top + rect.height / 2 + "px";
  }
  aberto.value = !aberto.value;
  document.body.style.overflow = aberto.value ? "hidden" : "";
}

function close() {
  aberto.value = false;
  document.body.style.overflow = "";
}

function onKey(e) {
  if (e.key === "Escape" && aberto.value) close();
}

onMounted(() => window.addEventListener("keydown", onKey));
onBeforeUnmount(() => {
  window.removeEventListener("keydown", onKey);
  document.body.style.overflow = "";
});
</script>

<template>
  <main class="app">
    <header class="topbar">
      <span class="brand">MorphMenu</span>
      <button
        class="burger"
        :class="{ aberto }"
        :aria-expanded="aberto"
        aria-label="Menu"
        @click="toggle"
      >
        <svg viewBox="0 0 40 40" width="32" height="32">
          <path class="line line1" d="M8 13 L32 13 L32 13 L8 13" />
          <path class="line line2" d="M8 20 L32 20 L32 20 L8 20" />
          <path class="line line3" d="M8 27 L32 27 L32 27 L8 27" />
        </svg>
      </button>
    </header>

    <section class="hero">
      <h1>Menu de Navegação Morphing</h1>
      <p>Clique no hambúrguer para ver o morph de path e a máscara circular.</p>
    </section>

    <div
      class="overlay"
      :class="{ aberto }"
      :style="{ '--x': menuX, '--y': menuY }"
    >
      <nav class="menu">
        <a
          v-for="(link, i) in links"
          :key="link"
          href="#"
          class="menu-link"
          :style="{ '--i': i }"
          @click.prevent="close"
        >{{ link }}</a>
      </nav>
    </div>
  </main>
</template>
