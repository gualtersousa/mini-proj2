<template>
  <!-- Portfolio Section -->
  <section class="page-section">
    <b-container>
      <HeaderPage title="Adicionar EXPERT" />

      <!--FORM-->

      <b-row>
        <b-col cols="2"></b-col>
        
          <b-col>
     
    
      <!--MENU DE TOPO-->
      <b-row class="mb-4">
        <b-col cols="0"></b-col>
        <b-col>
             <router-link
            :to="{name:'admin'}"
            tag="button"
            class="btn btn-outline-info mr-2 mt-2"
          ><i class="fas fa-bars"></i> MENU PRINCIPAL</router-link>
        </b-col>
        <b-col cols="1"></b-col>
         
      </b-row>
                  
          <form @submit.prevent="add">
            <!--input-box nome-->
            <div class="form-group">
              <input
                v-model="name"
                type="text"
                class="form-control form-control-lg"
                id="txtName"
                placeholder="Introduza o nome"
                required
              />
              
            </div>
          <!--input-box classe do expert-->
            <div class="form-group">
              <input
                v-model="name"
                type="text"
                class="form-control form-control-lg"
                id="txtName"
                placeholder="Classe"
                required
              />
              
            </div>
          <!--input-box tipo de exoert-->
            <div class="form-group">
              <input
                v-model="name"
                type="text"
                class="form-control form-control-lg"
                id="txtName"
                placeholder="Tipo de Expert (Quota)"
                required
              />
              
            </div>

            

            <button type="submit" class="btn btn-outline-success btn-lg mr-2">
              <i class="fas fa-plus-square"></i> ADICIONAR
            </button>
            <router-link
              :to="{ name: 'listExperts' }"
              tag="button"
              class="btn btn-outline-danger btn-lg"
              ><i class="fas fa-window-close"></i> CANCELAR</router-link
            >
          </form>
        </b-col>
        <b-col cols="2"></b-col>
      </b-row>
    </b-container>
  </section>
</template>

<script>
import { ADD_ANIMAL } from "@/store/experts/expert.constants";
import HeaderPage from "@/components/HeaderPage.vue";
import router from "@/router";
import { mapGetters } from "vuex";

export default {
  name: "AddExpert",
  components: {
    HeaderPage,
  },
  data: () => {
    return {
      name: "",
      group: "",
      description: "",
      level: "",

      evaluation: [],
      comments: [],
    };
  },
  computed: {
    ...mapGetters("expert", ["getMessage"]),
  },
  methods: {
    add() {
      this.$store.dispatch(`animal/${ADD_ANIMAL}`, this.$data).then(
        () => {
          this.$alert(this.getMessage, "Animal adicionado!", "success");
          router.push({ name: "listAnimals" });
        },
        (err) => {
          this.$alert(`${err.message}`, "Erro", "error");
        }
      );
    },
  },
};
</script>
