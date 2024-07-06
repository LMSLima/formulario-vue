<script setup>
import { ref } from 'vue'

const Forms = ref({
  nome: '',
  email: '',
  senha: '',
  confirmarSenha: '',
  dataNascimento: '',
  endereco: '',
  cidade: '',
  estado: '',
  hobbies: '',
  linguagemProg: '',
  biografia: '',
  avatar: ''
})

const mostrarPerfil = ref(false)

const states = [
  { uf: 'AC', name: 'Acre' },
  { uf: 'AL', name: 'Alagoas' },
  { uf: 'AP', name: 'Amapá' },
  { uf: 'AM', name: 'Amazonas' },
  { uf: 'BA', name: 'Bahia' },
  { uf: 'CE', name: 'Ceará' },
  { uf: 'DF', name: 'Distrito Federal' },
  { uf: 'ES', name: 'Espírito Santo' },
  { uf: 'GO', name: 'Goiás' },
  { uf: 'MA', name: 'Maranhão' },
  { uf: 'MT', name: 'Mato Grosso' },
  { uf: 'MS', name: 'Mato Grosso do Sul' },
  { uf: 'MG', name: 'Minas Gerais' },
  { uf: 'PA', name: 'Pará' },
  { uf: 'PB', name: 'Paraíba' },
  { uf: 'PR', name: 'Paraná' },
  { uf: 'PE', name: 'Pernambuco' },
  { uf: 'PI', name: 'Piauí' },
  { uf: 'RJ', name: 'Rio de Janeiro' },
  { uf: 'RN', name: 'Rio Grande do Norte' },
  { uf: 'RS', name: 'Rio Grande do Sul' },
  { uf: 'RO', name: 'Rondônia' },
  { uf: 'RR', name: 'Roraima' },
  { uf: 'SC', name: 'Santa Catarina' },
  { uf: 'SP', name: 'São Paulo' },
  { uf: 'SE', name: 'Sergipe' },
  { uf: 'TO', name: 'Tocantins' }
]

function handleAvatarChange(event) {
  const file = event.target.files[0]
  if (file) {
    Forms.value.avatar = URL.createObjectURL(file)
  }
}

function validarForms() {
  if (
    !Forms.value.nome ||
    !Forms.value.email ||
    !Forms.value.senha ||
    !Forms.value.confirmarSenha ||
    !Forms.value.dataNascimento ||
    !Forms.value.hobbies ||
    !Forms.value.linguagemProg ||
    !Forms.value.biografia ||
    !Forms.value.estado ||
    !Forms.value.cidade
  ) {
    alert('Por favor, preencha todos os campos obrigatórios.')
    return
  }

  if (Forms.value.senha !== Forms.value.confirmarSenha) {
    alert('As senhas não correspondem. Por favor, verifique.')
    return
  }

  mostrarPerfil.value = true
}
</script>

<template>
  <div class="container">
    <h1>Editor de Perfil</h1>
    <transition name="form" mode="out-in">
      <div :key="mostrarPerfil">
        <fieldset v-if="mostrarPerfil" class="fieldset">
          <legend>Perfil</legend>
          <div class="form-group">
            <img v-if="Forms.avatar" class="avatar" :src="Forms.avatar" />
            <p><strong>Nome:</strong> {{ Forms.nome }}</p>
            <p><strong>Email:</strong> {{ Forms.email }}</p>
            <p><strong>Data de Nascimento:</strong> {{ Forms.dataNascimento }}</p>
            <p><strong>Hobbies:</strong> {{ Forms.hobbies }}</p>
            <p><strong>Linguagens de Programação Preferida:</strong> {{ Forms.linguagemProg }}</p>
            <p><strong>Biografia:</strong> {{ Forms.biografia }}</p>
            <p><strong>Estado:</strong> {{ Forms.estado }}</p>
            <p><strong>Cidade:</strong> {{ Forms.cidade }}</p>
          </div>
          <div class="box-btn">
            <button @click="mostrarPerfil = false" class="button">Esconder</button>
          </div>
        </fieldset>

        <form @submit.prevent="validarForms" class="form">
          <fieldset v-if="!mostrarPerfil" class="fieldset">
            <legend>Dados pessoais</legend>
            <div class="form-group">
              <label for="nome">Nome:</label>
              <input
                type="text"
                id="nome"
                v-model="Forms.nome"
                placeholder="Digite seu nome"
                required
              />
            </div>

            <div class="form-group">
              <label for="email">Email:</label>
              <input
                type="email"
                id="email"
                v-model="Forms.email"
                placeholder="Digite seu email"
                required
              />
            </div>

            <div class="form-group">
              <label for="password">Senha:</label>
              <input
                type="password"
                id="password"
                v-model="Forms.senha"
                placeholder="Digite sua senha"
                required
              />
            </div>

            <div class="form-group">
              <label for="confirmarSenha">Confirmar Senha:</label>
              <input
                type="password"
                id="confirmarSenha"
                v-model="Forms.confirmarSenha"
                placeholder="Confirme sua senha"
                required
              />
            </div>

            <div class="form-group">
              <label for="dataNascimento">Data de Nascimento:</label>
              <input type="date" id="dataNascimento" v-model="Forms.dataNascimento" required />
            </div>

            <div class="form-group">
              <label for="hobbies">Hobbies:</label>
              <input
                type="text"
                id="hobbies"
                v-model="Forms.hobbies"
                placeholder="Hobbies"
                required
              />
            </div>

            <div class="form-group">
              <label>Linguagens de Programação Preferida:</label>
              <div class="radio-group">
                <input type="radio" id="langC" v-model="Forms.linguagemProg" value="C" />
                <label for="langC">C</label>

                <input type="radio" id="langJava" v-model="Forms.linguagemProg" value="Java" />
                <label for="langJava">Java</label>

                <input type="radio" id="langPython" v-model="Forms.linguagemProg" value="Python" />
                <label for="langPython">Python</label>

                <input type="radio" id="langJs" v-model="Forms.linguagemProg" value="JavaScript" />
                <label for="langJs">JavaScript</label>
              </div>
            </div>

            <div class="form-group">
              <label for="avatar">Avatar:</label>
              <input
                type="file"
                id="avatar"
                @change="handleAvatarChange"
                accept="image/*"
              />
            </div>

            <div class="form-group">
              <label for="biografia">Biografia:</label>
              <textarea
                name="biografia"
                id="biografia"
                v-model="Forms.biografia"
                placeholder="Conte um pouco sobre você"
                required
              ></textarea>
            </div>
          </fieldset>

          <fieldset v-if="!mostrarPerfil" class="fieldset">
            <legend>Endereço</legend>
            <div class="form-group">
              <label for="estado">Estado:</label>
              <select id="estado" v-model="Forms.estado" required>
                <option disabled value="">Selecione um estado</option>
                <option v-for="state in states" :key="state.uf" :value="state.uf">
                  {{ state.name }}
                </option>
              </select>
            </div>

            <div class="form-group">
              <label for="cidade">Cidade:</label>
              <input
                type="text"
                id="cidade"
                v-model="Forms.cidade"
                :disabled="!Forms.estado"
                placeholder="Escolha um estado primeiro"
                required
              />
            </div>

            <div class="box-btn">
              <button type="submit">Enviar</button>
            </div>
          </fieldset>
        </form>
      </div>
    </transition>
  </div>
</template>

<style scoped>
.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

h1 {
  text-align: center;
}

.form {
  background-color: #fff;
  padding: 20px;
  border-radius: 5px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.form legend {
  font-size: 1.5rem;
  font-weight: bold;
  margin-bottom: 10px;
}

.form label {
  display: block;
  margin-bottom: 8px;
  font-weight: bold;
  font-size: 1rem;
}

.form .form-group {
  margin-bottom: 20px;
}

.form input[type='text'],
.form input[type='email'],
.form input[type='password'],
.form textarea,
.form select,
.form button,
.form input[type='file'] {
  width: 95%;
  padding: 10px;
  font-size: 1rem;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.form textarea {
  resize: vertical;
}

.form .radio-group {
  display: flex;
  gap: 10px;
  align-items: center;
  margin-bottom: 15px;
}

.form .radio-group input[type='radio'] {
  margin-right: 5px;
}

.box-btn {
  display: flex;
  align-items: center;
  justify-content: center;
}

.form button[type='submit'] {
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 1.3rem;
  padding: 12px 20px;
  transition: background-color 0.3s ease;
}

.form button:hover {
  background-color: #45a049;
}

.fieldset {
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 20px;
  margin-bottom: 20px;
}

.form-enter-active,
.form-leave-active {
  transition: opacity 0.5s ease;
}

.form-enter-from,
.form-leave-to {
  opacity: 0;
}

.button {
  cursor: pointer;
  transition: background-color 0.3s ease, color 0.3s ease, transform 0.3s ease;
  background-color: #1d666b; 
  color: white; 
  border: none;
  border-radius: 5px;
  padding: 10px 20px;
  font-size: 1rem;
  margin-top: 10px;
}

.button:hover {
  background-color: #1d666b; 
}

.button:focus {
  outline: none; 
}

.button:active {
  transform: scale(0.95); 
}

.avatar {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  object-fit: cover;
  margin-bottom: 10px;
}

@media (max-width: 768px) {
  .form label {
    font-size: 0.9rem;
  }

  .form button {
    font-size: 0.9rem;
  }
}

@media (max-width: 480px) {
  .container {
    padding: 10px;
  }

  .form {
    padding: 15px;
  }

  .form legend {
    font-size: 1.3rem;
  }

  .form input[type='text'],
  .form input[type='email'],
  .form input[type='password'],
  .form textarea,
  .form select,
  .form button,
  .form input[type='file'] {
    font-size: 0.9rem;
    padding: 8px;
  }

  .form button[type='submit'] {
    padding: 10px;
  }
}
</style>
