<template>
    <li>
        <div class="question">
            <span>
                <input type="checkbox" class="inputCheck" v-on:change="question.selected = !question.selected; $emit('select-question')">
                <strong>{{ number + 1 }}</strong>
                {{ question.question }}
                </span>
            <div class="buttons">
                <button class="open" v-on:click="question.hide = !question.hide">OPEN</button>
                <button class="edit" v-on:click="question.hide_edit = !question.hide_edit">EDIT</button>
                <button class="rmv" v-on:click="$emit('remove-question', question.id)">DELETE</button>
            </div>
        </div>
        <div class="answer">
            <p v-bind:class="{hide: question.hide}">
                {{ question.answer }}
            </p>
        </div>
        <div v-bind:class="{hide: question.hide_edit}">
            <form @submit.prevent="updateQuestion">
                <h3>EDIT THE QUESTION</h3>
                <input type="text" v-model="question.question">
                <br>
                <textarea rows="10" v-model="question.answer"></textarea>
                <br>
                <button type="submit" v-on:click="question.hide_edit = !question.hide_edit">SAVE the QUESTION</button>
            </form>
        </div>
    </li>
</template>

<script>
    export default {
        props: {
            question: {
                type: Object,
                required: true
            },
            number: Number
        },
        methods: {
            updateQuestion() {
                this.$emit('edit-question', this.question)
            }
        }
    }
</script>

<style scoped>

    /* MAIN SECTION */

    .question {
        display: flex;
        justify-content: space-between;
        padding: .5rem 2rem;
        margin-bottom: .5rem;
        font-weight: bold;
    }

    .answer {
        text-align: justify;
        color: lightslategrey;
    }

    /* BUTTONS */

    .open {
        background-color: rgb(45, 163, 104);
        font-weight: bold;
        color: white;
        margin-right: .2rem;
    }

    .edit {
        background-color: rgb(15, 119, 189);
        color: white;
        margin-right: .2rem;
    }

    .rmv {
        background-color: rgb(194, 61, 61);
        font-weight: bold;
        color: white;
    }

    /* TAGS */

    input {
        margin-right: 1rem;
    }

    form {
        padding-top: 1rem;
        padding-bottom: 5rem;
    }

    input[type=text] {
        width: 100%;
        margin-bottom: .5rem;
    }

    textarea {
        width: 100%;
    }

    /* VISIBILITY */

    .hide {
        display: none;
    }

    .hide_edit {
        display: none;
    }

</style>