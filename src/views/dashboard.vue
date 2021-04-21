<template>
<section>
<h1> SAUDI ELECTRICITY COMPANY </h1>
<h1 v-if = "user">{{user.username}} </h1>
<h1 v-if = "!user">hey user you must log in first ok </h1>
<button @click="logout()" class="btn btn-primary">LogOut</button>
</section>
</template>


<script>

const api_Url = 'http://localhost:5000/';
export default {
data: () => ({
    user: null,
}),
mounted() {
    fetch(api_Url, {
        headers: {
            authorization: `Bearer ${localStorage.token}`,

        },
    })
    .then(res => res.json())
    .then((result) => {
        if(result.user) {
            this.user = result.user;
        } else {
            this.logout();
        }
    });

},

methods: {
    logout() {
        localStorage.removeItem('token');
        this.$router.push('/login');
    },
},
};


</script>
<style>


</style>
