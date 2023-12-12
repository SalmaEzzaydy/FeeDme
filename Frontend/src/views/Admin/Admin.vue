<template>
  <div class="adminPanel container">
      <router-link :to="{name : 'AdminProduct'}">
        <button type="button" class="btn btn-primary btn-lg">Admin Meals</button>
      </router-link>
      <router-link :to="{name : 'AdminCategory'}">
        <button type="button" class="btn btn-primary btn-lg">Admin Meal's Categories</button>
      </router-link>
     
  </div>
</template>

<script>
export default {
  mounted() {
    if (!localStorage.getItem('token') || localStorage.getItem('token')!='80febeb5-14e9-4354-bd22-eb54185503ad') {
      this.$router.push({name : 'Signin'});
    }
  }
}
</script>

<style>
.adminPanel{
  display : flex;
  flex-direction: column;
  align-items: center;
}
.adminPanel button{
  font-size: 30px;
  width: fit-content;
  margin: 55px 0;
  background-color: #e37878;
}
</style>