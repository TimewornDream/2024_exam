
<template>
    <div :class="windowClass">
        <img src="../assets/genshin.png" class="genshin">
        <emailInput @updateEmail="updateEmailHandler"/>
        <TransitionGroup name="fade">
            <passwordInput v-if="isDisplayPWInput()"  @updatePW="updatePWHandler"/>
            <ensurePwInput v-if="isDisplayPWInput()" :register="register" :password="password"/>
        </TransitionGroup>
        <button class="niceButton" @click="continueHandler"><span>继续</span></button>
        <button class="niceButton"><span>注册</span></button>
        <button class="niceButton"><span>登录</span></button>
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
            windowClass: ["window", "fadeInDown", ""],
            register: true,
            email: "",
            password: "",
            status: [0, 0, 0]
        }
    },
    methods:{
        updatePWHandler(pw){
            this.password = pw
        },
        updateEmailHandler(email){
            this.email = email
        },
        continueHandler(){
            if(this.email != ""){
                this.status[0] = 1
                this.windowClass[2] = "window__register"
            }
        },
        isDisplayPWInput(){
            if(this.status[0] == 0) {
                return false
            }
            return true
        }
    }
}

</script>