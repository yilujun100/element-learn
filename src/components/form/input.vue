<template>
    <div>
        <input :value="value" @input="handleInput" v-bind="$attrs" >
    </div>
</template>
<script>
export default {
    name: 'MyInput',
    inheritAttrs: false,
    props: {
        value: [String, Number]
    },
    watch: {
        value(val) {
            // 通知formItem进行校验
            this.$parent.$emit('validate')
        }
    },
    methods: {
        handleInput(event) {
            this.$emit('input', event.target.value)
        }
    }
}
</script>