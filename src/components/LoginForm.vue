<template>
	<form @submit.prevent="submitForm">
		<div>
			<label for="username"></label>
			<input id="username" v-model="userName" type="text" />
		</div>
		<div>
			<label for="password"></label>
			<input id="password" v-model="password" type="text" />
		</div>
		<button :disabled="!isUsernameValid || !password" type="submit">
			로그인
		</button>
		<p>{{ logMessage }}</p>
	</form>
</template>

<script>
import { loginUser } from '@/api'
import { validateEmail } from '@/utils/validation'

export default {
	data() {
		return {
			userName: '',
			password: '',
			logMessage: '',
		}
	},
	computed: {
		isUsernameValid() {
			return validateEmail(this.userName)
		},
	},
	methods: {
		async submitForm() {
			try {
				const userData = {
					username: this.userName,
					password: this.password,
				}
				const { data } = await loginUser(userData)
				this.logMessage = data.user.username
				this.initForm()
			} catch (e) {
				this.logMessage = e.response.data
			}
		},
		initForm() {
			this.userName = ''
			this.password = ''
		},
	},
}
</script>
