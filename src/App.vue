<template>
  <div class="wrapper">

    <div class="wrapper-content">
      <section>
        <div class="container">
            <!-- First modal -->
            <button class="btn btnPrimary" @click="modalFirst = !modalFirst">Show first modal</button>
          <modals
          title="First modal"
          v-show="modalFirst"
          @close="modalFirst = false">

            <div slot="body">
              <p>text text text text text text</p>
              <button class="btn btnPrimary" @click="modalFirst = !modalFirst"> Well Done </button>
            </div>
          </modals>
          <!-- Second modal -->
          <button class="btn btnPrimary" @click="modalSecond.show = !modalSecond.show">Show modal with form</button>
          <modals
          title="Modal with form"
          v-show="modalSecond.show"
          @close="closeSecondModal">

            <div slot="body">
              <form @submit.prevent="submitSecondForm">
                <label>Name:</label>
                <input type="text"  v-model="modalSecond.name">
                <label>Email::</label>
                <input type="text"  v-model="modalSecond.email">
                <button class="btn btnPrimary"> Submit </button>

              </form>
              </div>
          </modals>
          <!-- Modal with validate -->
          <button class="btn btnPrimary" @click="modalValidate = !modalValidate">Show modal with form + validate</button>
          <modalValidate v-show="modalValidate" @close="modalValidate = false" />
          <!-- Login -->
          <button class="btn btnPrimary" @click="loginModal = !loginModal">Login</button>
          <loginModal v-show="loginModal" @close="closeLoginModal" @openRegistration = 'openRegistration' />
          <!-- Registration -->
          <button class="btn btnPrimary" @click="RegistrationModal = !RegistrationModal">Registration</button>
          <RegistrationModal v-show="RegistrationModal" @close="closeRegistrationModal" />
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import modals from '@/components/UI/Modal.vue'
import modalValidate from '@/components/ModalValidate.vue'
import loginModal from '@/components/Login.vue'
import RegistrationModal from '@/components/Registration.vue'



export default {
  components: { modals,modalValidate,loginModal,RegistrationModal },
  data () {
    return {
      modalFirst: false,
      modalSecond: {
        show:false,
        name: "",
        email:'',
      },
      modalValidate: false,
      RegistrationModal: false,
      loginModal: false,
    }
  },
  methods: {
    submitSecondForm () {
      console.log({
        name: this.modalSecond.name,
        email: this.modalSecond.email
      });
      this.modalSecond.name = ''
      this.modalSecond.email = ""
      this.modalSecond.show = false
    },
    closeSecondModal () {
      this.modalSecond.name = ''
      this.modalSecond.email = ""
      this.modalSecond.show = false
    },
    closeRegistrationModal () {      
      this.RegistrationModal = false
    },
    closeLoginModal () {
      this.loginModal = false
    },
    openRegistration () {
      this.RegistrationModal = true

    }
  }
};
</script>

<style lang="scss" scope>
  .container {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    column-gap: 4rem;
    row-gap: 1.5rem;
  }
</style>></style>
