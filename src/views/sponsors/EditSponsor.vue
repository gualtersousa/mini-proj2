<template>
  <section class="page-section">
    <b-container>
      <HeaderPage title="Editar Patrocinadores" />

      <!--FORM-->
      <b-row>
        <b-col cols="2"></b-col>
        <b-col cols="8">
          <form @submit.prevent="update">
            <div class="form-group">
              <input
                v-model="sponsor.name"
                type="text"
                class="form-control form-control-lg"
                id="txtName"
                placeholder="escreve nome"
                required
              />
            </div>
            <div class="form-group">
              <select id="sltGroup" class="form-control form-control-lg" v-model="sponsor.group">
                <option value>-- SELECIONA TIPO --</option>
                <option value="economico">ECONÓMICO</option>
                <option value="material">MATERIAL</option>
                <option value="humano">HUMANO</option>
              </select>
            </div>
            <div class="form-group">
              <textarea
                id="txtDescription"
                class="form-control form-control-lg"
                placeholder="escreve descrição"
                cols="30"
                rows="10"
                v-model="sponsor.description"
                required
              ></textarea>
            </div>
            <div class="form-group">
              <div class="form-group">
                <input
                  v-model="sponsor.type"
                  type="number"
                  min="1"
                  max="5"
                  class="form-control form-control-lg"
                  id="txtLevel"
                  placeholder="escreve o nível"
                  required
                />
              </div>
            </div>
            
           
            
            
            <button type="button" class="btn btn-outline-success btn-lg mr-2" @click="removeComments()">
              <i class="fas fa-edit"></i> REMOVER COMENTÁRIOS
            </button>
            <button type="submit" class="btn btn-outline-success btn-lg mr-2">
              <i class="fas fa-edit"></i> ATUALIZAR
            </button>
            <router-link
              :to="{name: 'listAnimals'}"
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

