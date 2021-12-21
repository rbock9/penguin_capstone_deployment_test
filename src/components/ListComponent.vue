<template>
    <div class="row">
        <div class="col-md-12">
            <table class="table table-striped">
                <thead class="thead-dark">
                    <tr>
                        <th>Title</th>
                        <th>Publisher</th>
                        <th>Platform</th>
                        <th>Release Date</th>
                        <th>Actions</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="game in Games" :key="game._id">
                        <td>{{ game.title }}</td>
                        <td>{{ game.publisher }}</td>
                        <td>{{ game.platform }}</td>
                        <td>{{ game.release }}</td>
                        <td>
                            <router-link :to="{name: 'edit', params: { id: game._id }}" class="btn btn-success">Edit
                            </router-link>
                            <button @click.prevent="deleteGame(game._id)" class="btn btn-danger">Delete</button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
    import axios from "axios";

    export default {
        data() {
            return {
                Games: []
            }
        },
        created() {
            let apiURL = 'https://rb-penguin-project5-backend.herokuapp.com/games/';
            axios.get(apiURL).then(res => {
                this.Games = res.data;
            }).catch(error => {
                console.log(error)
            });
        },
        methods: {
            deleteGame(id){
                let apiURL = `https://rb-penguin-project5-backend.herokuapp.com/games/${id}`;
                let indexOfArrayItem = this.Games.findIndex(i => i._id === id);

                if (window.confirm("Do you really want to delete?")) {
                    axios.delete(apiURL).then(() => {
                        this.Games.splice(indexOfArrayItem, 1);
                    }).catch(error => {
                        console.log(error)
                    });
                }
            }
        }
    }
</script>

<style>
    .btn-success {
        margin-right: 10px;
    }

</style>