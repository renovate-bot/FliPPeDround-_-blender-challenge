<script setup lang="ts">
import routes from 'virtual:generated-pages'

const getChallenge = () => {
  const challenges = routes.filter(route => route.path.startsWith('/day/'))
  if (!challenges)
    throw new Error('No challenge found for path')

  const challengeList = challenges.map((item) => {
    const [_, day, name] = (item.name as string).split('-')
    return {
      day,
      name,
      path: `${item.path}`,
    }
  })

  return challengeList
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
      <a
        :href="challenge.path"
        class="link"
        link-block mr-4
        text-lg
        hover:c-gray-7 transition duration-200 ease-in-out
        c-gray
      >
        <span mr-2 opacity-50>
          {{ challenge.day }}
        </span>
        <b>
          {{ challenge.name }}
        </b>
      </a>
    </div>
  </div>
</template>
