<template>
	<div>
		<app-header></app-header>
		<router-view></router-view>
	</div>
</template>

<script>
import AppHeader from '@/components/common/AppHeader'
export default {
	name: 'App',
	components: {
		AppHeader,
	},
}
</script>
