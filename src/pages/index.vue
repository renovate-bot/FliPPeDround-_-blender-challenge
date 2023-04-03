<script setup lang="ts">
const getChallenge = () => {
  const modules = import.meta.glob('/public/modules/*.glb')

  const models = Object.keys(modules).map((item) => {
    const path = item.split('/')[3]
    const day = path.split('-')[0]
    const name = path.split('-')[1].split('.')[0]
    return {
      day,
      name,
      path,
    }
  })

  return models
}
</script>

<template>
  <div
    flex="~ col" items-start
    w-full max-w-3xl mx-auto
  >
    <h1
      mb-2 text-xl font-bold mb-4
    >
      100 days
    </h1>
    <div
      v-for="challenge in getChallenge()"
      :key="challenge.path"
      grid gap-x-4 gap-y-1 grid-cols-1 sm:grid-cols-2 lg:grid-cols-3
    >
      <p
        class="link"
        link-block
        mr-4 text-lg
        hover:c-gray-7
        transition duration-200 ease-in-out c-gray
        @click="() => $router.push(`/${challenge.path}`)"
      >
        <span mr-2 opacity-50>
          {{ challenge.day }}
        </span>
        <b>
          {{ challenge.name }}
        </b>
      </p>
    </div>
  </div>
</template>
