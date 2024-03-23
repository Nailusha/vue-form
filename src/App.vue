<template>
  <div id="app">
    <header>
      <h1>Мое приложение</h1>
    </header>
    <main>
      <ClientForm />
    </main>
    <footer>
      <p>&copy; 2024 Мое приложение</p>
    </footer>
  </div>
</template>

<script>
import ClientForm from './components/ClientForm.vue';

export default {
  components: {
    ClientForm
  }
};
</script>

<style>
#app {
  font-family: Arial, sans-serif;
  text-align: center;
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

header {
  background-color: #007bff;
  color: white;
  padding: 20px 0;
}

main {
  flex-grow: 1;
}

footer {
  background-color: #f8f9fa;
  padding: 10px 0;
}
</style>

