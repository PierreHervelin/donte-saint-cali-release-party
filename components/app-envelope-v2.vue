<template>
    <div
        style="
            width: 100vw;
            height: 100vh;
            position: relative;
            transition: background-color ease-out 0.5s 0.5s;
        "
        :style="{ backgroundColor: release ? 'white' : '#0b0b0b' }"
    >
        <div style="width: 100%; height: 100%; position: relative; padding: 20px">
            <nuxt-img
                :style="{ opacity: envelope ? 1 : 0 }"
                style="transition: opacity ease-out 0.3s; width: 100%; max-width: 250px"
                class="mid"
                src="/envelope.png"
                @click="handleEnvelopeClick"
            />
            <p
                v-if="warning && !release"
                :style="{
                    opacity: warning && !release ? 1 : 0,
                    pointerEvents: warning && !release ? 'auto' : 'none',
                }"
                style="
                    text-transform: uppercase;
                    font-family: Arial, Helvetica, sans-serif;
                    transition: all ease-out 0.3s 0.5s;
                    animation: blinker ease-out 1.5s infinite;
                    color: white;
                    font-size: 20px;
                    width: 100%;
                    padding: 20px;
                    text-align: center;
                    line-height: 30px;
                "
                class="mid"
                @click="release = true"
            >
                ⚠️ This message will disappear 10 seconds after you open it ⚠️
            </p>
            <div
                style="
                    margin: 20px;
                    font-family: Arial, Helvetica, sans-serif;
                    font-size: 20px;
                    font-weight: 500;
                    max-width: fit-content;
                    transition: opacity ease-out 0.3s 0.8s;
                "
                :style="{
                    opacity: release ? 1 : 0,
                    pointerEvents: release ? 'auto' : 'none',
                }"
            >
                <p>RELEASE PARTY</p>
                <p style="text-transform: uppercase">DONTé SAINT CALI</p>
                <div style="display: flex; flex-direction: column">
                    <p>Scandle 68 rue blanche 75009</p>
                    <div style="display: flex; justify-content: space-between; align-items: center">
                        <p>Jeudi 9 mai 2024</p>
                        <p>20h</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script lang="ts" setup>
const envelope = ref<boolean>(true);
const warning = ref<boolean>(false);
const release = ref<boolean>(false);

function handleEnvelopeClick() {
    envelope.value = false;
    setTimeout(() => {
        warning.value = true;
    }, 500);
}
</script>

<style lang="scss" scoped></style>
