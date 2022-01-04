<template>
  <div class="container">
    <h1>Login</h1>

    <form @submit.prevent="efetuarLogin">
      <div class="form-group">
        <label for="email">E-mail</label>
        <input type="email" name="email" class="form-control" v-model="usuario.email" />
      </div>

      <div class="form-group">
        <label for="senha">Senha</label>
        <input type="password" name="senha" class="form-control" v-model="usuario.senha" />
      </div>

      <div class="alert alert-danger" v-if="mensagemErro">
        {{ mensagemErro }}
      </div>

      <button type="submit" class="btn btn-primary mr-2">Logar</button>

      <router-link :to="{ name: 'novo.usuario' }">Não possui cadastro, cadastre-se aqui.</router-link>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      usuario: {},
      mensagemErro: ''
    }
  },
  methods: {
    efetuarLogin() {
      this.$store.dispatch('efetuarLogin', this.usuario)
      .then(() => {
        this.$router.push({ name: 'gerentes'})
        this.mensagemErro = ''
      })
      .catch(error => {
        if (error.request.status === 401){
          this.mensagemErro = 'Login ou senha inválidos'
        }
      })
    }
  }
}
</script>
