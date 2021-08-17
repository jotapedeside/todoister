<template>
    <div class="d-flex flex-column justify-content-center align-items-center h-100 my-1">
        <div class="inputParam d-flex flex-column">
            <b-card class="w-100 h-100">
                <div>
                    <div class="d-flex flex-row justify-content-between align-items-center">
                        <div></div>
                    <h3 class="title is-4">{{name}}</h3>
                        <b-button>
                            <b-icon-x font-scale="2"></b-icon-x>
                        </b-button>
                    </div>
                    <p class="subtitle is-6">{{description}}</p>
                    <p class="subtitle is-6">{{status}}</p>
                    <div>
                        <b-button @click="changeStuff" variant="primary w-100">
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
        name: String,
        description: String,
        status: Boolean
    },
    data(){
        return{

        }
    },
    methods:{
        changeStuff(){
            this.status = !this.status;
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