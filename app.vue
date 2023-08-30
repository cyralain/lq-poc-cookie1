

<script setup lang="ts">

const loading = ref(true)

// Expire dans un an
const expires = new Date();
expires.setTime(expires.getTime() + (365 * 24 * 60 * 60 * 1000));

const sunrise = useCookie('sunriseATE', { expires });

const reload = () => {
  location.reload();
}

function getRndInteger(min, max) {
  return Math.floor(Math.random() * max) + min;
}



  var userSelected = getRndInteger(1, 100);
  if (userSelected < 31) {
    sunrise.value = (sunrise.value || 0) + 1
  }

</script>

<template>
  <h1 class="text-3xl mb-3"> POC Cookies - Déploiement progressif avec A10</h1>
  <div>Valeur aléatoire: {{ userSelected }}</div>

  <template v-if="sunrise">
      <h1 class="text-3xl mb-3">
        Vous avez été selectionné pour ATE! 👋👋👋
      </h1>
      <div>
        <NTip n="green6" icon="carbon:idea" class="inline-flex">
          Le cookie 'sunrise' a été créé et en cliquant sur le bouton, la page va se recharger. Le A10 va détecter le cookie et vous serez diriger vers ATE!
        </NTip>
      </div>
      <div class="mt-3">
        <NButton n="red" icon="carbon:logout" @click="reload">
          Reload
        </NButton>
      </div>
    </template>

    <template v-else>
      <div>
        <NTip n="green6" icon="carbon:idea" class="inline-flex">
          Pas de cookie sunrise!
        </NTip>
      </div>
    </template>
</template>

