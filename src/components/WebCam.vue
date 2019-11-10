<template>
    <div class="webcam-container">
        <section class="webcam-header">
            <img v-if="!isCamActive" src="../assets/main.png" alt="main">
            <div v-show="isCamActive">
                <img class="face-line" src="../assets/face-line.png" alt="face">
                <video ref="video" id="video" width="640" height="480" autoplay></video>
                <canvas ref="canvas" id="canvas" width="640" height="480"></canvas>
            </div>
        </section>
        <section  class="webcam-content">
            <ButtonsHandler
              :is-cam-active="isCamActive"
              :captures="captures"
              @click:openWebCam="openWebCam"
              @click:clearHistory="clearHistory"
              @click:capture="capture"
              @click:closeWebCam="closeWebCam"
            />
            <History
              :captures="captures"
            />
        </section>
    </div>
</template>

<script>

    import History from "@/components/History";
    import ButtonsHandler from "@/components/ButtonsHandler";

    export default {
        name: 'WebCam',
        components:{ History,ButtonsHandler },
        data() {
            return {
                isCamActive: false,
                video: {},
                canvas: {},
                captures: []
            }
        },
        methods: {
            openWebCam(){
                this.video = this.$refs.video;
                this.isCamActive = true;
                if(navigator.mediaDevices && navigator.mediaDevices.getUserMedia) {
                    navigator.mediaDevices.getUserMedia({ video: true }).then(stream => {
                        this.video.srcObject = stream;
                        this.video.play();
                    });
                }
            },
            closeWebCam(){
                this.video.srcObject.getTracks().forEach(function(track) {
                    track.stop();
                });
                this.isCamActive = false;
            },
            capture() {
                this.canvas = this.$refs.canvas;
                this.canvas.getContext("2d").drawImage(this.video, 0, 0, 640, 480);
                this.captures.push({
                    img: this.canvas.toDataURL("image/png"),
                    id: this.captures.length
                });
            },
            clearHistory(){
                this.captures = []
            }
        },
    }
</script>

<style scoped>

    .webcam-container {
        padding: 20px;
        height: 100vh;
        box-sizing: border-box;
    }

    .webcam-header {

    }

    .webcam-content {
        display: flex;
        flex-direction: column;
        align-items: center;
        margin-top: 50px;
    }

    .face-line {
        position: absolute;
        top: 0;
        left: 50%;
        transform: translate(-50%, 30%);
        width: 500px;
    }

    #video {
        background-color: #000000;
    }
    #canvas {
        display: none;
    }


    @media screen and (max-width: 425px) {

        .webcam-header {
            display: contents;
        }

        .webcam-header , img {
            width: 360px;
        }

        .webcam-header , video {
            width: 320px;
            height: 240px;
        }

        .face-line {
            transform: translate(-50%, 50%);
            width: 250px;
        }
    }
</style>