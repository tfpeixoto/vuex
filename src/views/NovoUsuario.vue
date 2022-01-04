<template>
  <div class="container">
    <h1>Novo usuário</h1>

    <form @submit.prevent="enviarFormulario">
      <div class="form-group">
        <label for="name">Nome</label>
        <input name="nome" type="text" class="form-control" v-model="usuario.nome" />
      </div>

      <div class="form-group">
        <label for="email">E-mail</label>
        <input name="email" type="text" class="form-control" v-model="usuario.email" />
      </div>

      <div class="form-group">
        <label for="name">Senha</label>
        <input name="senha" type="password" class="form-control" v-model="usuario.senha" />
      </div>

      <button type="submit" class="btn btn-primary">Salvar</button>
    </form>
  </div>
</template>

<script>
export default{
  data: function() {
    return {
      usuario: {
        nome: '',
        email: '',
        senha: ''
      }
    }
  },
  methods: {
    enviarFormulario() {
      this.$http.post('auth/register', this.usuario)
      .then(response => {
        console.log(response)
        this.$router.push({ name: 'login' })
      })
      .catch(error => console.log(error))
    }
  }
}
</script>