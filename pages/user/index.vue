<template>
    <b-container fluid="md" class="mt-5 mb-5">
        <b-row>
            <b-col md="12">
                <b-card class="shadow-md border-0 rounded-lg">
                    <h5>Data Users</h5>
                    <hr>
                    <b-button :to="{name: 'user-create'}" variant="primary" class="mb-3">Create</b-button>
                    <b-table striped bordered hover :items="users" :fields="fields" show-empty>
                        <template v-slot:cell(actions)="row">
                            <b-button :to="{name: 'user-edit-id', params: {id: row.item.id}}" variant="warning" size="sm">Edit</b-button>
                            <b-button variant="danger" size="sm" @click="deleteUser(row)">Delete</b-button>
                        </template>
                    </b-table>
                </b-card>
            </b-col>
        </b-row>
    </b-container>
</template>

<script>
export default {
    data() {
       return {
           fields: [
                'first_name',
                'last_name',
                'phone',
                'address',
                'email',
                'password',
                'actions'
           ],
           users: [],
       } 
    },

    mounted(){
        this.$axios.get('/api/users')
        .then(response =>{
            this.users = response.data.data
        })
        .catch(error => {
            console.log(error.response.data)
        })
    },

    methods: {
        async deleteUser(row){
            await this.$axios.delete('/api/users/${row.item.id}')
            .then(() => {
                this.users.splice(row.index, 1);
            })
        }
    }
}
</script>