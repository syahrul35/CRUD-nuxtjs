<template>
    <b-container fluid="md" class="mt-5 md-5">
        <b-row>
            <b-col md="12">
                <b-card class="shadow-md border-0 rounded-lg">
                    <h5>Create User</h5>
                    <hr>
                    <b-form @submit="store">
                        <!-- first name -->
                        <b-form-group label="First Name">
                            <b-form-input type="text" v-model="post.first_name" :class="{'is-invalid': validation.first_name}" placeholder="Your First Name">
                            </b-form-input>
                            <div v-if="validation.first_name" class="mt-2">
                                <b-alert show variant="danger">{{ validation.first_name[0] }}</b-alert>
                            </div>
                        </b-form-group>

                        <!-- last name -->
                        <b-form-group label="Last Name">
                            <b-form-input type="text" v-model="post.last_name" :class="{'is-invalid': validation.last_name}" placeholder="Your last Name">
                            </b-form-input>
                            <div v-if="validation.last_name" class="mt-2">
                                <b-alert show variant="danger">{{ validation.last_name[0] }}</b-alert>
                            </div>
                        </b-form-group>

                        <!-- phone -->
                        <b-form-group label="Phone">
                            <b-form-input type="text" v-model="post.phone" :class="{'is-invalid': validation.phone}" placeholder="Your phone">
                            </b-form-input>
                            <div v-if="validation.phone" class="mt-2">
                                <b-alert show variant="danger">{{ validation.phone[0] }}</b-alert>
                            </div>
                        </b-form-group>

                        <!-- address -->
                        <b-form-group label="Address">
                            <b-form-input type="text" v-model="post.address" :class="{'is-invalid': validation.address}" placeholder="Your address">
                            </b-form-input>
                            <div v-if="validation.address" class="mt-2">
                                <b-alert show variant="danger">{{ validation.address[0] }}</b-alert>
                            </div>
                        </b-form-group>

                        <!-- email -->
                        <b-form-group label="Email">
                            <b-form-input type="email" v-model="post.email" :class="{'is-invalid': validation.email}" placeholder="Your email">
                            </b-form-input>
                            <div v-if="validation.email" class="mt-2">
                                <b-alert show variant="danger">{{ validation.email[0] }}</b-alert>
                            </div>
                        </b-form-group>

                        <!-- password -->
                        <b-form-group label="Password">
                            <b-form-input type="password" v-model="post.password" :class="{'is-invalid': validation.password}" placeholder="Your password">
                            </b-form-input>
                            <div v-if="validation.password" class="mt-2">
                                <b-alert show variant="danger">{{ validation.password[0] }}</b-alert>
                            </div>
                        </b-form-group>
                        <b-button type="submit" variant="primary">Save</b-button>
                    </b-form>
                </b-card>
            </b-col>
        </b-row>
    </b-container>
</template>

<script>
export default {
    data() {
        return{
            post: {
                first_name: '',
                last_name: '',
                phone: '',
                address: '',
                email: '',
                password: '',
            },
            validation: []
        }
    },

    methods: {
        async store(e){
            e.preventDefault()

            await this.$axios.post('/api/users', {
                first_name: this.post.first_name,
                last_name: this.post.last_name,
                phone: this.post.phone,
                address: this.post.address,
                email:this.post.email ,
                password: this.post.password,
            })
            .then(() => {
                this.$router.push({
                    name: 'user'
                })
            })
            .catch(error =>{
                this.validation = error.response.data
            })
        }
    }
}
</script>