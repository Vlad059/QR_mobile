<template>
    <div class="qr_gen_div">
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
.qr_gen_div{
    display: flex;
    flex-direction: column;
}
</style>