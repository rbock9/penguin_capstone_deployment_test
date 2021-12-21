<template>
    <div class="row justify-content-center">
        <div class="col-md-6">
            <h3 class="text-center">Create Game</h3>
            <form @submit.prevent="handleSubmitForm">
                <div class="form-group">
                    <label>Title</label>
                    <input type="text" class="form-control" v-model="game.title" required>
                </div>

                <div class="form-group">
                    <label>Image URL</label>
                    <input type="text" class="form-control" v-model="game.imagelink">
                </div>

                <div class="form-group">
                    <label>Developer(s)</label>
                    <input type="text" class="form-control" v-model="game.developer" >
                </div>

                <div class="form-group">
                    <label>Publisher(s)</label>
                    <input type="text" class="form-control" v-model="game.publisher" >
                </div>

                <div class="form-group">
                    <label>Platform(s)</label>
                    <input type="text" class="form-control" v-model="game.platform" >
                </div>

                <div class="form-group">
                    <label>Release Date</label>
                    <input type="text" class="form-control" v-model="game.release" >
                </div>

                <div class="form-group">
                    <label>Summary</label>
                    <input type="text" class="form-control" v-model="game.summary" >
                </div>

                <div class="form-group">
                    <button class="btn btn-danger btn-block">Create</button>
                </div>
            </form>
        </div>
    </div>
</template>

<script>
import axios from "axios"

export default {
    data() {
        return {
            game: {
                title: '',
                imagelink: '',
                developer: '',
                publisher: '',
                platform: '',
                release: '',
                summary: ''
            }
        }
    },
    methods: {
        handleSubmitForm() {
            let apiURL = 'https://rb-penguin-project5-backend.herokuapp.com/games/';
                
            axios.post(apiURL, this.game).then(() => {
                this.$router.push('/view')
                this.game = {
                        title: '',
                        imagelink: '',
                        developer: '',
                        publisher: '',
                        platform: '',
                        release: '',
                        summary: ''
                }
            }).catch(error => {
                console.log(error)
            });
        }
    }
}
</script>