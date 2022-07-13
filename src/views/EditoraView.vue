<script>
import { v4 as uuid } from "uuid";
export default {
  data() {
    return {
      nova_editora: "",
      editoras: [
        {
          id: "f12bc7ce-5ca7-4cbf-ac6e-be3e59cb2862",
          name: "Seguinte",
        },
        {
          id: "b880659d-5d33-4607-ae19-8a22a738b509",
          name: "Intríseca",
        },
        {
          id: "0f97fea6-72ac-4ee0-bf1b-92516d3417e1",
          name: "Aleph",
        },
        {
          id: "25c441be-e90a-4847-98a7-0d888e4c981f",
          name: "Suma",
        },
      ],
    };
  },
  methods: {
    salvar() {
      if (this.nova_editora !== "") {
        const novo_id = uuid();
        this.editoras.push({
          id: novo_id,
          name: this.nova_editora,
        });
        this.nova_editora = "";
      }
    },
    excluir(editora) {
      const indice = this.editoras.indexOf(editora);
      this.editoras.splice(indice, 1);
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
        <h2 class="title">Gerencimento de Editoras</h2>
      </div>
      <div class="form-input container d-flex">
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
            <td>Editoras</td>
            <td>Ações</td>
          </tr>
        </thead>
        <tbody>
          <tr v-for="editora in editoras" :key="editora.id">
            <td>{{ editora.id }}</td>
            <td>{{ editora.name }}</td>
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