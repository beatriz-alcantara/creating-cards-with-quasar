<template>
  <div>
    <div class="q-pa-md row items-start q-gutter-md" v-if="mostrarCard">
      <q-card :key="obj.id" v-for="obj in cardsContent" class="my-card">
        <q-card-section>
          <q-img class="image" @click="showImage(obj.image)" style="height: 280px; width: 300px;" :src="obj.image">
            <div class="absolute-bottom text-subtitle2 text-center">
              {{ obj.title }}
            </div>
          </q-img>
        </q-card-section>
        <q-card-section>Description: {{ obj.description }}</q-card-section>
      </q-card>
    </div>
    <q-dialog v-model="visualizingImage">
      <img :src="selectedImage">
    </q-dialog>
    <div class="row flex flex-center">
      <div class="fixed-center" v-if="showEditor">
        <div class="col-3 col-sm-6 content-center self-center">
          <q-uploader ref="upload" @added="savingImage"/>
        </div>
        <div class="col-3 col-sm-6 content-center self-center">
          <q-input type="text" v-model="content.description" label="Description" />
          <q-input type="text" v-model="content.title" label="Title" @keyup.enter="addingContent()" />
          <q-btn @click="addingContent()" label="Done" />
        </div>
      </div>
    </div>
      <div v-if="mostrarCard">
        <q-btn @click="edit()" label="Add Card"/>
      </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      cardsContent: [],
      visualizingImage: false,
      selectedImage: '',
      content: {
        description: '',
        title: ''
      },
      mostrarCard: false,
      showEditor: true
    }
  },
  methods: {
    savingImage (file) {
      this.content.image = file[0].__img.src
      this.content.id = this.cardsContent.length
    },
    addingContent () {
      this.mostrarCard = true
      this.showEditor = false
      this.cardsContent.push(this.content)
      this.content = {}
    },
    edit () {
      this.showEditor = true
      this.mostrarCard = false
    },
    showImage (img) {
      this.selectedImage = img
      this.visualizingImage = true
    }
  }
}
</script>

<style scoped>
.my-card {
  width: 100%;
  height: 100%;
  max-width: 350px;
  max-height: 360px;
  }

  .image {
    cursor: pointer;
  }
</style>
