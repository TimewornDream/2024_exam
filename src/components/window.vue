
<template>
    <div :class="windowClass">
        <img src="../assets/genshin.png" class="genshin" :disabled="true">
        <emailInput/>
        <passwordInput  @updatePW="updatePWHandler"/>
        <ensurePwInput :register="register" :password="password"/>
    </div>
</template>

<script setup>
    import emailInput from './emailInput.vue';
    import passwordInput from './passwordInput.vue';
    import ensurePwInput from './ensurePwInput.vue'
</script>
<script>



export default {
    
    data(){
        return {
            windowClass: ["window", "fadeInDown"],
            register: true,
            password: ""
        }
    },
    methods:{
        updatePWHandler(pw){
            this.password = pw
        }
    }
}

</script>