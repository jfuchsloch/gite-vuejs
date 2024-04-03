
<script setup>
import { ref} from 'vue'

// declare a ref to hold the element reference
// the name must match template ref value
const titleref = ref(null)

const titleerror =ref(false)

function sendMessage(){

    console.log(titleref.value);


    var formdata = new FormData();

    formdata.append("title", titleref.value);


    var obj = { title:titleref.value
    };

    var requestOptions = {
        method: 'POST',
        body: new URLSearchParams(obj).toString(),
        headers: {
            'Accept' : 'application/json',
            'Content-Type' : 'application/x-www-form-urlencoded',
           // 'Authorization': 'Bearer ' +  localStorage.getItem("gite-local-login-token" )
        },
        // mode: 'no-cors'
    };

    fetch("http://gite.local/contact-api-vue", requestOptions)
        .then(response => { console.log(response);
            return response.json() ;
        })
        .then(result => console.log(result))
        .catch(error => console.log('error', error));


    console.log("ok");


    // Init tab
    titleerror.value=titleref.value.length <2;

}

</script>


<template>
    <form name="contact" method="post"  @submit.prevent="sendMessage"  style="margin-top: 50px">
        <div>
            <div>
                <label for="contactTitle" class="required">TitleMessage</label>
                <input  v-model="titleref"   type="text" id="contactTitle" name="message" required="required" maxlength="255">
            </div>

            <div>
                <button type="submit"  name="Envoyer">Envoyer</button>
            </div>

        </div>
    </form>
</template>