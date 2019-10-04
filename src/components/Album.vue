<template>
  <div>
    <div class="row justify-center">
      <div class="col-6 items-center q-pb-xl">
        <q-card v-if="mostrarCard">
          <div class="relative-top text-subtitle2 text-center">
            {{ title }}
          </div>
          <q-card-section class="bg-blue-grey-10">
            <img :src="image" />
          </q-card-section>
          <q-card-section>Description: {{ description }}</q-card-section>
        </q-card>
      </div>
    </div>
    <div class="column">
      <div class="col-3 col-sm-6">
        <q-uploader ref="upload" @added="savingImage" @removed="removingImage" />
      </div>
      <div class="col-3 col-sm-6">
        <q-input type="text" v-model="description" label="Description" />
        <q-input type="text" v-model="title" label="Title" />
        <q-btn @click="showButton" label="Done" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      description: '',
      title: '',
      image: '',
      mostrarCard: false
    }
  },
  methods: {
    teste (file) {
      alert('oi')
      console.log(file)
    },
    savingImage (file) {
      this.image = file[0].__img.src
      console.log(file[0])
    },
    removingImage (file) {
      this.mostrarCard = true
      this.image = ''
    },
    showButton () {
      this.mostrarCard = true
    }
  }
}
</script>
