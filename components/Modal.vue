<template>
  <div>
    <button class="сomeIn" @click="showModal = true" :style="сomeInStyle" :disabled="!eventStatus">Участвовать</button>
        <transition name="modal">
            <div v-if="showModal" class="modal-mask">
                <div class="modal-wrapper">
                    <div class="modal-container">
                        <button class="toCloseBtn" @click="showModal = false"></button>
                        <form method="post" @submit.prevent="testSubmit(eventId, Participant)">

                            <label for="sername">Фамилия</label>
                            <input id="sername" type="text" v-model="Participant.last_name">

                            <label for="name">Имя</label>
                            <input id="name" type="text" v-model="Participant.first_name">

                            <label for="patronym">Отчество</label>
                            <input id="patronym" type="text" v-model="Participant.patronymic">

                            <label for="email">e-mail</label>
                            <input id="email" type="email" v-model="Participant.email">

                            <label for="tel">Телефон</label>
                            <input id="tel" type="tel" v-model="Participant.phone">

                            <label class="check_label">
                                    <input class="checkbox" type="checkbox" name="checkbox-test">
                                    <span class="label">Я согласен (согласна) на обработку моих персональных данных </span>
                            </label>

                            <input class="signInBtn" type="submit" value="Присоединиться"  @click="showModal = false">
                        </form>
                    </div>
                </div>
            </div>
    </transition>
  </div>
</template>

<script>
import {mapMutations, mapActions} from 'vuex'

export default {
  data() {
    return {
      showModal: false,
      Participant: {
        last_name: '',
        first_name: '',
        patronymic: '',
        email: '',
        phone: ''
      }
    }
  },
  props: {
        eventId: Number,
        eventStatus: Boolean
    },
  computed: {
    сomeInStyle() { 
            return {
                background: this.eventStatus ? "#5EB8D3" : "#C4C4C4"
            }
        },
  },
  methods: {
    ...mapActions({
      submitParticipant : 'submitParticipant',
    }),
    testSubmit(eventId, participant) {
      this.submitParticipant({ eventId, participant });
    }
  },
}
</script>

<style scoped>

.сomeIn {
  font-size: 1.7rem;
    padding: 1rem 1.7rem;
    height: 3.7rem;
        width: 100%;
        border: none;
        border-radius: 30px;
        font-family: 'Rubik', sans-serif;
        outline: none;
        color: white;
        font-weight: 500;
        cursor: pointer;
    }

button {
  cursor: pointer;  
}

.checkbox {
  cursor: pointer;
}

.modal-mask {
  color: #312E2E;
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, .5);
  display: table;
  transition: opacity .3s ease;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  display: flex;
  flex-direction: column;
  width: 30vw;
  margin: 0px auto;
  padding: 2vw;
  background-color: #fff;
  box-shadow: 0px 4px 12px rgba(0, 0, 0, 0.15);
  border-radius: 25px;
  font-weight: 500;
  position: relative;
}

.toCloseBtn {
  width: 1.5rem;
  height: 1.5rem;
  align-self: flex-end;
  border: none;
  background: url(../assets/reg_exit.png) 50% 50% no-repeat;
  background-size: contain;
  outline: none;
}

form {
    display: flex;
    flex-direction: column;
}

label {
    text-align: left;
    font-size: 1.1rem;
}

input[type=text],
input[type=email],
input[type=tel] {
    font-family: 'Rubik', sans-serif;
    border: 1px solid #C4C4C4;
    margin: 0.4rem 0 1rem;
    padding: 0.4rem;
    font-size: 1.1rem;
    border-radius: 8px;
    outline: none;
}

.check_label {
    display: flex;
    align-items: center;
}

.label {
    margin-left: 0.5rem;
    font-size: 0.8rem;
    line-height: 0.9rem;
    color: #312E2E;
}

.signInBtn {
  margin-top: 1rem;
  display: flex;
  justify-content: center;
  align-items: center;
  font-weight: bold;
  font-size: 1.5rem;
  background: #71D5A2;
  padding: 1rem 2rem;
  border: none;
  border-radius: 100px;
  text-decoration: none;
  color: white;
  outline: none;
  cursor: pointer;
}

.toClose {
    width: 1.5rem;
    height: 1.5rem;
    cursor: pointer;
    position: absolute;
    margin: 1rem;
    top: 0;
    right: 0;
}

@media (max-width: 576px) {
  label {
    font-size: 2rem;
  }

  input[type=text],
  input[type=email],
  input[type=tel] {
    margin: 1rem 0 1.5rem;
    padding: 0.7rem;
    font-size: 2rem;
    outline: none;
  }

  .label {
    margin-left: 0.5rem;
    font-size: 1rem;
    line-height: 0.9rem;
  }

  .signInBtn {
    margin-top: 2rem;
    font-size: 2rem;
    padding: 1.5rem 2.5rem;
  }

  .toClose {
    width: 1.5rem;
    height: 1.5rem;
    margin: 1rem;
  }
  .toCloseBtn {
    width: 2rem;
    height: 2rem;
  }
}

@media (min-width: 1450px) {
   .сomeIn {
    font-size: 1.7rem;
    padding: 1rem 1.7rem;
    height: 3.7rem;
  }
}

@media (max-width: 580px) {
   .сomeIn {
    font-size: 1.75rem;
    padding: 1.1rem 1.7rem;
    height: 3.95rem;
  }
}

@media (max-width: 480px) {
  .modal-container {
  width: 60vw;
   padding: 4vw;
  }
   .сomeIn {
    font-size: 1.75rem;
    padding: 0.90rem 1.7rem;
    height: 3.55rem;
  }
}

@media (max-width: 420px) {
   .сomeIn {
    font-size: 1.7rem;
    padding: 1rem 1.7rem;
    height: 3.7rem;
  }
}

.modal-enter {
  opacity: 0;
}

.modal-leave-active {
  opacity: 0;
}

.modal-enter .modal-container,
.modal-leave-active .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
</style>
