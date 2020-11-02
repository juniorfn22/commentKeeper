<template>
  <div class="form-group">
    <label for="" class="">Nome:</label>
    <input type="text" v-model="nome" class="form-control" required />
  </div>
  <div class="form-group">
    <label for="">Mensagem</label>
    <textarea class="form-control" v-model="mensagem" rows="3"></textarea>
  </div>
  <button
    type="button"
    v-on:click="adicionarComentario"
    class="btn btn-primary"
  >
    Comentar
  </button>
</template>

<script>
export default {
  data() {
    return {
      nome: "",
      mensagem: "",
    };
  },
  methods: {
    adicionarComentario() {
      if (this.mensagem.trim() === "") {
        alert("O campo mensagem não pode estar em branco!");
        return;
      }
      this.comentarios.push({
        nome: this.nome,
        mensagem: this.mensagem,
      });

      this.nome = "";
      this.mensagem = "";
    },
  },
};
</script>

<style>
</style>