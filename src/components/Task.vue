<template>
    <div class="d-flex flex-column justify-content-center align-items-center h-100 my-1">
        <div class="inputParam d-flex flex-column">
            <b-card class="w-100 h-100">
                <div>
                    <div class="d-flex flex-row justify-content-between align-items-center">
                        <div></div>
                    <h3 class="title is-4">{{name}}</h3>
                        <b-button @click="sendEventDelete">
                            <b-icon-x font-scale="2"></b-icon-x>
                        </b-button>
                    </div>
                    <p class="subtitle is-6">{{description}}</p>
                    <div>
                        <b-button @click="sendEventComplete" variant="primary w-100">
                            <b-icon icon="check" font-scale="2"></b-icon>
                        </b-button>
                    </div>
                </div>
            </b-card>
        </div>
    </div>
</template>

<script>
export default {
    props:{
        id: String,
        name: String,
        description: String,
        status: Boolean
    },
    data(){
        return{

        }
    },
    methods:{
        //send Event complete
        sendEventComplete: function(){
            this.$emit("completeMe", {taskId: this.id, component: this});
        },
        //send Event delete
        sendEventDelete: function(){
            this.$emit("deleteMe", {taskId: this.id, component: this});
        }
    }
}
</script>

<style>
.card{
    margin-top: 3%;
}
.inputParam{
  min-width: 400px;
  width: 35%;
}
</style>