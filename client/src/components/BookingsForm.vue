<template lang="html">
  <form class="bookings-form" @submit.prevent="handleSubmit">
    <h1>Add Booking</h1>
    <div class="form-wrapper">
      <label for="name">Name:</label>
      <input type="text" name="name" v-model="newBooking.name" required>
    </div>
    <div class="form-wrapper">
      <label for="emailAddress">E-mail:</label>
      <input type="email" name="emailAddress" v-model="newBooking.emailAddress" required>
    </div>
    <div class="form-wrapper">
      <input type="submit" value="Create Booking">
    </div>
  </form>
</template>

<script>
import {eventBus} from '@/main.js'

export default {
  name: "bookings-form",
  data() {
    return {
      newBooking: {
        name: "",
        emailAddress: "",
        checkedIn: false
      }
    }
  },
  methods: {
    handleSubmit() {
      eventBus.$emit('submit-booking', this.newBooking);
      this.newBooking = {
        name: "",
        emailAddress: "",
        checkedIn: false
      }
    }
  }
}
</script>

<style lang="css" scoped>

  .bookings-form {
    padding: 3em 0;
    background-color: whitesmoke;

  }

  .bookings-form h1 {
    padding: 0.5em 0;
    font-family: 'Roboto Slab', serif;
    font-size: 3em;
  }

  .form-wrapper input {
    padding: 1em 2em;
    margin: 1em 1em;
    border-radius: 2em;
    border: none;
    font-size: 1em;
    width: 20%;
  }

  .form-wrapper input[type="submit"] {
    background-color: #F4B41A;
    color: ghostwhite;
    font-size: 1.2em;
  }

  .form-wrapper input[type="submit"]:hover {
    cursor: pointer;
  }

  .form-wrapper input:focus {
    outline: none;
  }

  .form-wrapper input:hover {
    opacity: 80%;
  }

  .form-wrapper label {
    font-size: 1.2em;
  }


</style>
