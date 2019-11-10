<template>
    <div class="button-handler-container">
        <div v-if="!isCamActive" class="buttons">
            <button
               class="button green-button"
               type="button"
               @click="$emit('click:openWebCam')"
            >
                Open Camera
            </button>
            <button
               class="button"
               :class="{'red-button': captures.length > 0, 'disabled': captures.length < 1 }"
               :disabled="captures.length < 1"
               type="button"
               @click="$emit('click:clearHistory')"
            >
                Clear History
            </button>
        </div>
        <div v-if="isCamActive" class="buttons">
            <button
              class="button green-button"
              :class="{'disabled': !isCamOnline }"
              :disabled="!isCamOnline"
              id="snap"
              @click="$emit('click:capture')"
            >
                Capture
            </button>
            <button
              class="button white-button"
              type="button"
              @click="$emit('click:closeWebCam')"
            >
                Back
            </button>
        </div>
    </div>
</template>

<script>
    export default {
        name: "ButtonsHandler",
        props: {
            isCamActive: {
                type: Boolean,
                default: false,
            },
            isCamOnline: {
                type: Boolean,
                default: undefined,
            },
            captures:{
                type: Array,
                default: () => ([])
            }
        }
    }
</script>

<style scoped>

.button-handler-container {
    display: flex;
    align-items: center;
    width: 500px;
    height: 50px;
}

.buttons {
    width: 100%;
    display: flex;
    justify-content: space-around;
}

.button {
    height: 45px;
    border-radius: 5px;
    padding: 12px;
    font-size: 16px;
    text-align: center;
    min-width: 120px;
    -webkit-box-shadow: 0px 0px 10px 4px rgba(0,0,0,0.2);
    -moz-box-shadow: 0px 0px 10px 4px rgba(0,0,0,0.2);
    box-shadow: 0px 0px 10px 4px rgba(0,0,0,0.2);
}

.green-button {
    background-color: #4b9c7b;
    border-color: #4b9c7b;
    color: white;
}

.red-button {
    background-color: #c85b5b;
    border-color: #c85b5b;
    color: white;
}

.disabled {
    cursor: none;
    pointer-events: none;
    opacity: 0.5;
}


@media screen and (max-width: 425px) {
    .button-handler-container {
        width: 100%;
    }
}
</style>