<template>
  <v-layout
    column
    fill-height
    class="message-list"
  >
    <message
      ref="messages"
      v-for="message in messages"
      v-bind:message="message"
      v-bind:key="message.id"
      v-bind:class="`message-${message.type}`"
      v-on:scrollDown="scrollDown"
    ></message>
  </v-layout>
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
import Message from './Message';

export default {
  name: 'message-list',
  components: {
    Message,
  },
  computed: {
    messages() {
      return this.$store.state.messages;
    },
  },
  watch: {
    // autoscroll message list to the bottom when messages change
    messages() {
      this.scrollDown();
    },
  },
  methods: {
    scrollDown() {
      return this.$nextTick(() => {
        this.$el.scrollTop = this.$el.scrollHeight;
      });
    },
  },
};
</script>

<style scoped>
.message-list {
  overflow-y: auto;
  overflow-x: hidden;
}

.message-bot {
  align-self: flex-start;
  padding-left: 20px;
}

.message-human {
  align-self: flex-end;
  padding-right: 20px;
}

</style>
