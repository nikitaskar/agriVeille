<template>
    <div class="gauge">
        <div class="gauge__indicator">
            <div class="gauge__indicator__value">&nbsp;</div>
        </div>
        <div class="gauge__illu">
            <div class="gauge__illu__wrapper">
                <img :src="image" alt="Loader example">
            </div>
        </div>
        <p class="gauge__tuto heading--7">Scroll to digitalize&nbsp;!</p>
    </div>
</template>

<script>

    import getHead from '@/assets/js/utils/gaugeImage.js';
    /* Import Action STORE*/
    import { mapActions, mapGetters } from 'vuex';

    export default  {
        data () {
            return {
                image: getHead(1)
            }
        },
        computed: {
            ...mapGetters([
                'getDigitalValue',
                'getPercentValue'
            ])
        },
        methods: {
            setHead(id) {
                this.image = getHead(id);
            },
            setGaugeValue(value) {
                const el = this.$el.querySelector('.gauge__indicator__value');
                el.style.transform = `translateY(${100 - (value * 100)}%)`;
            }
        },
        mounted() {
            if (this.getDigitalValue) {
                this.setHead(this.getDigitalValue);
            }

            if (this.getPercentValue) {
                this.setGaugeValue(this.getPercentValue);
            }
        },
        watch: {
            getDigitalValue(val) {
                this.setHead(val);
            },
            getPercentValue(val) {
                this.setGaugeValue(val);
            }
        }
    }
</script>


<style lang="scss">
     @import "~styles/main.scss";

    .gauge{
        position: fixed;
        right: 10rem;
        top: 50%;
        height: 48rem;
        width: 3.4rem;
        transform: translateY(-50%);
        border: 2px solid $black;
        border-radius: 2.6rem;
        background-color: $dark-grey;

        &__tuto {
            position: absolute;
            width: 10rem;
            bottom: -8rem;
            left: 50%;
            text-align: center;
            transform: translateX(-50%);
            //animation: blink 2s $easeInOutCubic infinite;
        }

        &__indicator {
            position: absolute;
            top: 1rem;
            left: 50%;
            width: 1.5rem;
            height: 34.4rem;
            border: 2px solid $black;
            border-radius: 1.5rem;
            background-color: #fdf0d1;
            transform: translateX(-50%);
            overflow: hidden;

            &__value {
                position: absolute;
                top: 0;
                left: 0;
                width: 100%;
                height: 100%;
                border-radius: 1.5rem;
                background-color: $orange;
                transform: translateY(100%);
                transition: transform .8s $easeCustom;
            }
        }

        &__illu {
            position: absolute;
            bottom: -2px;
            left: 50%;
            width: 13.5rem;
            height: 13.5rem;
            border: 2px solid $black;
            border-radius: 50%;
            background-color: $dark-grey;
            transform: translateX(-50%);

            &__wrapper {
                position: absolute;
                top: 50%;
                left: 50%;
                width: calc(100% - 1rem);
                height: calc(100% - 1rem);
                border-radius: 50%;
                border: 2px solid $black;
                background-color: $main-color;
                transform: translate(-50%, -50%);

                img {
                    position: absolute;
                    bottom: 1rem;
                    width: 15rem;
                    left: 50%;
                    max-width: 15rem;
                    transform: translateX(-50%);
                }
            }
        }
    }


     @keyframes blink {
        0% {
            opacity: 1
        }
        50% {
            opacity: 0
        }
        100% {
            opacity: 1
        }
    }

</style>
