
<script setup>
import { ref} from 'vue'

// declare a ref to hold the element reference
// the name must match template ref value
const usernameref = ref(null)
const passwordref = ref(null)

const titleerror =ref(false)

    function login(){

    console.log(usernameref.value);
    console.log(passwordref.value);


       var formdata = new FormData();

        formdata.append("username", usernameref.value);
        formdata.append("password", passwordref.value);


        var obj = { username:usernameref.value,
                    password: passwordref.value
                  };

        var requestOptions = {
            method: 'POST',
            //body: new URLSearchParams(obj).toString(),
           body :JSON.stringify(obj),
            headers: {
                'Accept' : 'application/json',
                'Content-Type' : 'application/json',
               // 'X-Requested-With': 'XMLHttpRequest'
            },
        };

        fetch("http://gite.local/api/login", requestOptions)
            .then(response => { console.log(response);
                              return response.json() ;
                               })
            .then(result => {
                console.log(result)
                console.log(result.token)
                localStorage.setItem("gite-local-login-token", result.token )

            })
            .catch(error => console.log('error', error));


        console.log("ok");


        // Init tab
    //titleerror.value=titleref.value.length <2;

}

</script>


<template>
    <form name="location" method="post"  @submit.prevent="login">
        <div id="location">
            <div>
                <p v-if="titleerror">Le titre faire plus de 2 caracteres</p>
                <label for="location_Title" class="required">Email</label>
                <input  v-model="usernameref"   type="email" id="location_Title" name="location[Title]" required="required" maxlength="255"></div>
            <div><label for="location_description">Mot de passe </label>  <input  v-model="passwordref"   type="password" id="location_Title" name="location[Title]" required="required" maxlength="255">
            </div>
            <div>
                <button type="submit" id="location_Envoyer" name="location[Envoyer]">Envoyer</button>
            </div>
            <input type="hidden" id="location__token" name="location[_token]"
                   value="6a.IVrudzF2CH9CK9sWyjKUEPKhWqtLb1QryMazS6A3KkE.azytEhwdREoEQ69xnVfbKMX3Dsw5IjVZpazRDs0GUi9QDoM0B0B8Khtulg">
        </div>
    </form>
</template>