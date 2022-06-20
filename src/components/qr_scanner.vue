<template>
    <div class="qr_scan_div">
        <label>Ошибка: {{ error }}</label>
        <label>Строка из QR кода: {{gen_string}}</label>
        <qrcode-stream @init="onInit" @decode="onDecode" :camera="cam"/>
    </div>    
</template>

<script>
import {QrcodeStream} from 'vue3-qrcode-reader'

export default{
    data (){
        return {
            gen_string: '',
            error: '',
            cap: null,
            cam: 'auto'
        }
    },
    methods:{
        onDecode(decodedString){
            this.gen_string = decodedString;
        },
        async onInit (promise){
            // show loading indicator
            try {
                const { capabilities } = await promise;
                this.cap = capabilities;
                this.error = 'No errors';
            } catch (error) {
                if (error.name === 'NotAllowedError') {
                    this.error = 'user denied camera access permisson';
                } else if (error.name === 'NotFoundError') {
                    this.error = 'no suitable camera device installed';
                } else if (error.name === 'NotSupportedError') {
                    this.error = 'page is not served over HTTPS (or localhost)';
                } else if (error.name === 'NotReadableError') {
                    this.error = 'maybe camera is already in use';
                } else if (error.name === 'OverconstrainedError') {
                    this.error = 'did you requested the front camera although there is none?';
                } else if (error.name === 'StreamApiNotSupportedError') {
                    this.error = 'browser seems to be lacking features';
                }
            } finally {
                // hide loading indicator
            }
        },        
    },
    components: {
        QrcodeStream
    }
}
</script>

<style>
.qr_scan_div {
    display: flex;
    flex-direction: column;
}
</style>