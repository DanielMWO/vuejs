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
                <td> <ul> <li v-for ="participant in partictpants" :key = "participant.id">{{participant}} </li> </ul></td>
                <td v-if="!iAmInMeeting"><button
                @click ="enroll()">
                Zapisz Się</button></td>
                
                <td v-else><button
                @click="resign()"
                >Wypisz Się</button></td>

                <td v-if="emptyMeeting"><button
                @click="removeMeeting(meeting.name)"
                >Usuń Puste Spotkanie</button></td>

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
        enroll(){
            this.partictpants.push(this.email)
        },
        resign(){
            this.partictpants.splice(this.partictpants.indexOf(this.email), 1)
        },

         removeMeeting(meeting) {
             console.log(meeting)
             this.$emit(removeMeeting, meeting)
             
             
        }
    },
    
    computed:{
        
        
       
        
        emptyMeeting() {
            if (!this.partictpants.length) {
                return true;
            }
            else {
                return false;}
        
        },
        iAmInMeeting() {
            if (this.partictpants.includes(this.email)) {
                return true;
                }
            else {return false;}
            

        }
    }
        

}
</script>