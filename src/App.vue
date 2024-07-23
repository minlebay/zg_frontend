<template>
  <div id="app">
    <div class="container">
      <div class="column">
        <MessageListNoSql @messageSelected="selectedNoSqlMessageId = $event" />
        <NoSqlMessageDetails :id="selectedNoSqlMessageId" v-if="selectedNoSqlMessageId" />
      </div>
      <div class="column">
        <MessageListSql @messageSelected="selectedSqlMessageId = $event" />
        <SqlMessageDetails :id="selectedSqlMessageId" v-if="selectedSqlMessageId" />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import MessageListNoSql from './components/MessageListNoSql.vue';
import MessageListSql from './components/MessageListSql.vue';
import NoSqlMessageDetails from './components/NoSqlMessageDetail.vue';
import SqlMessageDetails from './components/SqlMessageDetail.vue';

export default defineComponent({
  name: 'App',
  components: {
    MessageListNoSql,
    MessageListSql,
    NoSqlMessageDetails,
    SqlMessageDetails,
  },
  setup() {
    const selectedNoSqlMessageId = ref<string | null>(null);
    const selectedSqlMessageId = ref<string | null>(null);

    return { selectedNoSqlMessageId, selectedSqlMessageId };
  }
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  align-content: center;
}

.container {
  display: flex;
  justify-content: space-around;
}

.column {
  width: 90%;
}
</style>
