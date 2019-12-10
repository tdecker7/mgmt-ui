<template>
    <div id="home-form">
        <form @submit.prevent="handleSubmit">
            <label>Home Name</label>
            <input 
                ref="first"
                :class="{ 'has-error': submitting && invalidName }"
                v-model="home.name" 
                @focus="clearStatus"
                @keypress="clearStatus"
                type="text" 
            />
            <label>Home Address</label>
            <input 
                :class="{ 'has-error': submitting && invalidAddress }"
                v-model="home.address" 
                type="text" 
                @focus="clearStatus"
            />
            <label>Home Type</label>
            <input 
                :class="{ 'has-error': submitting && invalidType }"
                v-model="home.type" 
                type ="text" 
                @focus="clearStatus"
            />
            <p v-if="error && submitting" class="error-message">
                Please fill out all required fields
            </p>
            <p v-if="success" class="success-message">
                Home added successfully
            </p>
            <button>Add Home</button>
        </form>
    </div>
</template>

<script>
export default {
    name: 'home-form',
    data() {
        return {
            submitting: false,
            error: false,
            success: false,
            home: {
                name: '',
                address: '',
                type: '',
            },
        }
    },
    methods: {
        handleSubmit() {
            this.submitting = true
            this.clearStatus()
            if (this.invalidName || this.invalidAddress || this.invalidType) {
                this.error = true
                return
            }
            this.$emit('add:home', this.home)
            this.$refs.first.focus()
            this.home = { 
                name: '',
                address: '',
                type: '',
            }
            this.error = false
            this.success = false
            this.submitting = false
        },
        clearStatus() {
            this.success = false
            this.error = false
        }
    },
    computed: {
        invalidName() {
            return this.home.name === ''
        },
        invalidAddress() {
            return this.home.address === ''
        },
        invalidType() {
            return this.home.type === ''
        }
    }
}
</script>

<style scoped>
    form {
        margin-bottom: 2rem;
    }

    [class*='-message'] {
        font-weight: 500;
    }

    .error-message {
        color: #d33c40;
    }

    .success-message {
        color: #32a95d;
    }
</style>
