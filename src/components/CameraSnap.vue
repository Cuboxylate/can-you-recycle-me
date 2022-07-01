<template>
    <div class="CameraSnap">
    <h2>Camera Snap Component</h2>
    <button class="CameraSnap__button">Take picture</button>
    <label for="postcode">Postcode:</label>
    <input
        type="text"
        id="postcode"
        name="postcode"
        required
        minlength="4"
        maxlength="8"
        class="CameraSnap__input">
    <button @click="myFunction()">Get info</button>

        <div id="myDIV">
            
        </div>
    </div>
</template>

<script>
export default {
    name: "CameraSnap",
    
    methods: {
        myFunction() {
            console.log("hello")
            var x = document.getElementById("myDIV");
            if (x.style.display === "none") {
                x.style.display = "block";
            } else {
                x.style.display = "none";
            }
        }
    }
}
</script>

<style scoped>
.CameraSnap {
    display: flex;
    flex-direction: column;
    max-width: 400px;
    margin: 0 auto;
}

.CameraSnap__button {
    margin: 10px;
    width: 80%;
}

.CameraSnap__input {
    margin: 10px;
    width: 40%;
}

</style>