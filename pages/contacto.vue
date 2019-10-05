<template lang="pug">
  v-container
    h2.display-1.text-center.mt-5 Escribenos
    v-row(justify="center")
      v-col(cols="11")
        v-form(method="post" style="max-width:700px;margin:2rem auto 0")
          v-text-field(v-model="name" :counter="10" label="Name" outlined)
          v-text-field(v-model="email" :counter="10" label="E-mail" outlined)
          v-textarea(outlined name="input-7-4" label="Outlined textarea" value="Su mensaje aquí")
          v-btn(color="success" type="submit") Enviar mensaje
</template>
