<template>
    <div>
        <NavBar />

        <div class="container">
            <EditModal :music="selectedMusic" />
            <DeleteModal :music="selectedMusic" @onDeleted="getAll" />
            
            <h1>
                <MusicEntryModal class="float-right" @onAdd="getAll" />
                Music
            </h1>

            <table class="table table-boredered">
                <thead>
                    <tr class="bg-info text-white">
                        <th>Music Tittle</th>
                        <th>Description</th>
                        <th>Artist Name</th>
                        <th>TopList</th>
                        <th>Released On</th>
                        <th>Status</th>
                        <th>&nbsp;</th>
                        <th>&nbsp;</th>
                    </tr>
                </thead>

                <tbody>
                    <tr v-for="music in musics" :key="music.id">
                        <td>{{music.music_tittle}}</td>
                        <td>{{music.description}}</td>
                        <td>{{music.artist_name}}</td>
                        <td>{{music.toplist}}</td>
                        <td>{{music.released_on}}</td
                        <td>{{music.status}}</td>
                        <td>
                            <b-button @click="onEdit(music)" variant="info" size="sm">Edit</b-button>
                        </td>
                        <td>
                            <b-button @click="onDelete(music)" variant="danger" size="sm">Delete</b-button>
                        </td>
                    </tr>
                </tbody>

            </table>

        </div>

    </div>
</template>

<script>
export default {
    data() {
        return {
            musics: [],
            selectedMusic: {}
        }
    },
    methods: {
        async getAll() {
            await this.$axios.get('http://localhost:8000/api/musics')
            .then((res)=>{
                if(res.status==200) {
                    this.musics = res.data
                    console.log(this.musics)
                }
            })
        },
        onEdit(selectedMusic) {
            this.selectedMusic = selectedMusic;
            this.$bvModal.show('editModal')
        },
        onDelete(selectedMusic) {
            this.selectedMusic = selectedMusic;
            this.$bvModal.show('deleteModal')
        }
    },
    created() {
        this.getAll()
    }
}
</script>