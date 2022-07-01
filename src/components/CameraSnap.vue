<template>
    <div>
        <div>
            <h2>Gomeco Vision</h2>
            <video ref="video">Stream unavailable</video>
        </div>
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
    </div>
</template>

<script>
export default {
    name: "CameraSnap",
    mounted() {
        this.video = this.$refs.video
        this.startCapture()
    },

    methods: {
        startCapture() {
            navigator.mediaDevices.getUserMedia({video: true, audio: false}).then(
                stream => {
                    this.video.srcObject = stream
                    this.video.play()
                }
            ).catch( error => {
                console.log(error)
            })
        },
        myFunction() {
            console.log("hello")
            var x = document.getElementById("myDIV");
            if (x.style.display === "none") {
                x.style.display = "block";
            } else {
                x.style.display = "none";
            }
        }
    },

    data() {
        return {
            video: null
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