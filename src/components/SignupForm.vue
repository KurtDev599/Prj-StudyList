<template>
	<form @submit.prevent="submitForm">
		<div>
			<label for="userName">id(email) :</label>
			<input id="userName" type="text" v-model="userName" />
		</div>
		<div>
			<label for="password">password :</label>
			<input id="password" type="text" v-model="password" />
		</div>
		<div>
			<label for="nickName">nickName :</label>
			<input id="nickName" type="text" v-model="nickName" />
		</div>
		<button
			:disabled="!isUsernameValid || !password || !nickName"
			type="submit"
		>
			회원 가입
		</button>
		<p>{{ logMessage }}</p>
	</form>
</template>

<script>
import { registerUser } from '@/api'
import { validateEmail } from '@/utils/validation'
export default {
	name: 'SignupForm',
	data() {
		return {
			userName: '',
			password: '',
			nickName: '',
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
			const userData = {
				username: this.userName,
				password: this.password,
				nickname: this.nickName,
			}
			const { data } = await registerUser(userData)
			this.logMessage = `${data.username} 님이 가입되었습니다.`
			this.initForm()
		},
		initForm() {
			this.userName = ''
			this.password = ''
			this.nickName = ''
		},
	},
}
</script>
