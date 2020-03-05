<template lang="html">
  <div class="booking">
    <div v-if="!edit" class="booking-wrapper">

      <details>

        <summary>
          <b>{{booking.name}}</b>
        </summary>
        <br><hr><br>

        <div class="booking-element-email">
          <h3><span><b>E-mail:  </b></span>{{booking.emailAddress}}</h3>
        </div>

        <div class="booking-element-checkin">
          <div v-if="booking.checkedIn" class="checked-in-container">
            <h3 class="checked-in">Checked in</h3>
          </div>
          <div class="check-in-button">
            <button
              name="check-in"
              v-if="!booking.checkedIn"
              @click="handleCheckIn"> Check in
            </button>
          </div>

        </div>

        <button name="delete" @click="handleDelete">Delete booking</button>
        <button name="edit" @click="handleEdit">Edit booking</button>
      </details>

    </div>

    <div v-if="edit" class="booking-wrapper">
      <details>
        <summary>
          <b>{{booking.name}}</b>
        </summary>

        <form class="edit-booking" @submit.prevent="handleUpdate">
          <div class="edit-wrapper">
            <label for="name">Name: </label>
            <input type="text" name="name" :value="booking.name">
          </div>
          <div class="edit-wrapper">
            <label for="emailAddress">E-mail: </label>
            <input type="text" name="emailAddress" :value="booking.emailAddress">
          </div>

          <div class="edit-wrapper">
            <input type="submit" value="Confirm changes">
          </div>

        </form>
      </details>
    </div>

  </div>
</template>

<script>
import {eventBus} from '@/main.js'

export default {
  name: "booking",
  data() {
    return {
      edit: false
    }
  },
  props: ['booking'],
  methods: {
    handleCheckIn() {
      this.booking.checkedIn = true
      eventBus.$emit('update-booking', this.booking)
    },

    handleDelete(){
      eventBus.$emit('delete-booking', this.booking._id)
    },

    handleEdit(){
      this.edit = true
    },

    handleUpdate(event){
      this.booking.name = event.target.elements[0].value
      this.booking.emailAddress = event.target.elements[1].value
      eventBus.$emit('update-booking', this.booking)
      this.edit = false
    }
  }
}
</script>

<style lang="css" scoped>

  .checked-in {
    color: ghostwhite;
  }

  .checked-in-container {
    background-color: #F4B41A;
    padding: 0.2em 3em;
    border-radius: 4em;
    margin: 1em 1em 1em 1em;
    border: 3px solid #F4B41A;
  }

  .checked-in-container:hover {
    cursor: default;
  }

  .booking {
    width: 70%;
    background-color: pink;
    padding: 1em;
    margin: 0.5em 1em;
    border-radius: 4em;
    background-color: #143D59;
    color: white;
  }

  summary {
    font-size: 1.5em;
  }

  summary:focus {
    outline: none;
    user-select: none;
  }

  .booking-wrapper h3 {
    font-size: 1.5em;
    padding: 0.5em 0;
  }

  .booking-wrapper h3 span {
    font-size: 1.1em;
  }

  .booking-element-email {
    width: 60%;
    display: inline-flex;
    justify-content: center;
  }

  .booking-element-checkin {
    width: 35%;
    display: inline-flex;
    justify-content: center;
  }

  hr {
    border: 1px solid #F4B41A;
    border-radius: 4em;
    margin: 0 5%;
  }

  .booking-wrapper button {
    padding: 0.6em 1.5em;
    border-radius: 4em;
    margin: 1em 1em 1em 1em;
    font-size: 1em;
  }

  .booking-wrapper button:hover {
    opacity: 0.8;
    cursor: pointer;
  }

  .booking-wrapper button:focus {
    outline: none;
  }

  .booking-wrapper button[name="delete"] {
    background-color: orangered;
    border: none;
    color: ghostwhite;
  }

  .booking-wrapper button[name="edit"] {
    background-color: steelblue;
    border: none;
    color: ghostwhite;
  }

  .edit-booking {
    padding: 3em 0;
    display: flex;
    width: 100%;
    justify-content: center;
    flex-wrap: wrap;
  }

  .edit-wrapper {
    width: 45%;
    margin: 0 1em;
  }

  .edit-wrapper label {
    font-size: 1.5em;
  }

  .edit-wrapper input {
    padding: 1em 2em;
    width: 100%;
    border-radius: 2em;
    border: none;
    font-size: 1em;
  }

  .edit-wrapper input[type="submit"] {
    font-size: 1.2em;
    color: ghostwhite;
    background-color: #F4B41A;
    margin-top: 2em;
  }

  .check-in-button button {
    border: 3px solid #F4B41A;
    background-color: inherit;
    padding: 0.5em 2em;
    border-radius: 4em;
    color: white;
    font-size: 1.5em;
  }

  .check-in-button button:hover {
    cursor: pointer;
    background-color: #F4B41A;
    border: 3px solid ghostwhite;
  }






</style>
