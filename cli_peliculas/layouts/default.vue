<template>
  <div>
    <nav
      class="navbar header has-shadow is-primary"
      role="navigation"
      aria-label="main navigation"
    >
      <div class="navbar-brand">

        <a class="navbar-item" href="/">Super Películas</a>

        <div class="navbar-burger" @click="isActive = !isActive">
          <span />
          <span />
          <span />
        </div>
      </div>
      <!-- Contenido del menú, al nivel del navbar-brand-->
      <div class="navbar-menu" :class="{ active: isActive }">
        <div class="navbar-end">
          <div class="navbar-item">
            <div class="buttons">
<a class="button" v-if="!user">
  <strong>Registro</strong>
</a>
<a class="button is-primary" v-else>
  Bienvenido {{user}} 😄
</a>
<a class="button is-light" @click="isLoginActive=true" v-if="!user">
  Acceder
</a>
<a class="button is-light" @click="logout" v-else>
  Salir
</a>
              <!-- Modal para el login -->
                <b-modal :active.sync="isLoginActive">
                  <form action="" v-on:submit.prevent="login">
                    <div class="modal-card" style="width: auto">
                      <header class="modal-card-head">
                        <p class="modal-card-title">Identificación</p>
                      </header>
                      <section class="modal-card-body">
                        <b-field label="Email">
                          <b-input
                            type="email"
                            v-model="loginEmail"
                            placeholder="Tu email"
                            required>
                          </b-input>
                        </b-field>
                        <b-field label="Contraseña">
                          <b-input
                            type="password" 
                            v-model="loginPassword"
                            password-reveal
                            placeholder="Tu contraseña"
                            required>
                          </b-input>
                        </b-field>
                    </section>
                    <footer class="modal-card-foot">
                      <button class="button is-primary">Acceder</button>
                    </footer>
                    </div>
                  </form>
                </b-modal>
            </div>
          </div>
        </div>
      </div>
    </nav>

    <section class="main-content columns">
<aside class="column is-2 section"> <!-- 3 en lugar de 2 y 9 por 10 -->
  <p class="menu-label is-hidden-touch">General</p>
  <ul class="menu-list">
    <li>
      <nuxt-link to="/" exact-active-class="is-active">
        <b-icon icon="video"/>
        Películas
      </nuxt-link>
    </li>
    <li>
      <nuxt-link to="/favoritas" exact-active-class="is-active">
        <b-icon icon="star"/>
        Favoritas
      </nuxt-link>
    </li>
  </ul>
</aside>

      <div class="container column is-9">
        <nuxt />
      </div>
    </section>
  </div>
</template>

<script>
export default {
  data () {
    return {
      isActive: false,
      isLoginActive: false,

      loginEmail: 'test@test.com',
      loginPassword: 'TEST1234A',
    };
  },
  computed: {
  user: function () {
    return this.$store.state.user;
  }
},
  methods: {
    login() {
      return this.$axios.post('/auth/login/', {
        email: this.loginEmail,
        password: this.loginPassword
      })
      .then((res) => {
        if (res.data.key){
          this.$store.commit('saveToken', res.data.key)
          this.$store.commit('saveUser', this.loginEmail.split("@")[0])
          // Reiniciamos los campos
          this.loginEmail = ''
          this.loginPassword = ''
          // Escondemos la modal
          this.isLoginActive = false;
        }
      })
      .catch((error) => {
        alert(Object.values(error.response.data))
      })
    },
    logout() {
  this.$store.commit('saveToken', null)
  this.$store.commit('saveUser', null)
}
 }
};
</script>
<style>
.active{
  display: block !important;
}
</style>