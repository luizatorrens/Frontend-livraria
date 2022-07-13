<script>
import axios from "axios";
export default {
  data() {
    return {
      novo_autor: "",
      autores: [],
    };
  },
    async created() {
    const autores = await axios.get("http://localhost:4000/autores");
    this.autores = autores.data;
  },
  methods: {
    async salvar() {
      const autor = {
        nome: this.novo_autor,
      };
      const autor_criado = await axios.post("http://localhost:4000/autores", autor);
      this.autores.push(autor_criado.data);
      this.novo_autor = "";
    },
     async excluir(autor) {
      await axios.delete(`http://localhost:4000/autores/${autor.id}`);
      const indice = this.autores.indexOf(autor);
      this.autores.splice(indice, 1);
    },
    alerta() {
      alert("Ok!");
    },
  },
};
</script>

<template>
  <div class="position-absolute top-50 start-50 translate-middle">
    <div class="formulario">
      <div>
        <h2 class="title">Gerencimento de Autores</h2>
      </div>
      <div class="form-input container d-flex">
        <input
          class="col-10"
          type="text"
          v-model="novo_autor"
          @keyup.enter="salvar"
          placeholder="Autores"
        />
        <button class="btn btn_save" @click="salvar">Salvar</button>
      </div>
    </div>
    <div class="list-items">
      <table>
        <thead>
          <tr>
            <td>ID</td>
            <td>Nomes</td>
            <td>Ações</td>
          </tr>
        </thead>
        <tbody>
          <tr v-for="autor in autores" :key="autor.id">
            <td>{{ autor.id }}</td>
            <td>{{ autor.nome }}</td>

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
