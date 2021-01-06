<template>
  <div class="container">
    <h1>Comentários</h1>
    <hr />
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
    <hr />
    <!-- {{comentarios}} -->
    <ul class="list-group">
      <div
        class="list-group-item"
        v-bind:key="index"
        v-for="(comentario, index) in comentarios">
        <span class="coment__autor">Autor: {{ comentario.nome}}</span>
        <p>Mensagem: {{ comentario.mensagem}}</p>
        <a href="#" v-on:click.prevent="removerComentario(comentario.id)">Excluir</a>
      </div>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  data() {
    return {
      /*
      * Array de comentários
      * Autor: José Carlos Júnior
      */
      // comentarios: [],
      nome: "",
      mensagem: "",
      comentarios: '',
    };
  },
  methods: {
    /**
     * Função para adição de comentário
     * Autor: José Carlos Júnior
     */
    adicionarComentario() {
      // if (this.mensagem.trim() === "") {
      //   alert("O campo mensagem não pode estar em branco!");
      //   return;
      // }
      axios
        .post('http://127.0.0.1:8000/api/comentarios/',{'nome':this.nome,'mensagem':this.mensagem})
        .then(response => console.log(response))
        location.reload();
        
      
      // this.comentarios.push({
      //   nome: this.nome,
      //   mensagem: this.mensagem,
      // });

      this.nome = "";
      this.mensagem = "";
    },
    /**
     * Função para remover comentários
     * Autor: José Carlos Júnior
     */
    removerComentario(id) {
      console.log(id);
      axios 
        .delete('http://127.0.0.1:8000/api/comentarios/'+id)
        .then(response => (console.log(response.data),location.reload()))
      // this.comentarios.splice(index, 1);
    },
  },
  mounted (){
    axios
      .get('http://127.0.0.1:8000/api/')
      .then(response => (this.comentarios = response.data))
      
  },
  computed: {
    /**
     * Função para classificar como anônimo os usuários que não informam o nome no momento do comentário
     * Autor: José Carlos Júnior
     */
    todosComentarios() {
      return this.comentarios.map((comentario) => ({
        ...comentario,
        nome: comentario.nome.trim() === "" ? "Anonimo" : comentario.nome,
      }));
    },
  },
  watch: {
    /**
     * Função para monitor os comentários
     * Autor: José Carlos Júnior
     */
    comentarios() {
      // console.log("Valores: ", val);
    },
  },
};
</script>