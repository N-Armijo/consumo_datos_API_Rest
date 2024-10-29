<script setup>
  import { ref} from 'vue';
  const props = defineProps({
    user: {
      type: Object,
      required: true,
    },
  });
  const emit = defineEmits(['enviar-mensaje']);
  const message = ref('');
  const color = ref('');
  const enviarMensaje = () => {
    emit('enviar-mensaje', message.value, color.value, props.user.name.first, props.user.side);
    message.value = '';
  }
</script>
<template>
  <div class="user-component">
    <h2>CardUser</h2>
    <div class="card" >
      <img :src="user.picture.large" class="card-img-top" alt="foto usuario" />
      <div class="card-body">
        <h5 class="card-title">{{ user.name.first }} {{ user.name.last }}</h5>
        <form @submit.prevent="enviarMensaje" >
          <input v-model="color" type="color" class="col-12 rounded"/>
          <textarea v-model="message" class="col-12 form-control mb-1" cols="5" required></textarea>
          <button class="btn btn-success col-12">Enviar</button>
        </form>
      </div>
    </div>
  </div>
</template>
