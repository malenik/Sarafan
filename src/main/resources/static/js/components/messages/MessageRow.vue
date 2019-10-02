<template>
    <v-card class="my-2">
        <v-card-text primary-title>
        <i>({{ message.id }})</i>
            {{ message.text }}
        </v-card-text>
        <media v-if="message.link" :message="message"></media>
        <v-card-actions>
            <v-btn value="Edit" @click="edit" small rounded>Edit</v-btn>
            <v-btn icon @click="del" small rounded>
                <v-icon>{{mdiDelete}}</v-icon>
            </v-btn>
        </v-card-actions>
        <comment-list>
            :comments="message.comments"
            :message-id="message.id"
        </comment-list>
    </v-card>
</template>

<script>
    import { mdiDelete } from '@mdi/js';
    import { mapActions } from 'vuex'
    import Media from 'components/media/Media.vue'
    import CommentList from '../comment/CommentList.vue'
    export default {
        components: {
            mdiDelete,
            CommentList,
            Media
        },
        data() {
            return {
                mdiDelete: mdiDelete

            }
        },
        props: ['message', 'editMessage'],
        methods: {
            ...mapActions(['removeMessageAction']),
            edit() {
                this.editMessage(this.message)
            },
            del() {
                this.removeMessageAction(this.message)
            }
        }
    }
</script>

<style>

</style>