<template>
  <div>
    <h2>Message Detail</h2>
    <div v-if="message">
      <p><strong>ID:</strong> {{ message.uuid }}</p>
      <p><strong>Content:</strong> {{ message.MessageContent }}</p>
    </div>
    <div v-else>
      <p>Loading...</p>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, watch } from 'vue';
import { DefaultApi, Configuration } from '@/api-client';

export default defineComponent({
  name: 'NoSqlMessageDetails',
  props: {
    id: {
      type: String,
      required: true
    }
  },
  setup(props) {
    const message = ref(null);

    const fetchMessage = async () => {
      const config = new Configuration({ basePath: 'http://localhost:8080/api/v1' });
      const api = new DefaultApi(config);
      try {
        const response = await api.nosqlIdGet(props.id);
        message.value = response.data.data;
      } catch (error) {
        console.error('Failed to fetch message', error);
      }
    };

    watch(() => props.id, fetchMessage, { immediate: true });

    return { message };
  }
});
</script>

<style scoped>
/* Add your styles here */
</style>
