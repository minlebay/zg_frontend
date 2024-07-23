<template>
  <div>
    <h2>Messages from MySQL</h2>
    <table>
      <tbody>
      <tr v-for="message in messages" :key="message.uuid" @click="selectMessage(message.uuid)">
        <td>{{ message.uuid }}</td>
      </tr>
      </tbody>
    </table>
    <div class="pagination">
      <button @click="prevPage" :disabled="page === 1">Previous</button>
      <span>Page {{ page }}</span>
      <button @click="nextPage">Next</button>
      <CustomDropdown :options="[10, 20, 50]" :value="10" v-model="size" @change="handleSizeChange" />
    </div>
  </div>
</template>

<script lang="ts">
import {defineComponent, ref, onMounted, watch} from 'vue';
import {DefaultApi, Configuration} from '@/api-client';
import CustomDropdown from "@/components/CustomDropdown.vue";

export default defineComponent({
  name: 'MessageListSql',
  components: {CustomDropdown},
  emits: ['messageSelected'],
  setup(_, {emit}) {
    const messages = ref([]);
    const page = ref(1);
    const size = ref(10);

    const fetchMessages = async () => {
      const config = new Configuration({basePath: 'http://localhost:8080/api/v1'});
      const api = new DefaultApi(config);
      try {
        const response = await api.sqlGet(page.value, size.value);
        messages.value = response.data.data;
      } catch (error) {
        console.error('Failed to fetch messages', error);
      }
    };

    const selectMessage = (id: string) => {
      emit('messageSelected', id);
    };

    const nextPage = () => {
      page.value++;
    };

    const prevPage = () => {
      if (page.value > 1) page.value--;
    };

    const handleSizeChange = (newSize) => {
      page.value = 1;
      size.value = newSize
      fetchMessages();
    };

    watch([page, size], fetchMessages);

    onMounted(fetchMessages);

    return { messages, page, size, selectMessage, nextPage, prevPage, fetchMessages, handleSizeChange };
  },
});
</script>

<style scoped>
table {
  width: 100%;
  border-collapse: collapse;
}

th, td {
  padding: 8px;
  text-align: left;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

tbody tr:hover {
  background-color: #33333333;
  cursor: pointer;
}

.pagination {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 10px;
}

.pagination button {
  margin: 0 5px;
  padding: 8px 16px;
  background-color: #44444444;
  color: #2c3e50;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease, box-shadow 0.3s ease;
}

.pagination button:hover {
  background-color: #66655545;
}

.pagination button:focus {
  outline: none;
  box-shadow: 0 0 5px #66655545;
}

.pagination button:disabled {
  background-color: #33333333;
  cursor: not-allowed;
  color: #2c3e50;
}
</style>
