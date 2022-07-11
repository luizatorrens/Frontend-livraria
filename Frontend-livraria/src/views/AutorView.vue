<script>
import { v4 as uuid } from "uuid";
export default {
  data() {
    return {
      novo_autor: "",
      autores: [
        { id: "f12bc7ce-5ca7-4cbf-ac6e-be3e59cb2862", name: "Autor 1" },
        { id: "b880659d-5d33-4607-ae19-8a22a738b509", name: "Autor 2" },
        { id: "0f97fea6-72ac-4ee0-bf1b-92516d3417e1", name: "Autor 3" },
        { id: "25c441be-e90a-4847-98a7-0d888e4c981f", name: "Autor 4" },
      ],
    };
  },
  methods: {
    salvar() {
      if (this.novo_autor !== "") {
        const novo_id = uuid();
        this.autores.push({
          id: novo_id,
          name: this.novo_autor,
        });
        this.novo_autor = "";
      }
    },
    excluir(autor) {
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
            <td>{{ autor.name }}</td>

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
