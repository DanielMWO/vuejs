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
                <td>{{partictpants}}</td>
                <td v-if="emptyMeeting"><button
                @click ="enroll()">
                Zapisz Się</button></td>
                <td v-if="emptyMeeting"><button>Usuń Puste Spotkanie</button></td>
                <td v-else><button
                @click="resign()"
                >Wypisz Się</button></td>

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
            this.partictpants.pop(this.email)
        }
    },
    
    computed:{
        emptyMeeting() {
            if (!this.partictpants.length) {
                return true;
            }
            else {
                return false;}

        }
    }
        

}
</script>