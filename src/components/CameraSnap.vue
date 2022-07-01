<template>
    <div>
        <div>
             <img class="CameraSnap__logo" src="@/assets/Gomeco-logo.png" alt="logo" />
        </div>
        <p class="CameraSnap__paragraph">
            Scan your item's recycling logo and enter your postcode to find out how to responsibly dispose of it!
        </p>
        <div class="CameraSnap">
            <video class="CameraSnap__video" ref="video" @canplay="initCanvas()">Stream unavailable</video>
            <canvas ref="canvas" style="display: none;" />
            <button class="CameraSnap__button" @click="takePicture()">Take picture</button>

            <div class="CameraSnap__location-input">
                <label for="postcode">Postcode:</label>
                <input
                    type="text"
                    id="postcode"
                    name="postcode"
                    required
                    minlength="4"
                    maxlength="8"
                    class="CameraSnap__input">
            </div>

            <button class="CameraSnap__button" @click="getResults()">Get info</button>

            <div id="results">
                <p class="CameraSnap__text">Your item has been identifed as:</p>
                <p class="CameraSnap__text"><strong>Plastics type 2</strong></p>
                <h2 class="CameraSnap__text">How to dispose of this item</h2>
                <div class="CameraSnap__response-box">
                    <h3>1. Preparation</h3>
                    <p class="CameraSnap__respose-paragraph">Please wash well.</p>
                </div>
                <div class="CameraSnap__response-box">
                    <h3>2. Where to put this item</h3>
                    <p class="CameraSnap__respose-paragraph">This item can be added to your council's kerbside recycling bin.</p>
                </div>
                <div class="CameraSnap__response-box">
                    <h3>3. What will happen next?</h3>
                    <p class="CameraSnap__respose-paragraph">This plastic will be melted down and used to make new bottles, reducing our need to extract and refine crude oil.</p>
                </div>
                <p class="CameraSnap__thanks"><strong>Thank you!</strong></p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "CameraSnap",

    data() {
        return {
            video: null,
            image: null
        }
    },

    mounted() {
        this.canvas = this.$refs.canvas
        this.video = this.$refs.video
        this.startCapture()
        var x = document.getElementById("results");
        x.style.display = "none";
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

        getResults() {
            var x = document.getElementById("results");
            x.style.display = x.style.display === "none" ? "block" : "none"
        },

        initCanvas() {
            console.log("Init canvas")
            this.canvas.setAttribute('width', this.video.videoWidth)
            this.canvas.setAttribute('height', this.video.videoHeight)
        },

        takePicture() {
            let context = this.canvas.getContext('2d')
            context.drawImage(this.video, 0, 0, this.video.videoWidth, this.video.videoHeight)
            this.image = this.canvas.toDataURL('image/png')
            this.video.style.display = "none"
            this.canvas.style.display = "block"
            this.canvas.srcObject = this.image
        }

    },

}
</script>

<style scoped>
.CameraSnap {
    display: flex;
    flex-direction: column;
    max-width: 400px;
    margin: 0 auto;
}

.CameraSnap__logo {
    width: 15%;
    min-width: 200px;
}

.CameraSnap__button {
    width: 40%;
    height: 30px;
    margin: 20px auto;
    background-color: #87e378;
    border: 1px solid #299416;
    border-radius: 5px;
}

.CameraSnap__input {
    margin: 10px;
    width: 60%;
}

.CameraSnap__paragraph {
    font-size: 24px;
    width: 80%;
    margin: 20px auto;
}

.CameraSnap__video {
    margin-top: 30px;
}

.CameraSnap__location-input {
    margin: 0 auto;
}

.CameraSnap__respose-paragraph {
    padding-left: 5%;
}

.CameraSnap__response-box {
    border: 1px solid #299416;
    margin: 10px;
    padding: 20px;
}

.CameraSnap__thanks {
    color: #299416;
    font-size: 24px;
    font-weight: 1000;
    text-align: center;
}

.CameraSnap__text {
    text-align: center;
}

</style>