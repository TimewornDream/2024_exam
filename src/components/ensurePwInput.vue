<template>
    <div v-if="register">
        <span :class="inputClass" >
			<input class="input__field--jiro" :type="inputType" id="email-input" v-model="input" :style="{ letterSpacing: inputLetterSpacing }"/>
            <label class="input__label--jiro" for="email-input" :style="{ color: allColor[index]}">
                <span class="input__label-content--jiro" >确认密码{{ addContent }}</span>
            </label>
			<button v-show="isDisplay()" @click="togglePasswordVisibility" class="toggle-password-btn">
				<img v-if="displayPW" src="../assets/eye1.svg" class="eyes" @click="eyeClickHandler">
				<img v-else="displayPW" src="../assets/eye2.svg" class="eyes" @click="eyeClickHandler">
        	</button>
		</span>
    </div>
</template>

<script>
    export default {
        data(){
            return {
                input: "",
                inputClass: ["input", "input--jiro", ""],
                inputLabelClass: ["input__label--jiro"],
                allColor: ["#3a6089", "#DC143C"],
                addContent: "",
                index: 0,
				displayPW: false,
				inputType: "password",
				inputLetterSpacing: "0.2rem"
            }
        },	
		props: {
        	register: Boolean,
			password: String
    	},
        watch:{
            input(newInput){
                // 内容不为空，保持展开
                if(newInput != ""){
                    this.inputClass[2] = "input--filled"
                } else {
                    this.inputClass[2] = ""
                    this.index = 0
                    this.addContent = ""
                    return
                }
                
                if(this.password == newInput){
                    this.index = 0
                    this.addContent = ""
					this.$emit("updateEnsureStatus", false)
                } else {
                    this.index = 1
                    this.addContent = "（两次输入密码不一致）"
					this.$emit("updateEnsureStatus", true)
                }
            }
        },
		methods:{
			isDisplay(){
				if(this.input == "") {
					return false
				} else {
					return true
				}
			},
			eyeClickHandler(){
				if(this.displayPW){
					this.displayPW = false
					this.inputType = "password"
					this.inputLetterSpacing = "0.2rem"
				} else {
					this.displayPW = true
					this.inputType = "text"
					this.inputLetterSpacing = "0"
				}
			}
		}
    }
</script>
