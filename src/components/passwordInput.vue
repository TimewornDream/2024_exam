<template>
    <div>
        <span :class="inputClass" >
            <input class="input__field--jiro" :type="inputType" id="email-input" v-model="input" :style="{ letterSpacing: inputLetterSpacing }"/>
            <label class="input__label--jiro" for="email-input" :style="{ color: allColor[index]}">
                <span class="input__label-content--jiro" >密码{{ addContent }}</span>
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
        watch:{
            input(newInput){
				this.$emit("updatePW", newInput)

                // 内容不为空，保持展开
                if(newInput != ""){
                    this.inputClass[2] = "input--filled"
                } else {
                    this.inputClass[2] = ""
                    this.index = 0
                    this.addContent = ""
                    return
                }
                
                const re = new RegExp("^.*(?=.{8,})(?=.*\\d)(?=.*[A-Z])(?=.*[a-z])(?=.*[!@#$%^&*? ]).*$")
                if(re.test(newInput)){
                    this.index = 0
                    this.addContent = ""
                } else {
                    this.index = 1
                    this.addContent = "（请确保至少含有1个大写字母、小写字母、数字、特殊符号，密码长度大于8位）"
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

<style lang="scss" scoped>


.input--jiro {
    position: relative;
	z-index: 1;
	display: inline-block;
	margin: 1em;
	width: 20rem;
	vertical-align: top;
	margin-top: 2em;
}

.input__field--jiro {
    outline: none;
    position: relative;
	display: block;
	float: left;
	border: none;
	border-radius: 0;
	font-weight: bold;
	font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
	padding: 0.85em 0.5em;
	width: 100%;
	background: transparent;
	color: #DDE2E2;
	opacity: 0;
	-webkit-transition: opacity 0.3s;
	transition: opacity 0.3s;
}

.input__label--jiro {
    display: inline-block;
	padding: 0 1em;
	width: 40%;
	font-weight: bold;
	font-size: 80%;
	-webkit-touch-callout: none;
	-webkit-user-select: none;
	-khtml-user-select: none;
	-moz-user-select: none;
	-ms-user-select: none;
	user-select: none;
	position: absolute;
	left: 0;
	padding: 0 0.85em;
	width: 100%;
	height: 100%;
	text-align: left;
	pointer-events: none;
}

.input__label-content--jiro {
    position: relative;
	display: block;
	padding: 1.6em 0;
	width: 100%;
	-webkit-transition: -webkit-transform 0.3s 0.3s;
	transition: transform 0.3s 0.3s;
}

.input__label--jiro::before,
.input__label--jiro::after {
	content: '';
	position: absolute;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
	-webkit-transition: -webkit-transform 0.3s;
	transition: transform 0.3s;
}

.input__label--jiro::before {
	border-top: 2px solid #3a6089;
	-webkit-transform: translate3d(0, 100%, 0) translate3d(0, -2px, 0);
	transform: translate3d(0, 100%, 0) translate3d(0, -2px, 0);
	-webkit-transition-delay: 0.3s;
	transition-delay: 0.3s;
}

.input__label--jiro::after {
	z-index: -1;
	background: #3a6089;
	-webkit-transform: scale3d(1, 0, 1);
	transform: scale3d(1, 0, 1);
	-webkit-transform-origin: 50% 0%;
	transform-origin: 50% 0%;
}

.input__label--jiro__currect {
    z-index: -1;
	background: #ff3223;
	-webkit-transform: scale3d(1, 0, 1);
	transform: scale3d(1, 0, 1);
	-webkit-transform-origin: 50% 0%;
	transform-origin: 50% 0%;
}

.input__field--jiro:focus,
.input--filled .input__field--jiro {
	opacity: 1;
	-webkit-transition-delay: 0.3s;
	transition-delay: 0.3s;
}

.input__field--jiro:focus + .input__label--jiro .input__label-content--jiro,
.input--filled .input__label-content--jiro {
	-webkit-transform: translate3d(0, -80%, 0);
	transform: translate3d(0, -80%, 0);
	-webkit-transition-timing-function: cubic-bezier(0.2, 1, 0.3, 1);
	transition-timing-function: cubic-bezier(0.2, 1, 0.3, 1);
}

.input__field--jiro:focus + .input__label--jiro::before,
.input--filled .input__label--jiro::before {
	-webkit-transition-delay: 0s;
	transition-delay: 0s;
}

.input__field--jiro:focus + .input__label--jiro::before,
.input--filled .input__label--jiro::before {
	-webkit-transform: translate3d(0, 0, 0);
	transform: translate3d(0, 0, 0);
}

.input__field--jiro:focus + .input__label--jiro::after,
.input--filled .input__label--jiro::after {
	-webkit-transform: scale3d(1, 1, 1);
	transform: scale3d(1, 1, 1);
	-webkit-transition-delay: 0.3s;
	transition-delay: 0.3s;
	-webkit-transition-timing-function: cubic-bezier(0.2, 1, 0.3, 1);
	transition-timing-function: cubic-bezier(0.2, 1, 0.3, 1);
}
.toggle-password-btn {
  position: absolute;
  right: -5%;
  top: 30%;
  transform: translateY(-50%);
  margin-left: 1em;
  padding: 0.5em 0.5em;
  background: none;
  border: none;
  cursor: pointer;
  transition: background-color 0.3s;
  height: 80%;
}

.toggle-password-btn i {
  font-size: 16px;
}
.eyes {
  width: 2rem;
  height: 2rem;
}
</style>