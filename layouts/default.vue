<template>
  <div>
    <CommonSidenav />
    <main>
      <Nuxt />
    </main>
  </div>
</template>

<script>
export default {
  name: 'DefaultLayout',
}
</script>

<style lang="scss">
main {
  min-height: 100vh;
  @include pc {
    padding-left: 200px;
  }
	@include sp {
		padding-top: 40px;
	}
}
</style>