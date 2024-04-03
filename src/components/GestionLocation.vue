
<script setup>
import { ref} from 'vue'

// declare a ref to hold the element reference
// the name must match template ref value
const titleref = ref(null)
const descriptionref = ref(null)

const titleerror =ref(false)

    function addLocation(){

    console.log(titleref.value);
    console.log(descriptionref.value);


       var formdata = new FormData();

        formdata.append("title", titleref.value);
        formdata.append("description", descriptionref.value);


        var obj = { title:titleref.value,
                    description: descriptionref.value
                  };

        var requestOptions = {
            method: 'POST',
            body: new URLSearchParams(obj).toString(),
            headers: {
                'Accept' : 'application/json',
                'Content-Type' : 'application/x-www-form-urlencoded',
                'Authorization': 'Bearer ' +  localStorage.getItem("gite-local-login-token" )
            },
           // mode: 'no-cors'
        };

        fetch("http://gite.local/api/location", requestOptions)
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
    <form name="location" method="post"  @submit.prevent="addLocation">
        <div id="location">
            <div>
                <p v-if="titleerror">Le titre faire plus de 2 caracteres</p>
                <label for="location_Title" class="required">Title</label>
                <input  v-model="titleref"   type="text" id="location_Title" name="location[Title]" required="required" maxlength="255"></div>
            <div><label for="location_description">Description</label><textarea  v-model="descriptionref" id="location_description"
                                                                                name="location[description]"></textarea>
            </div>
            <div>
                <button type="submit" id="location_Envoyer" name="location[Envoyer]">Envoyer</button>
            </div>
            <input type="hidden" id="location__token" name="location[_token]"
                   value="6a.IVrudzF2CH9CK9sWyjKUEPKhWqtLb1QryMazS6A3KkE.azytEhwdREoEQ69xnVfbKMX3Dsw5IjVZpazRDs0GUi9QDoM0B0B8Khtulg">
        </div>
    </form>
</template>