<template>
  <section class="page-section">
    <b-container>
     <HeaderPage title="Gestão de Experts"/>
      
      <!--MENU TOPO-->
      <b-row class="mb-4">
        <b-col cols="1"></b-col>
        <b-col>
          <router-link
            :to="{name:'addExpert'}"
            tag="button"
            class="btn btn-outline-success mr-2 mt-2"
          ><i class="fas fa-plus-square"></i> ADICIONAR EXPERT</router-link>
          <router-link
            :to="{name:'admin'}"
            tag="button"
            class="btn btn-outline-info mr-2 mt-2"
          ><i class="fas fa-bars"></i> MENU PRINCIPAL</router-link>
        </b-col>
        <b-col cols="1"></b-col>
      </b-row>

      <!-- TABELA -->
      <b-row>
        <b-col cols="1"></b-col>
        <b-col>
          <table class="table table-striped">
            <thead class="thead-dark">
              <tr>
                <th scope="col">
                  NOME
                  <i class="fas fa-arrow-up" v-if="sortType===1" @click="sort()"></i>
                  <i class="fas fa-arrow-down" v-else  @click="sort()"></i>
                </th>
                <th scope="col">ESPÈCIE</th>
                <th scope="col">DATA DE CRIAÇÃO</th>
                <th scope="col">AÇÕES</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="user of users" :key="user._id">                
                <td class="pt-4">{{user.name}}</td>
                <td class="pt-4">{{user.type==="admin"?"Administrador":"Utilizador normal"}}</td>
                <td class="pt-4">{{formatDate(user.registration_date)}}</td>
                <td>
                  <router-link
                    :to="{name:'editUser', params:{userId: user._id}}"
                    tag="button"
                    class="btn btn-outline-success mr-2"
                  ><i class="fas fa-edit"></i> EDITAR</router-link>
                  <button
                    @click="viewUser(user._id)"
                    type="button"
                    class="btn btn-outline-success mr-2"
                  ><i class="fas fa-search"></i> VER</button>
                  <button
                    @click="removeUser(user._id)"
                    type="button"
                    class="btn btn-outline-danger mr-2 "
                  ><i class="fas fa-trash-alt"></i> REMOVER</button>
                </td>
              </tr>
            </tbody>
          </table>
        </b-col>
        <b-col cols="1"></b-col>
      </b-row>
    </b-container>
  </section>
</template>

<script>
import HeaderPage from "@/components/HeaderPage.vue";
export default {
  components: {
    HeaderPage
  }
};
</script>
