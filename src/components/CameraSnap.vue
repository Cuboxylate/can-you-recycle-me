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
            <button @click="getResults()">Get info</button>

            <div id="results">
                <p>Your item has been identifed as: <strong>Plastics type 2</strong></p>
                <h2>How to dispose of this item</h2>
                <h3>Preparation</h3>
                <p>Please wash well.</p>
                <h3>Where to put this item</h3>
                <p>This item can be added to your council's kerbside recycling bin.</p>
                <h3>What will happen next?</h3>
                <p>This plastic will be melted down and used to make new bottles, reducing our need to extract and refine crude oil.</p>
                <p>Thank you!</p>
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