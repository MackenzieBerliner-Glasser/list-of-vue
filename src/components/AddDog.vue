<template>
  <form v-on:submit.prevent="handleSubmit">
    <div v-if="errors.length">
      <b>Please correct the following error(s):</b>
      <p v-for="error in errors"
       v-bind:key="error"
       > {{ error }}</p>
    </div>
    <p>
      <label>
        Name: <input v-model="name" placeholder="Dogo Name">
      </label>
    </p>
    <p>
      <label>
        Type: <input v-model="type" placeholder="Dogo Type">
      </label>
    </p>
    <p>
      <label>
        Food: <input v-model="food" placeholder="Favorite Food">
      </label>
    </p>
    <p>
      <label>
        Image: <input v-model="img" placeholder="Dogo Image">
      </label>
    </p>
    <p>
      <button>Add A Dogo</button>
    </p>
  </form>
</template>

<script>
export default {
  props: {
    onAdd: Function
  },
  data() {
    return {
      errors: [],
      name: '',
      type: '',
      food: '',
      img: ''
    };
  },
  methods: {
    checkForm() {
      this.errors = [];

      if(!this.name) {
        this.errors.push('Name required.');
      }
      if(!this.type) {
        this.errors.push('Type required.');
      }

      if(!this.food) {
        this.errors.push('Food required.');
      }
      if(!this.img) {
        this.errors.push('Image required.');
      }
      return !this.errors.length;
    },
    handleSubmit() {
      this.errors = [];
      if(!this.checkForm()){
        return;
      }
      const newDogo = {
        name: this.name,
        type: this.type,
        food: this.food,
        img: this.img
      };
      this.onAdd(newDogo);

      this.name = '';
      this.type = '';
      this.food = '';
      this.img = '';
    }
  }
};
</script>

<style>

</style>
