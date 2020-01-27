<template>
    <div>   
        <button class="plus_button" v-on:click="visible = !visible">&#43;</button>
        <form id="form" @submit.prevent="addNewQuestion" v-show="visible">
            <h2>ADD A QUESTION</h2>
            <input type="text" placeholder="Question" v-model="question">
            <br>
            <textarea rows="10" placeholder="Answer" v-model="answer"></textarea>
            <br>
            <button type="submit" class="add_button" v-on:click="hide = !hide">ADD a QUESTION</button>
        </form>
    </div>
</template>

<script>
export default {
    data() {
        return {
            question: '',
            answer: '',
            visible: false
        }
    },
    methods: {
        addNewQuestion() {
            if (this.question.trim()&&this.answer.trim()) {
                const newQuestion = {
                    id: Date.now(),
                    question: this.question,
                    answer: this.answer,
                    hide: true,
                    hide_edit: true
                }

                this.$emit('add-question', newQuestion)
                this.question = '',
                this.answer = ''
            }
        }
    }
}
</script>

<style scoped>

/* TAGS */

form {
    padding-top: .5rem;
}

input[type=text] {
    width: 100%;
    margin-bottom: .5rem;
}
textarea {
    width: 100%;
}

/* BUTTONS */

.add_button {
    display: flex;
    background-color: rgb(10, 151, 104);
    margin-right: auto;
}

.plus_button {

    display: flex;
    background-color: rgb(209, 86, 14);
    color: white;
    font-size: 1rem;
    padding: .25rem .5rem;
    margin-left: auto;
}

</style>