<template>
    <div class="row justify-content-center">
        <div class="col-md-6">
            <h3 class="text-center">Update Game</h3>
            <form @submit.prevent="handleUpdateForm">
                <div class="form-group">
                    <label>Title</label>
                    <input type="text" class="form-control" v-model="game.title" required>
                </div>

                <div class="form-group">
                    <label>Image URL</label>
                    <input type="text" class="form-control" v-model="game.imagelink">
                </div>

                <div class="form-group">
                    <label>Developer</label>
                    <input type="text" class="form-control" v-model="game.developer">
                </div>

                <div class="form-group">
                    <label>Publisher</label>
                    <input type="text" class="form-control" v-model="game.publisher">
                </div>

                <div class="form-group">
                    <label>Platform</label>
                    <input type="text" class="form-control" v-model="game.platform">
                </div>

                <div class="form-group">
                    <label>Release Date</label>
                    <input type="text" class="form-control" v-model="game.release">
                </div>

                <div class="form-group">
                    <label>Summary</label>
                    <input type="text" class="form-control" v-model="game.summary">
                </div>

                <div class="form-group">
                    <button class="btn btn-danger btn-block">Update</button>
                </div>
            </form>
        </div>
    </div>
</template>

<script>
import axios from "axios";

export default {
    data() {
        return {
            game: { }
        }
    },
    created() {
        // let apiURL = `http://localhost:4000/api/edit-student/${this.$route.params.id}`;
        let apiURL = `https://rb-penguin-project5-backend.herokuapp.com/games/${this.$route.params.id}`
        axios.get(apiURL).then((res) => {
            this.game = res.data;
        })
    },
    methods: {
        handleUpdateForm() {
            // let apiURL = `http://localhost:4000/api/update-student/${this.$route.params.id}`;
            let apiURL = `https://rb-penguin-project5-backend.herokuapp.com/games/${this.$route.params.id}`

            axios.put(apiURL, this.game).then((res) => {
                console.log(res)
                this.$router.push('/view')
            }).catch(error => {
                console.log(error)
            });
        }
    }
}
</script>