<template>
  <header class="banner">
    <div class="banner-content">
      <img src="../../public/icone-vue.png" alt="Ícone do Vue.js" class="icone-vue"> <!--BAIXAR A IMAGEM DO DRIVE COM O LINK DO SLIDE-->
      <h1>Lista de Tarefas 📅</h1> <!--PESQUISAR "EMOJI CALENDÁRIO" NO GOOGLE-->
    </div>
  </header>
</template>


<style scoped>
.banner {
  background: linear-gradient(135deg, #2a9d8f, #264653);
  color: #fff;
  text-align: center;
  padding: 1.5rem 1rem;
  border-radius: 0 0 16px 16px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.15);
  font-family: sans-serif;
}

.banner-content {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;
}

.banner h1 {
  font-size: 1.8rem;
  font-weight: 600;
  letter-spacing: 1px;
}

.icone-vue {
  width: 60px;
  height: 60px;
}

@media (max-width: 600px) {
  .banner h1 {
    font-size: 0.9rem;
  }
}
</style>
