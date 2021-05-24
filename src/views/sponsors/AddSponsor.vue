<template>
  <!-- Portfolio Section -->
  <section class="page-section">
    <b-container>
      <HeaderPage title="Adicionar SPONSOR" />

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
                placeholder="introduza o nome"
                required
              />
            </div>
            <!--opcão-box Type de SPONSOR-->
               <div class="form-group">
              <select
                id="sltGroup"
                class="form-control form-control-lg"
                v-model="type"
                required
              >
                <option value>-- SELECIONA Type--</option>
                <option value="1">1</option>
                <option value="2">2</option>
                <option value="h3">3</option>
              </select>
            </div>
            <!--text-box  atribuir Quota do EXPERT-->
               <div class="form-group">     
              <textarea
                id="txtDescription"
                class="form-control form-control-lg"
                placeholder="Atribua uma percentagem de 0 a 100 explique brevemente o motivo da atribuição"
                cols="30"
                rows="10"
                v-model="description"
                required
              ></textarea>
            </div>
 <button type="submit" class="btn btn-outline-success btn-lg mr-2">
              <i class="fas fa-plus-square"></i> ADICIONAR
            </button>

            <router-link
              :to="{ name: 'listSponsors' }"
              tag="button"
              class="btn btn-outline-danger btn-lg">
              <i class="fas fa-window-close"></i> CANCELAR</router-link>
          
          </form>

        </b-col>
        <b-col cols="2"></b-col>
      </b-row>
    </b-container>
  </section>
</template>

<script>
import { ADD_SPONSOR } from "@/store/sponsors/sponsor.constants";
import HeaderPage from "@/components/HeaderPage.vue";
import router from "@/router";
import { mapGetters } from "vuex";

export default {
  name: "AddSponsor",
  components: {
    HeaderPage,
  },
  data: () => {
    return {
      name: "",
      type: "",
      description: "",
      montante: "",

      evaluation: [],
      comments: [],
    };
  },
  computed: {
    ...mapGetters("sponsor", ["getMessage"]),
  },
  methods: {

    teste(){
      console.log(this.$data.name);
    },
    add() {
      this.$store.dispatch(`sponsor/${ADD_SPONSOR}`, this.$data).then(
        () => {
          this.$alert(this.getMessage, "patrocinador adicionado!", "success");
          router.push({ name: "listSponsors" });
        },
        (err) => {
          this.$alert(`${err.message}`, "Erro", "error");
        }
      );
    },
  },
};
</script>
