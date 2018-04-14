<template>
  <v-card>
    <v-card-title v-if="responseCard.title.trim()" primary-title class="blue-bg lighten-5 center">
      <span class="headline">{{responseCard.title}}</span>
    </v-card-title>
    <v-card-text v-if="responseCard.subTitle">
      <span>{{responseCard.subTitle}}</span>
    </v-card-text>
    <v-card-media
      v-if="responseCard.imageUrl"
      v-bind:src="responseCard.imageUrl"
      contain
      height="33vh"
    ></v-card-media>
    <v-card-actions
      v-for="(button, index) in responseCard.buttons"
      v-bind:key="index"
      actions
      class="button-row"
    >
      <v-btn
        v-if="button.text && button.value"
        v-on:click.once.native="onButtonClick(button.value)"
        v-bind:disabled="hasButtonBeenClicked"
        default
      >
        {{button.text}}
      </v-btn>
    </v-card-actions>
    <v-card-actions v-if="responseCard.attachmentLinkUrl">
      <v-btn
        flat
        class="red lighten-5"
        tag="a"
        v-bind:href="responseCard.attachmentLinkUrl"
        target="_blank"
      >
        Open Link
      </v-btn>
    </v-card-actions>
  </v-card>
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
export default {
  name: 'response-card',
  props: ['response-card'],
  data() {
    return {
      hasButtonBeenClicked: false,
    };
  },
  computed: {
  },
  methods: {
    onButtonClick(value) {
      this.hasButtonBeenClicked = true;
      const message = {
        type: 'human',
        text: value,
      };

      this.$store.dispatch('postTextMessage', message);
    },
  },
};
</script>

<style scoped>
.card {
  width: 75vw;
  position: inherit; /* workaround to card being displayed on top of toolbar shadow */
  padding-bottom: 0.5em;
      height: auto;
    position: relative;
    display: -ms-flexbox;
    display: flex;
    -ms-flex-direction: column;
    flex-direction: column;
    min-width: 0;
    word-wrap: break-word;
    background-color: #fff;
    background-clip: border-box;
    border: 1px solid rgba(0,0,0,.125);
    border-radius: .25rem;
    box-shadow: 0 0 0 0 rgba(0,0,0,0);
}
.btn {
    background-color: rgba(49, 184, 150, 1) !important;
    color: #fff;
    border-radius: 11px;
    display: inline-block;
    font-weight: 800;
    text-align: center;
    white-space: nowrap;
    vertical-align: middle;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    border: 1px solid transparent;
    padding: .375rem .75rem;
    font-size: 1rem;
    line-height: 1.5;
    border-radius: .25rem;
    transition: color .15s ease-in-out,background-color .15s ease-in-out,border-color .15s ease-in-out,box-shadow .15s ease-in-out;
    box-shadow: 0 0 0 0 !important;
}
.card__title {
  padding: 0.5em;
  padding-top: 0.75em;
  font-family: 'Nunito Sans', sans-serif;
}
.card__text {
  padding: 0.33em;
  font-family: 'Nunito Sans', sans-serif;
  text-align: center;
  padding: 10px;
}
.card__actions.button-row {
  justify-content: center;
  padding-bottom: 0.15em;
  font-family: 'Nunito Sans', sans-serif;
}
</style>
