
<template>
    <div :class="windowClass">
        <img src="../assets/genshin.png" class="genshin">
        <emailInput @updateEmail="updateEmailHandler"/>
        <TransitionGroup name="fade">
            <passwordInput v-if="isDisplayPWInput()"  @updatePW="updatePWHandler"/>
            <ensurePwInput v-if="isDisplayPWInput()" @updateEnsureStatus="updateEnsureStatusHandler" :register="register" :password="password"/>
        </TransitionGroup>
        <button :disabled="isDisabled[0]" class="niceButton" @click="continueHandler" v-if="status[0] == 0"><span>继续</span></button>
        <button :disabled="isDisabled[1] || isDisabled[2]" class="niceButton" @click="registerHandler"  v-if="status[0] == 1 && register"><span>注册</span></button>
        <button :disabled="isDisabled[1]" class="niceButton" @click="loginHandler" v-if="status[0] == 1 && !register"><span>登录</span></button>
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
            register: false,
            email: "",
            password: "",
            status: [0, 0, 0],
            isDisabled: [true, true, true]
        }
    },
    methods:{
        updatePWHandler(data){
            if(data.password != ""){
                this.password = data.password
            }
            this.isDisabled[1] = data.isDisabled
        },
        updateEmailHandler(data){
            if(data.email != "") {
                this.email = data.email
            }
            this.isDisabled[0] = data.isDisabled
        },
        updateEnsureStatusHandler(status){
            this.isDisabled[2] = status
        },
        continueHandler(){
            if(this.email != ""){
                this.status[0] = 1
                if(localStorage.getItem(this.email) != null) {
                    this.register = false
                    this.windowClass[2] = "window__login"
                } else {
                    this.register = true
                    this.windowClass[2] = "window__register"
                }
            }
        },
        isDisplayPWInput(){
            if(this.status[0] == 0) {
                return false
            }
            return true
        },
        registerHandler(){
            localStorage.setItem(this.email, this.password)
            alert("注册成功")
            this.resetToEmailInput()
        },
        loginHandler(){
            if(localStorage.getItem(this.email) == this.password){
                alert("登录成功")
            } else {
                alert("密码错误")
            }
        },
        resetToEmailInput() {
            this.password = "";
            this.status[0] = 0;
            this.register = false;
            this.windowClass[2] = "";
            this.isDisabled[1] = true;
            this.isDisabled[2] = true;
        },
    }
}

</script>