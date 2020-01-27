<template>
    <div>
        <ul>
            <Question 
                v-for="(question, i) of questions"
                v-bind:question="question"
                v-bind:number="i"
                v-on:remove-question="removeQuestion"
                v-on:edit-question="editQuestion"
                @select-question="selectQuestion"
            />
        </ul>
    </div>
</template>

<script>
import Question from '@/components/Question'
export default {
    props: ['questions'],
    components: {
        Question
    },
    methods: {
        removeQuestion(id) {
            this.$emit('remove-question', id)
        },
        editQuestion(question) {
            this.$emit('edit-question', question)
        },
        selectQuestion() {
            this.$emit('select-question')
        }
    }
}
</script>

<style scoped>
    ul {
        list-style: none;
        margin: 0;
        padding: 0;
    }
</style>