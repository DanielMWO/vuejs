<template>
    <form @submit.prevent="addNewMeeting()">
            <h3>Dodaj nowe spotkanie</h3>
            <label>Nazwa</label>
            <input type="text" v-model="newMeeting.name">
            <label>Opis</label>
            <textarea v-model="newMeeting.description"></textarea>
            <button 
                     @click="verifyNotEmpty()"
            >Dodaj</button>
            <p v-if="displayNotice">Nazwa spotkanie nie może być pusta</p>
        </form>
</template>

<script>
export default {
  data() {
    return {
      newMeeting: {},
      meetingNameEmpty: true,
      displayNotice: false
    };
  },
  methods: {
    addNewMeeting() {
      if (!this.meetingNameEmpty) {
        this.newMeeting.participants = [];
        this.$emit("added", this.newMeeting);
        this.newMeeting = {};
        this.displayNotice = false;
      }
    },
    verifyNotEmpty() {
      if (this.newMeeting.name) {
        this.meetingNameEmpty = false;
      } else {
        this.meetingNameEmpty = true;
        this.displayNotice = true;
      }
    }
  }
};
</script>