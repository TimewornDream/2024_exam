<template>
    <div :class="windowClass">123</div>
</template>

<script>

export default {
    data(){
        return {
            msg: "你好",
            windowClass: ["window", "fadeInDown"]
        }
    }
}

</script>