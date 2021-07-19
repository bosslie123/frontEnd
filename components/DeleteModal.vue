<template>
    <div>

        <b-modal id="deleteModal" title="Delete Music" ok-title="Save" @ok="onDelete" ok-variant="danger">
            Are You Sure Want to delete this?
            <br>
            <br>
            <h1>{{music.music_tittle}}</h1>
        </b-modal>

    </div>
</template>

<script>
export default {
    props: {
        music: {}
    },
    methods: {
        async onDelete() {
            this.$axios.delete('http://localhost:8000/api/musics/' + this.music.id)
            .then((res)=>{
                if(res.status==202) {
                    alert('Music is deleted Successfully')
                    this.$emit('onDeleted')
                }
            })
        }
    }
    
}
</script>