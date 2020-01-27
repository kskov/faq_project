<template>
  <transition name="modal-fade">
    <div class="modal-backdrop">
      <div class="modal"
        role="dialog"
        aria-labelledby="modalTitle"
        aria-describedby="modalDescription"
      >
        

        <section
          class="modal-body"
          id="modalDescription"
        >
          <slot name="body">
            <form>
                <h3>USERNAME & PASSWORD</h3>
                <input type="text" placeholder="E-MAIL">
                <br>
                <input type="text" placeholder="PASSWORD">
                <br>
                <button type="submit" class="btn-login">LOGIN</button>
            </form>
          </slot>
        </section>

        <footer class="modal-footer">
          <slot name="footer">

            <button
              type="button"
              class="btn-green"
              @click="close"
              aria-label="Close modal"
            >
              CLOSE
            </button>
          </slot>
        </footer>
      </div>
    </div>
  </transition>
</template>

<script>
  export default {
    name: 'modal',
    methods: {
      close() {
        this.$emit('close');
      },
    },
  };
</script>

<style scoped>
  .modal-backdrop {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: rgba(0, 0, 0, 0.3);
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .modal {
    background: #FFFFFF;
    box-shadow: 2px 2px 20px 1px;
    overflow-x: auto;
    display: flex;
    flex-direction: column;
  }

  .modal-header,
  .modal-footer {
    padding: 15px;
    display: flex;
  }

  .modal-header {
    border-bottom: 1px solid #eeeeee;
    color: #294157;
    justify-content: space-between;
    font-weight: bold;
  }

  .modal-footer {
    border-top: 1px solid #eeeeee;
    justify-content: flex-end;
  }

  .modal-body {
    position: relative;
    padding: 20px 20px;
  }

  input {
      width: 100%;
      height: 1.5rem;
      margin-bottom: .5rem;
  }

  .btn-login {
    border: none;
    font-size: 20px;
    padding: 20px;
    cursor: pointer;
    font-weight: bold;
    color: #c94343;
    background: transparent;
  }

  .btn-close {
    border: none;
    font-size: 20px;
    padding: 20px;
    cursor: pointer;
    font-weight: bold;
    color: #294157;
    background: transparent;
  }

  .btn-green {
    color: white;
    background: #294157;
  }
</style>