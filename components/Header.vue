<template>
  <nav>
    <NuxtLink to="/"> Home </NuxtLink>
    <NuxtLink to="/contact"> Contact </NuxtLink>
  </nav>
</template>
<style>
nav {
  display: flex;
  padding: 1rem 2.5rem;
}
a {
  margin-right: 1rem;
}
.nuxt-link-exact-active {
  text-decoration: underline;
}
</style>
