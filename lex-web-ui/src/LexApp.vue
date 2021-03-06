<template>
  <div id="lex-app">
    <page
      v-bind:favIcon="favIcon"
      v-bind:pageTitle="pageTitle"
      v-once
    ></page>
    <router-view></router-view>
  </div>
</template>

<script>
/*
Copyright 2017-2017 Amazon.com, Inc. or its affiliates. All Rights Reserved.

Licensed under the Amazon Software License (the "License"). You may not use this file
except in compliance with the License. A copy of the License is located at

http://aws.amazon.com/asl/

or in the "license" file accompanying this file. This file is distributed on an "AS IS"
BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, express or implied. See the
License for the specific language governing permissions and limitations under the License.
*/

/* eslint no-console: ["error", { allow: ["warn", "error", "info"] }] */
import Vue from 'vue';
import Vuex from 'vuex';
import Vuetify from 'vuetify';

import Page from '@/components/Page';
import { Loader as LexWebUi } from '@/lex-web-ui';

import flowerLogo from './assets/storage_pug_logo.png';

function getToolbarLogo() {
  // Search for logo image files in ../assets/
  // if not found, assigns the default flower logo.
  const toolbarLogoRequire =
    // Logo loading depends on the webpack require.context API:
    // https://webpack.github.io/docs/context.html
    require.context('@/assets', false, /^\.\/logo.(png|jpe?g|svg)$/);
  const toolbarLogoRequireKey = toolbarLogoRequire.keys().pop();

  return (toolbarLogoRequireKey) ?
    toolbarLogoRequire(toolbarLogoRequireKey) :
    flowerLogo;
}

function getFavIcon() {
  // search for favicon in assets directory - use toolbar logo if not found
  const favIconRequire =
    require.context('@/assets', false, /^\.\/favicon.(png|jpe?g|svg|ico)$/);
  const favIconRequireKey = favIconRequire.keys().pop();
  return (favIconRequireKey) ?
    favIconRequire(favIconRequireKey) :
    flowerLogo;
}

Vue.use(Vuex);
Vue.use(Vuetify);

const lexWebUi = new LexWebUi({
  ui: {
    toolbarLogo: getToolbarLogo(),
  },
});

export default {
  name: 'lex-app',
  store: lexWebUi.store,
  components: { Page },
  data() {
    return {
      favIcon: getFavIcon(),
      pageTitle: 'Order Flowers Bot',
    };
  },
};
</script>

<style>
@import '../node_modules/material-design-icons/iconfont/material-icons.css';
@import '../node_modules/vuetify/dist/vuetify.min.css';
@import 'https://stackpath.bootstrapcdn.com/bootstrap/4.1.0/css/bootstrap.min.css'
@import url('https://fonts.googleapis.com/css?family=Nunito+Sans');

.message-text, .toolbar__title, #text-input {
  font-family: 'Nunito Sans', sans-serif;
}
.application.theme--light {
  background: #fff !important;
}
.primary-bg {
  background: #31B896;
  color: #fff !important;
}
.blue-bg {
  background: #3D73B9;
  color: #fff !important;
}
.primary-c {
  color: #31B896;
}
.center {
  text-align: center;
      display: block;
}

</style>
