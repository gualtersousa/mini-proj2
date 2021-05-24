<template>
  <section class="page-section">
    <b-container>
      <HeaderPage title="Gestão de EXPERTS"/>
      <!--MENU DE TOPO-->
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
      
      <!--TABLE-->
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
                <th scope="col">CLASS</th>
                <th scope="col">QUOTA</th>
                <th scope="col"></th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="question of questions" :key="question._id">
                <td  class="pt-4">{{question.question}}</td>
                <td class="pt-4">{{question.level}}</td>
                <td>
                  <router-link
                    :to="{name:'editExpert', params:{questionId: question._id}}"
                    tag="button"
                    class="btn btn-outline-success mr-2"
                  ><i class="fas fa-edit"></i> EDITAR</router-link>
                  <button
                    @click="viewExpert(question._id)"
                    type="button"
                    class="btn btn-outline-warning mr-2"
                  ><i class="fas fa-search"></i> VER</button>
                  <button
                    @click="removeExpert(question._id)"
                    type="button"
                    class="btn btn-outline-danger mr-2"
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
import {
  FETCH_QUESTIONS,
  REMOVE_QUESTION
} from "@/store/questions/question.constants";
import HeaderPage from "@/components/HeaderPage.vue"
import { mapGetters } from "vuex";


export default {
  name: "ListExperts",
   components: {
    HeaderPage
  },
  data: function() {
    return {
      questions: [],
      sortType: 1
    };
  },
  computed: {
    ...mapGetters("question", ["getExperts","getMessage"])
  },
  methods: {
    fetchExperts() {
      this.$store.dispatch(`question/${FETCH_QUESTIONS}`).then(
        () => {
          this.questions = this.getExperts;
        },
        err => {
          this.$alert(`${err.message}`, "Erro", "error");
        });
    },
    sort() {
      this.questions.sort(this.compareNames)
      this.sortType *= -1      
    },
    compareNames(u1,u2) {
      if(u1.question > u2.question) return 1 * this.sortType
      else if(u1.question < u2.question) return -1 * this.sortType
      else return 0
    },
    viewExpert(id) {
      const question = this.questions.find(question => question._id === id);
      this.$fire({
        title: question.question,
        html: this.generateTemplate(question)
        /* imageUrl: user.name,
        imageWidth: 400,
        imageHeight: 200,
        imageAlt: "Imagem desconhecida" */
      });
    },
    generateTemplate(question) {
      let response = `
          <p><b>Descrição:</b> ${question.description}</p>
          <p><b>Tipo:</b> ${question.type}</p>
          <p><b>Lista de respostas possíveis (correta a verde):</b></p>`          
          for ( let i=0; i<question.answers.length;i++) {
            if(question.answers[i].correct)
            response += `<p class="green"}>${i+1}. ${question.answers[i].title}</p>`
            else
            response += `<p class="red"}>${i+1}. ${question.answers[i].title}</p>`
              
          }
      return response;
    },
    removeExpert(id) {
      this.$confirm(
        "Se sim, clique em OK",
        "Deseja mesmo remover a questão?",
        "warning",
        { confirmButtonText: "OK", cancelButtonText: "Cancelar" }
      ).then(
        () => {
          this.$store.dispatch(`question/${REMOVE_QUESTION}`, id).then(() => {
            this.$alert(
              this.getMessage,
              "Questão removida!",
              "success"
            );
            this.fetchExperts();
          });
        },
        () => {
          this.$alert("Remoção cancelada!", "Informação", "info");
        }
      );
    }
  },
  created() {
    this.fetchExperts();
  }
};
</script>
<style>
.green {
  color: green
}

.red {
  color: red
}
</style>