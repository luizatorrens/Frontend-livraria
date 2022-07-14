<script>
import axios from "axios";
export default {
  data() {
    return {
      nova_editora: "",
      editoras: [],
    };
  },
  async created() {
    const editoras = await axios.get("http://localhost:4000/editoras");
    this.editoras = editoras.data;
  },
  methods: {
    async salvar() {
      const categoria = {
        nome: this.nova_editora,
      };
      const categoria_criada = await axios.post(
        "http://localhost:4000/editoras",
        categoria
      );
      this.editoras.push(categoria_criada.data);
      this.nova_editora = "";
    },
    async excluir(categoria) {
      await axios.delete(`http://localhost:4000/editoras/${categoria.id}`);
      const indice = this.editoras.indexOf(categoria);
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
        <h2 class="title">Gerencimento de Categorias</h2>
      </div>
      <div class="form-input container d-flex">
        <input
          class="col-10"
          type="text"
          v-model="nova_editora"
          @keyup.enter="salvar"
          placeholder="Categorias"
        />
        <button class="btn btn_save" @click="salvar">Salvar</button>
      </div>
    </div>

    <div class="list-items">
      <table>
        <thead>
          <tr>
            <td>ID</td>
            <td>Categorias</td>
            <td>Ações</td>
          </tr>
        </thead>
        <tbody>
          <tr v-for="categoria in editoras" :key="categoria.id">
            <td>{{ categoria.id }}</td>
            <td>{{ categoria.nome }}</td>

            <td class="button-group d-flex salvar_editar">
              <button class="btn btn-primary" @click="alerta(categoria)">
                Editar
              </button>
              <button class="btn btn-danger" @click="excluir(categoria)">
                Excluir
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>