<template>
  <div class="c-sidenav">
    <ul>
      <li><nuxt-link to="/">商品写真</nuxt-link></li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'SidenavComponent',
}
</script>

<style lang="scss" scoped>
.c-sidenav {
  position: fixed;
  top: 0;
  left: 0;
  background: #eee;
	@include pc {
		bottom: 0;
		width: 200px;
		padding: 20px 30px;
	}
  @include sp {
		display: flex;
		align-items: center;
		right: 0;
		height: 40px;
		padding: 5px 15px;
  }
}
</style>
