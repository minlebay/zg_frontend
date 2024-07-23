<template>
  <div>
    <h2>Messages from MongoDB</h2>
    <ul>
      <li v-for="message in messages" :key="message.id" @click="selectMessage(message.uuid)">
        {{ message.uuid }}
      </li>
    </ul>
    <button @click="fetchMessages">Load More</button>
  </div>
</template>

<script lang="ts">
import {defineComponent, ref} from 'vue';
import {DefaultApi, Configuration} from '@/api-client';

export default defineComponent({
  name: 'MessageListNoSql',
  emits: ['messageSelected'],
  setup(_, {emit}) {
    const messages = ref([]);
    const page = ref(1);
    const size = ref(10);

    const fetchMessages = async () => {
      const config = new Configuration({basePath: 'http://localhost:8080/api/v1'});
      const api = new DefaultApi(config);
      try {
        const response = await api.nosqlGet(page.value, size.value);
        console.log(response);
        messages.value = [...messages.value, ...response.data.data];
        page.value++;
      } catch (error) {
        console.error('Failed to fetch messages', error);
      }
    };

    const selectMessage = (id: string) => {
      console.log('Selected message:', id);
      emit('messageSelected', id);
    };

    return {messages, fetchMessages, selectMessage};
  },

  mounted() {
    this.fetchMessages();
  }
});
</script>
