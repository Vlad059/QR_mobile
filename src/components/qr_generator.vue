<template>
    <div>
        <input v-model="read_string">
        <qrcode-vue :value="read_string" :size="300" level="H"></qrcode-vue>
    </div>   
</template>

<script>
import QrcodeVue from 'qrcode.vue'

export default {
    data (){
        return {
            read_string: ''
        }
    },
    components: {
        QrcodeVue
    }
}

</script>


<style>
</style>