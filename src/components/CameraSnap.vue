<template>
    <div>
        <div class="CameraSnap">
        <h2>Camera Snap Component</h2>
        <video ref="video" @canplay="initCanvas()">Stream unavailable</video>
        <canvas ref="canvas" style="display: none;" />

        <button class="CameraSnap__button" @click="takePicture()">Take picture</button>
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
        this.canvas = this.$refs.canvas
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
        },

        initCanvas() {
            console.log("Init canvas")
            this.canvas.setAttribute('width', this.video.videoWidth)
            this.canvas.setAttribute('height', this.video.videoHeight)
        },

        takePicture() {
            let context = this.canvas.getContext('2d')
            context.drawImage(this.video, 0, 0, this.video.videoWidth, this.video.videoHeight)
            this.$emit('picture-taken', this.canvas.toDataURL('image/png'))
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