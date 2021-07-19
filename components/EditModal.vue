<template>
    <div>

        <b-modal id="editModal" title="Music Entry" ok-title="Save" @ok="onSubmit">
            <form action="#">
                <b-form-group
                    label="Music Tittle"
                    label-for="music_tittle"
                    >
                    <b-form-input id="music_tittle" v-model="music.music_tittle" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="Description"
                    label-for="description"
                    >
                    <b-form-input id="description" v-model="music.description" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="Artist Name"
                    label-for="artist_name"
                    >
                    <b-form-input id="artist_name" v-model="music.artist_name" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="TopList"
                    label-for="toplist"
                    >
                    <b-form-input id="toplist" v-model="music.toplist" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="Released On"
                    label-for="released_on"
                    >
                    <b-form-input id="released_on" type="number" v-model="music.released_on" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="Status"
                    label-for="status"
                    >
                    <b-form-select id="status" v-model="music.status" :options="statuses"></b-form-select>
                </b-form-group>
            </form>
        </b-modal>
    </div>
</template>

<script>
export default {
    props: {
        music: {}

    },
    
    data() {
        return {
            music: {},
            statuses: [
                { value: 'good', text: 'Good' },
                { value: 'very good', text: 'Very Good' },
                { value: 'bad', text: 'Bad' },
                { value: 'very bad', text: 'Very Bad' },
                
            ]
        }
    },
    methods: {
        async onSubmit() {
            this.$axios.put('http://localhost:8000/api/musics/' + this.music.id, this.music)
            .then((res)=>{
                if(res.status==202) {
                    alert('Update Successfully')
                }
            })
            .catch((err)=>{
                alert(err.message)
            })
        }
    }
    
}
</script>