<template>
    <div v-if="show" class="wc" :class="{ show: currentShow }">
        <div class="wc-popup">
            <div class="wc-popup-inner">
                <div class="wc-popup-title" v-if="title">{{title}}</div>
                <div class="wc-popup-text">{{content}}</div>
            </div>
            <div class="wc-popup-buttons">
                <span class="wc-popup-button" :style="yes.style" @click="success">{{yes.text}}</span>
                <span class="wc-popup-button" :style="no.style" @click="cancel">{{no.text}}</span>
            </div>
        </div>
    </div>
</template>
<script>
    import pageChange from '../../mixins'
    import preventPageScroll from 'wc-utils/prevent-page-scroll'
    export default {
        mixins: [pageChange],
        data () {
            return {
                show: false,
                title: '提示',
                content: '',
                yes: {
                    text: '确定',
                    style: {}
                },
                no: {
                    text: '取消',
                    style: {}
                },
                currentShow: false,
            }
        },
        mounted () {
            preventPageScroll.prevent();
        },
        methods: {
            success () {
                this.show = false;
                preventPageScroll.recover();
            },
            cancel () {
                this.show = false;
                preventPageScroll.recover();
            }
        },
        watch: {
            show (val, oldval) {
                if( val ){
                    setTimeout(()=>{
                        this.currentShow = true;
                    }, 10);
                }
            }
        }
    }
</script>