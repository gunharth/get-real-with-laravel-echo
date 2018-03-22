<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card card-default">
                    <div class="card-header">Messages</div>

                    <div class="card-body">
                        <ul>
                            <li v-for="message in messages" v-text="message"></li>
                        </ul>

                        <input type="text" v-model="newMessage" @blur="addMessage">
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                messages: [],
                newMessage: ''
            };
        },

        created() {
            axios.get('/messages').then(response => (this.messages = response.data));
        },

        methods: {
            addMessage() {
                axios.post('/messages', { body: this.newMessage });

                this.messages.push(this.newMessage);

                this.newMessage = '';
            }
        }
    };
</script>
