<script>
import axios from "axios";
export default {
  data() {
    return {
      nova_categoria: "",
      categorias: [],
    };
  },
  async created() {
    const categorias = await axios.get("http://localhost:4000/categorias");
    this.categorias = categorias.data;
  },
  methods: {
    async salvar() {
      const categoria = {
        nome: this.nova_categoria,
      };
      const categoria_criada = await axios.post(
        "http://localhost:4000/categorias",
        categoria
      );
      this.categorias.push(categoria_criada.data);
      this.nova_categoria = "";
    },
    async excluir(categoria) {
      await axios.delete(`http://localhost:4000/categorias/${categoria.id}`);
      const indice = this.categorias.indexOf(categoria);
      this.categorias.splice(indice, 1);
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
          v-model="nova_categoria"
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
          <tr v-for="categoria in categorias" :key="categoria.id">
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
