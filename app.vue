<script setup lang="ts">

  const loading = ref(true)

  // Expire dans un an
  const expires = new Date();
  expires.setTime(expires.getTime() + (365 * 24 * 60 * 60 * 1000));

  const sunrise = useCookie('sunriseATE', { expires });

  // Reload de la page avec même URL
  const reload = () => {
    location.reload();
  }

  // Retourne un integer aléatoire en min et max
  function getRndInteger(min, max) {
    return Math.floor(Math.random() * max) + min;
  }

  // Assignation valeur aléatoire
  const userSelected = getRndInteger(1, 100);
  
  var cookieAlreadyExist = false; 
  if (sunrise.value) {
    //si cookie exist, on fait rien
    cookieAlreadyExist = true; 
  } else {
      // Pas de cookie, on set la valeur aléatoire
      sunrise.value = userSelected;
  }

</script>

<template>
  <h1 class="text-3xl mb-3"> POC Cookies - Déploiement progressif avec A10</h1>

  <template v-if="cookieAlreadyExist">
      <h1 class="text-3xl mb-3">
        Cookie existe déjà... pour ATE! 👋👋👋<br />
        <div>Valeur aléatoire présente: {{ sunrise }}</div>

      </h1>
      <div class="mt-3">
        <NButton n="red" icon="carbon:logout" @click="reload">
          Reload
        </NButton>
      </div>
    </template>

    <template v-else>
      <h1 class="text-3xl mb-3">
        Cookie vient d'être créé pour ATE! 👋👋👋 <br />
        <div>Valeur aléatoire: {{ userSelected }}</div>
      </h1>
      <div>
        <NTip n="green6" icon="carbon:idea" class="inline-flex">
          Le cookie 'sunriseATE' a été créé et en cliquant sur le bouton, la page va se recharger. Le A10 va détecter le cookie et vous serez dirigé vers ATE!
        </NTip>
      </div>
      <div class="mt-3">
        <NButton n="red" icon="carbon:logout" @click="reload">
          Reload
        </NButton>
      </div>
    </template>
</template>