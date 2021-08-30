<template>
  <v-form
    v-model="valid"
    class="pa-2"
    data-netlify="true"
    data-netlify-honeypot="bot-field"
    name="psa-pets"
  >
    <v-container>
      <v-row>
        <input type="hidden" name="form-name" value="psaPets" />
        <v-col cols="12" md="6">
          <v-text-field
            v-model="firstname"
            :rules="nameRules"
            label="First name"
            required
            prepend-icon="mdi-account"
          ></v-text-field>
        </v-col>

        <v-col cols="12" md="6">
          <v-text-field
            v-model="lastname"
            :rules="nameRules"
            label="Last name"
            required
          ></v-text-field>
        </v-col>

        <v-col cols="12" md="12">
          <v-text-field
            v-model="email"
            :rules="emailRules"
            label="Email"
            prepend-icon="mdi-email"
            required
          ></v-text-field>
        </v-col>

        <v-col cols="12" md="12">
          <v-text-field
            v-model="socialMedia"
            label="Social media or website"
            required
            prepend-icon="mdi-share"
          ></v-text-field>
        </v-col>

        <v-col cols="12" md="12">
          <v-text-field
            v-model="petsName"
            label="Pet's Name"
            required
            prepend-icon="mdi-dog"
          ></v-text-field>
        </v-col>

        <v-col cols="12" md="12">
          <v-file-input
            v-model="petsImage"
            label="Picture of Pet"
            prepend-icon="mdi-image"
            accept="image/png, image/jpeg, image/jpg"
            :rules="imageSize"
          ></v-file-input>
        </v-col>
      </v-row>
    </v-container>
    <v-card-actions>
      <v-spacer></v-spacer>
      <v-btn color="blue darken-1" text @click="$emit('close')">
        Close
      </v-btn>
      <v-btn color="blue darken-1" text @click="submitForm">
        Submit
      </v-btn>
    </v-card-actions>
  </v-form>
</template>

<script>
import axios from 'axios';

export default {
  data: () => ({
    valid: false,
    firstname: '',
    lastname: '',
    nameRules: [(v) => !!v || 'Name is required'],
    email: '',
    emailRules: [
      (v) => !!v || 'E-mail is required',
      (v) => /.+@.+/.test(v) || 'E-mail must be valid',
    ],
    socialMedia: '',
    imageSize: [
      (value) => !value || value.size < 2000000 || 'Avatar size should be less than 2 MB!',
    ],
    petsImage: null,
    petsName: '',
  }),

  methods: {
    submitForm() {
      function encode(name, value) {
        return `${encodeURIComponent(name)}=${encodeURIComponent(value)}`;
      }

      const formData = [
        encode('form-name', 'psa-pets'),
        encode('first', this.firstname),
        encode('last', this.lastname),
        encode('email', this.email),
        encode('social', this.socialMedia),
        encode('petsName', this.petsName),
      ].join('&');

      const axiosConfig = {
        header: { 'Content-Type': 'application/x-www-form-urlencoded' },
      };

      axios.post('/', formData, axiosConfig);
    },
  },
};
</script>

<style></style>
