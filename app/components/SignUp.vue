<template>
    <Page class="page">
		<ActionBar title="Todo app" class="action-bar" />

        <FlexboxLayout class="page" width="100%" height="100%">
			<StackLayout class="form" width="100%" height="100%">
				
				<StackLayout class="input-field" marginBottom="25">
					<Label fontSize="24"> Créer compte</Label>
				</StackLayout>

				<StackLayout class="input-field" marginBottom="25">
					<TextField class="input" hint="Prenom" keyboardType="text" autocorrect="false" autocapitalizationType="none" v-model="user.firstname"
					 returnKeyType="next" @returnPress="focusPassword" fontSize="18" />
					<StackLayout class="hr-light" />
				</StackLayout>

				<StackLayout class="input-field" marginBottom="25">
					<TextField class="input" hint="Nom" keyboardType="text" autocorrect="false" autocapitalizationType="none" v-model="user.lastname"
					 returnKeyType="next" @returnPress="focusPassword" fontSize="18" />
					<StackLayout class="hr-light" />
				</StackLayout>

				<StackLayout class="input-field" marginBottom="25">
					<TextField class="input" hint="Email" keyboardType="email" autocorrect="false" autocapitalizationType="none" v-model="user.email"
					 returnKeyType="next" @returnPress="focusPassword" fontSize="18" />
					<StackLayout class="hr-light" />
				</StackLayout>

				<StackLayout class="input-field" marginBottom="25">
					<TextField class="input" hint="female / male" keyboardType="text" autocorrect="false" autocapitalizationType="none" v-model="user.gender"
					 returnKeyType="next" @returnPress="focusPassword" fontSize="18" />
					<StackLayout class="hr-light" />
				</StackLayout>

				<Button :text="'Créer compte'" @onTap="signUp" />
				
				<Label class="login-label sign-up-label" @tap="signIn">
                <FormattedString>
                    <Span :text="'Vous aves déjà de compte ? '"></Span>
                    <Span :text="'Se connecter'" class="bold"></Span>
                </FormattedString>
            </Label>
				
			</StackLayout>

		</FlexboxLayout>

    </Page>
</template>

<script>
import Home from './Home.vue';
import SignIn from './SignIn.vue';
import axios from 'axios';
import SignInVue from './SignIn.vue';

/*email: 'test10@mail.fr',
JS:   password: 'tACE2y5wiH',
JS:   uuid: 'dd288ca0-5f86-11ea-a204-a7a3efa88c7c'*/

export default {
	components : {
		Home,
		SignInVue
	},
	methods: {
		signUp() {
			//console.log(this.$navigateTo(SignInVue)+'clickonbutton');
			axios
			.post("https://api.todolist.sherpa.one/users/signup", this.user)
			.then((response) => {
				console.log(response.data)
				this.$navigateTo(SignInVue);
			}).catch((response) => {
				console.log(response)
			})
		}
	},
	data() {
		return {
			user: {firstname: "", lastname: "", email: "", gender: ""}
		}
	}
}
</script>

<style scoped>
#active-task {
  font-size: 20;
  font-weight: bold;
  color: #53ba82;
  margin-left: 20;
  padding-top: 5;
  padding-bottom: 10;
}

#completed-task {
  font-size: 20;
  color: #d3d3d3;
  margin-left: 20;
  padding-top: 5;
  padding-bottom: 10;
  text-decoration: line-through;
}

.home-panel {
  vertical-align: center;
  font-size: 20;
  margin: 15;
}

.description-label {
  margin-bottom: 15;
}

TextField {
  font-size: 20;
  color: #53ba82;
  margin-top: 10;
  margin-bottom: 10;
  margin-right: 5;
  margin-left: 20;
}

Button { 
  font-size: 15; 
  font-weight: bold; 
  color: white; 
  background-color: #53ba82; 
  height: 40;
  margin-top: 10; 
  margin-bottom: 10; 
  margin-right: 10; 
  margin-left: 10; 
  border-radius: 20px; 
}

ActionBar {
  background-color: #35495e;
  color: white; 
}

.login-label {
        horizontal-align: center;
        color: #A8A8A8;
        font-size: 16;
    }

    .sign-up-label {
        margin-bottom: 20;
    }
</style>