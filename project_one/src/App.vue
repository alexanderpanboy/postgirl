<template>
  <v-app>
    <v-app-bar
    app
    color="blue lighten-1"
    dark
    flat
    >
    <p v-text="barText" class="mt-4" justify-right style="font-size:2em"></p>

  </v-app-bar>

  <v-content>
    <MainPage/>
  </v-content>
</v-app>
</template>

<script>
import MainPage from './components/MainPage';
import GFaceManagerPage from './components/GFaceManagerPage';
import { mdiPlayCircleOutline } from '@mdi/js';
import { mdiFormatVerticalAlignBottom } from '@mdi/js';
import { mdiPlus } from '@mdi/js';
import { mdiChevronDown } from '@mdi/js';
import { mdiCloseCircleOutline } from '@mdi/js';
import { mdiPlusCircleOutline } from '@mdi/js';
import { mdiChevronDownCircleOutline } from '@mdi/js';
import { mdiCircleEditOutline } from '@mdi/js';

export default {
  name: 'App',

  components: {
    MainPage,
    GFaceManagerPage,
  },

  data() {
    return{
    barText: "Guide"
  }
},
};
</script>
