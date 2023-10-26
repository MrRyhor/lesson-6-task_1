<template>
    <div class="container">
        <label>
            {{ title }}
            <input ref="inp" type="number" v-model="currentAge" :key="updateKey" />
        </label>
        <template v-if="message">
            <div class="message">{{ message }}</div>
            <button type="button" @click="updateInp">Enter Correct Age</button>
        </template>
    </div>
</template>

<script>
export default {
    name: 'UserAge',

    props: {
        title: {
            type: String,
            default: '',
        },
        ageVal: {
            type: Number,
        },
        ageValModifiers: {
            default: () => ({}),
        },
    },

    data() {
        return {
            updateKey: 0,
            message: null,
        }
    },

    computed: {
        currentAge: {
            get() {
                return this.ageVal
            },
            set(val) {
                if (this.ageValModifiers.check) {
                    this.setVal(val)
                }
                this.$emit('update:ageVal', val)
                if (this.ageValModifiers.setColor) {
                    this.setColor(val)
                }
            },
        },
    },
    methods: {
        setColor(val) {
            if (!val) this.$refs.inp.style.backgroundColor = 'transparent'
            else if (val <= 10) this.$refs.inp.style.backgroundColor = 'green'
            else if (val <= 21) this.$refs.inp.style.backgroundColor = 'yellow'
            else this.$refs.inp.style.backgroundColor = 'orange'
        },
        setVal(val) {
            this.message = ''
            if (val > 150) {
                this.$refs.inp.disabled = true
                this.message = 'Age is incorrect should be <= 150'
            }
        },
        updateInp() {
            this.message = ''
            this.$refs.inp.disabled = false
            this.$refs.inp.focus()
            this.$refs.inp.style.backgroundColor = 'transparent'
            this.$nextTick(() => {
                this.$refs.inp.value = null
            })
        },
    },
}
</script>
<style lang="scss" scoped>
.message {
    color: red;
}
div {
    margin-top: 10px;
}
button {
    margin-top: 10px;
}
</style>
