<script>

</script>

<template>
	<header class="header">
		<div class="header__container">
			<div class="header__inner">
				<a href="" class="header__logo logo">
					<img src="@/assets/images/logo.svg" loading="lazy" alt="Картинка">
				</a>
				<div class="header__text">
					Contact management
					<span>Nuxt3</span>
				</div>
			</div>
		</div>
	</header>
</template>

<style scoped lang="scss">
	.header {
		position: fixed;
		z-index: 50;
		width: 100%;
		padding: 0.9375rem 0;
		background-color: #fff;
		box-shadow: 0 0 0.3125rem rgba(0, 0, 0, 0.5);
		@media (max-width: 48em){
			padding: 0.9375rem 0;  
		}
	}
	.header__container {
	}
	.header__inner {
		display: flex;
		align-items: center;
		flex-wrap: wrap;
		column-gap: 1.5625rem;
		row-gap: 0.9375rem;
		@media (max-width: 48em) {
			  flex-direction: column;
		}
	}
	.header__logo {
		width: 11.25rem;
		flex: 0 0 11.25rem;
    height: 1.75rem;
		@media (max-width: 48em){
			  flex: 1 1 auto;
				height: 1.25rem;
		}
	}
	.logo {
		position: relative;
		display: flex;
		justify-content: center;
		align-items: center;
		overflow: hidden;
		img {
			width: 100%;
			height: 100%;
			object-fit: contain;
		}
	}
	.header__text {
		font-size: 2.25rem;
    font-weight: 700;
    height: 100%;
    flex: 0 1 68%;
    display: flex;
		flex-direction: column;
    justify-content: center;
		align-items: center;
		gap: 0.375rem;
		span {
			font-size: 1.625rem;
			font-weight: 500;
			color: #8ed078;
		}
		@media (max-width: 48em){
				display: none;
		}
	}
 </style>