<template>
    <div>
       <div>
       <button  
       @click="addMeting()"
       >{{buttonText}}</button>
       <h2 v-if="!meetings.length">Brak zaplanowyanycyh zajęć</h2>
       <h2 v-else>Zaplanowane zajęcia {{meetings.length}}</h2>
        </div>

       <div v-show="showAddMeting">
       <new-meeting-form @added="addNewMeeting($event)"></new-meeting-form>
       </div>
       
       <meetings-list 
                      @removed="removeMeeting($event)"
                      @addedParticipant="addParticipant($event)"
                      @removedParticipant="removeParticipant($event)"
                      :meetings="meetings"
                      :email = "email" 
                        ></meetings-list>
    </div>
</template>






<script>
import NewMeetingForm from "./NewMeetingForm";
import MeetingsList from "./MeetingsList";

export default {
  components: { NewMeetingForm, MeetingsList },

  props: ["email"],

  data() {
    return {
      meetings: [],
      showAddMeting: false
    };
  },

  methods: {
    addNewMeeting(meeting) {
      this.meetings.push(meeting);
      this.showAddMeting = false;
    },
    addMeting() {
      this.showAddMeting = true;
    },

    removeMeeting(meeting) {
      this.meetings.splice(this.meetings.indexOf(meeting), 1);
    },

    addParticipant(meeting) {
      console.log("DUPA");
      meeting.participants.push(this.email);
      this.meetings.sort(); /// MASAKRA 3h szuknania by się stało reakwtwe
    },

    removeParticipant(meeting) {
      console.log("DUPA2");
      meeting.participants.splice(meeting.participants.indexOf(this.email), 1);
      this.meetings.sort();
    }
  },
  computed: {
    buttonText() {
      if (!this.meetings.length) {
        return "Dodaj Nowe Zajęcia";
      } else {
        return "Dodaj Kolejne zajecia";
      }
    }
  }
};
</script>