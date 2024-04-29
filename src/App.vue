<template>
  <div class="background">
    <h1>Editor Activity </h1> 
    
    <table>
      <thead>
        <tr>
          <th>Kegiatan</th>
          <th>Status</th>
          <th>Tindakan</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="activity in activities" :key="activity.id" :class="{ completed: activity.completed }">
          <td>
            <span :style="{ 'text-decoration': activity.completed ? 'line-through' : 'none' }">{{ activity.name }}</span>
          </td>
          <td>
            <span v-if="activity.completed">Telah Selesai</span>
            <span v-else>Belum Selesai</span>
            <input type="checkbox" v-model="activity.completed">
          </td>
          <td>
            <button @click="cancelActivity(activity.id)">Hapus</button>
          </td>
        </tr>
      </tbody>
    </table>

    <form @submit.prevent="addActivity">
      <input type="text" v-model="newActivity" placeholder="Masukkan kegiatan baru">
      <button type="submit">Tambahkan</button>
    </form>
  </div>
</template>

<script>
  const { ref } = Vue;

  const activities = ref([
    { id: 1, name: 'Berenang', completed: false },
  ]);


  const newActivity = ref('');


  function addActivity() {
    if (newActivity.value.trim() !== '') {
      activities.value.push({ id: Date.now(), name: newActivity.value, completed: false });
      newActivity.value = '';
    }
  }


  function cancelActivity(id) {
    const index = activities.value.findIndex(activity => activity.id === id);
    if (index !== -1) {
      activities.value.splice(index, 1);
    }
  }

  Vue.createApp({
    setup() {
      return { activities, newActivity, addActivity, cancelActivity };
    }
  }).mount('#app');
</script>


<style>
h1{
  font-family: Arial, Helvetica, sans-serif;
  text-align: center;
}
.background {
    background-image: url(bg.jpg);
    background-repeat: no-repeat;
    background-size: cover;
    min-height: 100vh; 
    padding: 20px;
    
}

form {
  font-family: Arial, Helvetica, sans-serif;
  text-align: center;
}


  table {
    width: 100%;
    border-collapse: collapse;
  }
  th, td {
    font-family: Arial, Helvetica, sans-serif;
    border: 1px solid black;
    padding: 8px;
    text-align: left;
  }

  th {
    color: white;
    background-color: rgb(0, 0, 0);
  }

  
  .completed span {
    text-decoration: line-through;
  }
</style>
