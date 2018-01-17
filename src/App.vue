<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm_8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1>Built-in Directives</h1>
                <p v-text="'Some Text'"></p>
                <p v-html="'<strong>Strong Text</strong>'"></p>
            </div>
        </div>
        <hr>
        <div class="row">
            <div class="col-xs-12 col-sm_8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1>Custom Directives</h1>
                <!--<p v-highlight="'red'" >Color this</p>-->
                <!--<p v-highlight:background="'red'" >Color this</p>-->
                <!--<p v-highlight:background.delayed="'red'" >Color this</p>-->
                <p v-local-highlight:background="'red'" >Color this</p>
                <p v-highlight:background.delayed="'red'" >Color this</p>
                <p v-local-highlight:background.delayed.blink="{mainColor: 'red', secondColor: 'green', delay: 500}" >Color this</p>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        directives: {
            'local-highlight': {
                bind(el, binding, vnode) {
                    let delay = 0;

                    if (binding.modifiers['delayed']) {
                        delay = 1000;
                    }
                    if (binding.modifiers['blink']) {
                        console.log('dd')
                        let { mainColor, secondColor, delay } = binding.value
                        let currentColor = mainColor;
                        setTimeout(() => {
                            setInterval(() => {
                                currentColor = (currentColor == secondColor) ? mainColor : secondColor;
                                console.log(currentColor)
                                if (binding.arg == 'background') {
                                    el.style.backgroundColor = currentColor
                                } else {
                                    el.style.color = currentColor
                                }}, delay);
                            }, 1000);
                    } else {
                        setTimeout(() => {
                            if (binding.arg == 'background') {
                                el.style.backgroundColor = binding.value
                            } else {
                                el.style.color = binding.value
                            }}, delay
                        );
                    }
                }
            }
        }
    }
</script>

<style>

</style>
