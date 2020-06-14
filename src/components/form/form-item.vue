<template>
    <div>
        <label>{{ label }}</label>
        <slot></slot>
        <p v-if="validateState === 'error'">{{ validateMessage }}</p>
    </div>
</template>
<script>
import Schema from 'async-validator'
export default {
    name: 'MyFormItem',
    inject: ['myForm'],
    props: {
        label: String,
        prop: String
    },
    data() {
        return {
            validateState: '',
            validateMessage: ''
        }
    },
    mounted() {
        this.$on('validate', this.handleValidate)
    },
    methods: {
        handleValidate() {
            // 这里使用async-validator进行校验
            return new Promise((resolve, reject) => {
                const value = this.myForm.model[this.prop]
                const rules = this.myForm.rules[this.prop]
                const descriptor = {};
                descriptor[this.prop] = rules
                // 校验器
                const validator = new Schema(descriptor)
                validator.validate({[this.prop]: value}, errors => {
                    if (errors) {
                        this.validateState = 'error'
                        this.validateMessage = errors[0].message
                        reject(false)
                    } else {
                        this.validateState = ''
                        this.validateMessage = ''
                        resolve(true)
                    }
                })
            })
        }
    }
}
</script>