<script>
import axios from "axios";
export default {
  data() {
    return {
      livro: {},
      livros: [],
      autores: [],
      categorias: [],
      editoras: [],
    };
  },
  async created() {
    await this.buscarTodosOsAutores();
    await this.buscarTodasAsCategorias();
    await this.buscarTodosAsEditoras();
  },

  methods: {
    async buscarTodosOsAutores() {
      const autores = await axios.get("http://localhost:4000/autores");
      this.autores = autores.data;
    },
    async buscarTodosAsCategorias() {
      const categorias = await axios.get("http://localhost:4000/categorias");
      this.categorias = categorias.data;
    },
    async buscarTodosAsEditoras() {
      const editoras = await axios.get("http://localhost:4000/editoras");
      this.editoras = editoras.data;
    },
  },
};
</script>

<template>
  <div class="position-absolute top-50 start-50 translate-middle">
    <div class="formulario">
      <div>
        <h2 class="title" >Gerencimento de Livros</h2>
      </div>
      <div class="input-group container">
        <input
          class="col form-control d-flex"
          type="text"
          v-model="novo_livro"
          @keyup.enter="salvar"
          placeholder="Livros"
        />
        <input
          class="col form-control d-flex"
          type="text"
          v-model="novo_autor"
          @keyup.enter="salvar"
          placeholder="Autores"
        />
        <select v-model="livro.categoriaId" @keyup.enter="salvar">
        <option v-for="categoria in categorias" :key="categoria.id" :value="categoria.id">
        {{ categoria.nome }}
        </option>
        </select>

        <select class="form-select" v-model="nova_editora">
          <option value="" class="col form-control d-flex" disabled>Editora</option>
          <option value="Editora 1">Editora 1</option>
          <option value="Editora 2">Editora 2</option>
          <option value="Editora 3">Editora 3</option>
          <option value="Editora 4">Editora 4</option>
          <option value="Editora 5">Editora 5</option>
        </select>

        <button class="btn btn_save" @click="salvar">Salvar</button>
      </div>
    </div>
    <div class="list-items">
      <table>
        <thead>
          <tr>
            <td>ID</td>
            <td>Livros</td>
            <td>Autores</td>
            <td>Categorias</td>
            <td>Editoras</td>
            <td>Ações</td>
          </tr>
        </thead>
        <tbody>
          <tr v-for="livro in livros" :key="livro.id">
            <td>{{ livro.id }}</td>
            <td>{{ livro.nome }}</td>
            <td>{{ livro.autorId }}</td>
            <td>{{ livro.categoriaId }}</td>
            <td>{{ livro.editoraId }}</td>

            <td class="button-group d-flex salvar_editar">
              <button class="btn btn-primary" @click="alerta(livro)">Editar</button>
              <button class="btn btn-danger" @click="excluir(livro)">Excluir</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<style></style>
