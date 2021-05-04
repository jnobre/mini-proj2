<template>
  <section class="page-section">
    <b-container>
      <HeaderPage title="Adicionar Expert" />
      <b-row>
        <b-col cols="2"></b-col>
        <b-col cols="8">
          <form @submit.prevent="add">
            <div class="form-group">
              <input
                v-model="name"
                type="text"
                class="form-control form-control-lg"
                id="txtName"
                placeholder="escreve nome"
                required
              />
            </div>
            <div class="form-group">
              <select
                id="sltType"
                class="form-control form-control-lg"
                v-model="type"
                required
              >
                <option value="">-- ESPÉCIE --</option>
                <option value="peixe">PEIXES</option>
                <option value="ave">AVES</option>
                <option value="mamífero">MAMÍFEROS</option>
                <option value="reptil">RÉPTIES</option>
              </select>
            </div>
            <div class="form-group">
              <input
                v-model="birth_date"
                type="text"
                onmouseenter="(this.type='date')"
                onmouseleave="(this.type='text')"
                class="form-control form-control-lg"
                id="txtBirthDate"
                placeholder="escreve data de nascimento"
                required
              />
            </div>
            <div class="form-group">
              <textarea
                v-model="location.descricao"
                type="text"
                class="form-control form-control-lg"
                id="txtCity"
                placeholder="Escreva uma descrição"
              ></textarea>
            </div>
            <div class="form-group">
              <input
                v-model="location.city"
                type="text"
                class="form-control form-control-lg"
                id="txtCity"
                placeholder="Cidade"
              />
            </div>
            <div class="form-group">
              <input
                v-model="location.country"
                type="text"
                class="form-control form-control-lg"
                id="txtCountry"
                placeholder="País"
              />
            </div>
            <div class="form-group">
              <input
                v-model="location.username"
                type="text"
                class="form-control form-control-lg"
                id="txtCountry"
                placeholder="Username"
              />
            </div>
            <div class="form-group">
              <input
                v-model="location.password"
                type="password"
                class="form-control form-control-lg"
                id="txtCountry"
                placeholder="Password"
              />
            </div>
            <div class="form-group">
              <input
                type="password"
                class="form-control form-control-lg"
                id="txtCountry"
                placeholder="Confirme a Password"
              />
            </div>

            <button type="submit" class="btn btn-outline-success btn-lg mr-2">
              <i class="fas fa-plus-square"></i> ADICIONAR
            </button>
            <router-link
              :to="{ name: 'listExperts' }"
              tag="button"
              class="btn btn-outline-danger btn-lg"
            >
              <i class="fas fa-window-close"></i> CANCELAR
            </router-link>
          </form>
        </b-col>
        <b-col cols="2"></b-col>
      </b-row>
    </b-container>
  </section>
</template>

<script>
import { ADD_USER } from "@/store/users/user.constants";
import HeaderPage from "@/components/HeaderPage.vue";
import router from "@/router";
import { mapGetters } from "vuex";
export default {
  name: "AddUser",
  components: {
    HeaderPage,
  },
  data: () => {
    return {
      location: { city: "", district: "", country: "" },
      auth: { username: "", password: "" },
      gamification: { points: "", quiz: "" },
      active: true,
      name: "",
      type: "",
      birth_date: "",
      description: "",
    };
  },
  computed: {
    ...mapGetters("user", ["getMessage"]),
  },
  methods: {
    add() {
      if (
        document.querySelector("#txtPassword").value !==
        document.querySelector("#txtConfirmPassword").value
      ) {
        this.$alert(
          "Campos password não coincidem",
          "Erro de validação do formulário",
          "error"
        );
      } else {
        this.$store.dispatch(`user/${ADD_USER}`, this.$data).then(
          () => {
            this.$alert(this.getMessage, "Utilizador adicionado!", "success");
            router.push({ name: "listUsers" });
          },
          (err) => {
            this.$alert(`${err.message}`, "Erro", "error");
          }
        );
      }
    },
  },
};
</script>
