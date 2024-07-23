<template>
  <div>
    <h2>Message Detail</h2>
    <div v-if="message">
      <p><strong>ID:</strong> {{ message.uuid }}</p>
      <div class="json-container">
        <pre><code>{{ formatJson(message.MessageContent) }}</code></pre>
      </div>
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
  name: 'SqlMessageDetails',
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

    const formatJson = (content) => {
      try {
        return JSON.stringify(JSON.parse(content), null, 2);
      } catch (e) {
        console.error('Failed to parse JSON content', e);
        return content;
      }
    };

    return { message, formatJson };
  }
});
</script>

<style scoped>
.json-container {
  color: #2c3e50;
  padding: 20px;
  border-radius: 8px;
  overflow: auto;
  max-width: 600px;
  margin: 20px auto;
  font-family: 'Courier New', Courier, monospace;
  text-align: left;
}
.json-container pre {
  margin: 0;
}
.json-container code {
  white-space: pre;
  display: block;
}
</style>
