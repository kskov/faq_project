<template>
  <div id="app">

    <div class="top">

      <button
        type="button"
        class="modal_btn"
        @click="showModal"
      >
        LOGIN
      </button>
      <div class="switch-theme-field">
          <input type="radio" id="radio-two" name="switch-one" value="day" checked />
          <label for="radio-two">Light</label>
          <input type="radio" id="radio-one" name="switch-one" value="night" />
          <label for="radio-one">Dark</label>
      </div>
    </div>
    

    <div class="main">
      <h1>FAQs</h1>

      <br>
      <button class="open_all" v-show="visible" v-on:click="openSelected">OPEN SELECTED</button>
      <button class="open_all" v-show="!hide" v-on:click="closeSelected">CLOSE ALL</button>


      <QuestionsList 
        v-bind:questions="questions"
        @remove-question="removeQuestion"
        @edit-question="editQuestion"
        @select-question="selectQuestion"
      />

      <AddQuestion 
        @add-question="addQuestion"
      />
      
      <UserLogin
        v-show="isModalVisible"
        @close="closeModal"
      />
    </div>
  </div>
</template>

<script>
import QuestionsList from '@/components/QuestionsList'
import AddQuestion from '@/components/AddQuestion'
import UserLogin from '@/components/UserLogin'
export default {
  name: 'app',
  data() {
    return {
      questions: [
        {id: 1, question: 'How much is the fish?', answer: 'Lorem ipsum dolor sit amet, salutatus hendrerit eu vim, summo recusabo corrumpit per cu, eu nibh case est. Ne debet elaboraret nam, ex sed magna harum, no has utamur omittantur. Ut sit labore fastidii eligendi, ea eum recteque consequuntur. Erant doming sea ea, in eum case quodsi torquatos.', hide: true, hide_edit: true, selected: false},
        {id: 2, question: 'How much is the crab?', answer: 'Lorem ipsum dolor sit amet, salutatus hendrerit eu vim, summo recusabo corrumpit per cu, eu nibh case est. Ne debet elaboraret nam, ex sed magna harum, no has utamur omittantur. Ut sit labore fastidii eligendi, ea eum recteque consequuntur. Erant doming sea ea, in eum case quodsi torquatos.', hide: true, hide_edit: true, selected: false},
        {id: 3, question: 'How much is the shark?', answer: 'Lorem ipsum dolor sit amet, salutatus hendrerit eu vim, summo recusabo corrumpit per cu, eu nibh case est. Ne debet elaboraret nam, ex sed magna harum, no has utamur omittantur. Ut sit labore fastidii eligendi, ea eum recteque consequuntur. Erant doming sea ea, in eum case quodsi torquatos.', hide: true, hide_edit: true, selected: false},
        {id: 4, question: 'How much is the octopus?', answer: 'Lorem ipsum dolor sit amet, salutatus hendrerit eu vim, summo recusabo corrumpit per cu, eu nibh case est. Ne debet elaboraret nam, ex sed magna harum, no has utamur omittantur. Ut sit labore fastidii eligendi, ea eum recteque consequuntur. Erant doming sea ea, in eum case quodsi torquatos.', hide: true, hide_edit: true, selected: false},
        {id: 5, question: 'How much is the cat?', answer: 'Lorem ipsum dolor sit amet, salutatus hendrerit eu vim, summo recusabo corrumpit per cu, eu nibh case est. Ne debet elaboraret nam, ex sed magna harum, no has utamur omittantur. Ut sit labore fastidii eligendi, ea eum recteque consequuntur. Erant doming sea ea, in eum case quodsi torquatos.', hide: true, hide_edit: true, selected: false}
      ],
      visible: false,
      hide: true,
      beginningState: '',
      selectedQuestions: '',
      isModalVisible: false
    }
  },
  methods: {
    removeQuestion(id) {
      this.questions = this.questions.filter(t => t.id !== id)
    },
    addQuestion(question) {
      this.questions.push(question)
    },
    editQuestion(question) {
      this.question = this.questions[question.id]
    },
    selectQuestion() {
      let selQuestions = this.questions.filter(t => t.selected === true)
      if (selQuestions.length > 0) {
        this.visible = true
      } else {
        this.visible = false    // ЭТО НАДО СОКРАТИТЬ
      }
      let selectedIds = []
      for (let quest of selQuestions) {
        selectedIds.push(quest)
      }
      this.selectedQuestions = selectedIds
    },
    openSelected() {
      this.beginningState = this.questions
      this.questions = this.selectedQuestions
      for (let selquestions of this.questions) {
        selquestions.hide = false
      }
      var w = document.getElementsByTagName('input'); 
      for(var i = 0; i < w.length; i++){ 
        if(w[i].type=='checkbox'){ 
          w[i].checked = true; 
        }
      }
      this.hide = false
      this.visible = false
    },
    closeSelected() {  
      this.questions = this.beginningState
      for (let selquestions of this.questions) {
        selquestions.hide = true
        selquestions.selected = false
      }
      var w = document.getElementsByTagName('input'); 
      for(var i = 0; i < w.length; i++){ 
        if(w[i].type=='checkbox'){ 
          w[i].checked = false; 
        }
      }
      this.hide = true
    },
    showModal() {
        this.isModalVisible = true;
      },
    closeModal() {
        this.isModalVisible = false;
    }
  },
  components: {
    QuestionsList, AddQuestion, UserLogin
  }
}
</script>
