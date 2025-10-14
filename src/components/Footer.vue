<template>
  <footer class="rodape">
    <h1>Mini-curso de Vue.Js IFSP - 2025</h1>
  </footer>
</template>

<style scoped>
.rodape {
  background: linear-gradient(135deg, #264653, #2a9d8f);
  color: #fff;
  text-align: center;
  padding: 15px;
  margin-top: 50px;
  border-radius: 16px 16px 0 0;
  font-family: sans-serif;
  margin-top: 2rem;
  position: fixed;
  bottom: 0;
  width: 100%;
}

.rodape h1 {
  font-size: 1rem;
  font-weight: normal;
  letter-spacing: 0.5px;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.3);
  margin: 0;
}

@media (max-width: 600px) {
  .rodape h1 {
    font-size: 0.9rem;
  }
}
</style>
