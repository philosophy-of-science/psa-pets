<template>
  <v-row justify="end">
    <v-dialog v-model="dialog" max-width="600px">
      <template v-slot:activator="{ on, attrs }">
        <v-btn color="blue" dark v-bind="attrs" v-on="on" class="mr-2">
          Share Your Pet
        </v-btn>
      </template>
      <v-card>
        <v-card-title>
          <p class="text-h5 mb-0">Share Your Pet with the PSA</p>
        </v-card-title>

        <v-container>
          <pet-share-form @close="dialog = false" />
        </v-container>
      </v-card>
    </v-dialog>
  </v-row>
</template>

<script>
import PetShareForm from './PetShareForm.vue';

export default {
  components: { PetShareForm },

  data() {
    return {
      dialog: false,
    };
  },
};
</script>

<style></style>
