<script setup>
  import { ref, onMounted } from 'vue';
  import axios from 'axios';
  import ChatBoard from '@/components/ChatBoard.vue';
  import CardUser from '@/components/CardUser.vue';

  const userLeft = ref({});
  const userRight = ref({});
  const messages = ref([]);

  const fetchUsers = async () => {
    try {
      const url = 'https://randomuser.me/api/?results=2';
      const { data } = await axios.get(url);

      userLeft.value = { ...data.results[0], side: 'left' };
      userRight.value = { ...data.results[1], side: 'right' };
    } catch (error) {
      console.error(error);
    }
  }

  const enviarMensaje = (message, color, name, side) => {
    messages.value.push({ message, color, name, side });
  }

  onMounted(() => {
    fetchUsers();
  });
</script>
<template>
  <h1>MiChat</h1>
  <div class="chat-app-container container">
    <div class="row">
      <CardUser
        :user="userLeft"
        @enviar-mensaje="enviarMensaje"
        class="col-4"
        v-if="Object.keys(userLeft).length > 0"
      />
      <ChatBoard class="col-4" :messages="messages" />
      <CardUser
        :user="userRight"
        class="col-4"
        @enviar-mensaje="enviarMensaje"
        v-if="Object.keys(userRight).length > 0"
      />
    </div>
  </div>
</template>

