<template>
    <table v-if="meetings.length > 0">
        <thead>
            <tr>
                <th>Nazwa spotkania</th>
                <th>Opis</th>
                <th>Uczestnicy</th>
                
            </tr>
        </thead>
        <tbody>
            <tr v-for="meeting in meetings" :key="meeting.name">
                <td>{{ meeting.name }}</td>
                <td>{{ meeting.description }}</td>
                <td> <ul> <li v-for ="participant in meeting.participants" :key = "participant.id">{{participant}} </li> </ul></td>
                <td v-if="!meeting.participants.includes(email)"><button
                @click.capture ="enroll(meeting)">
                Zapisz Się</button></td>
                
                <td v-else><button
                @click="resign(meeting)"
                >Wypisz Się</button></td>

                <td v-if="!meeting.participants.length"><button
                @click="removeEmptyMeeting(meeting)">
                Usuń Puste Spotkanie</button></td>

            </tr>
        </tbody>
    </table>
</template>

<script>
export default 
{
    props:  
        ['meetings','email'],

    data() 
    {
        return{
            partictpants: [],
           
        }
    },
    methods: {
        enroll(meeting){
            this.$emit('addedParticipant', meeting)
        },
        resign(meeting){
             ///console.log("dupa2")
             this.$emit('removedParticipant', meeting)
        },

         removeEmptyMeeting(meeting) {
            this.$emit('removed', meeting);
             
             
        }
    },
    
    computed:{
        
        
       
        
        emptyMeeting(meeting) {
            if (!meeting.participants.length) {
                return true;
            }
            else {
                return false;}
        
        },
        iAmInMeeting(meeting) {
            if (meeting.participants.includes(this.email)) {
                return true;
                }
            else {return false}
            

        }
    }
        

}
</script>