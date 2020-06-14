<template>
    <form class="my-form">
        <slot></slot>
    </form>
</template>
<script>
    export default {
        name: 'MyForm',
        provide() {
            return {
                myForm: this
            }
        },
        props: {
            model: Object,
            rules: Object
        },
        methods: {
            async validate(callback) {
                try {
                    // 这里返回的是promise组成的数组
                    const tasks = this.$children.filter(item => item.prop).map(item => item.handleValidate())
                    const results = await Promise.all(tasks)
                    let ret = true
                    results.forEach(valid => {
                        if (!valid) {
                            ret = false
                        }
                    })
                    callback(ret)
                } catch(err) {
                    console.log(err)
                }

                /* Promise.all(tasks)
                    .then(() => callback(true))
                    .catch(() => callback(false)) */
            }
        }
    }
</script>