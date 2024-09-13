
<template>
    <div :class="windowClass">
        <img src="../assets/genshin.png" class="genshin" :disabled="true">
        <emailInput/>
    </div>
</template>

<script setup>
    import emailInput from './emailInput.vue';
</script>
<script>



export default {
    
    data(){
        return {
            windowClass: ["window", "fadeInDown"]
        }
    }
}

</script>