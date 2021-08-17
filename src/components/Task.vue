<template>
    <div class="card">
        <div class="card-content">
            <div class="media">
                <div class="media-content">
                    <p class="title is-4">{{task.name}}</p>
                    <p class="subtitle is-6">{{task.description}}</p>
                    <p class="subtitle is-6">{{task.status}}</p>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props:{
        name: String,
        description: String,
        status: Boolean
    },
    data(){
        return{            
            task: {
                name: "Tarefa simples",
                description: "tarefa elaboradamente complexa",
                status: false
            }
        }
    }
}
</script>

<style>
.card{
    margin-top: 3%;
}

</style>