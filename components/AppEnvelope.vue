<template>
    <div
        ref="target"
        class="custom-transition mid"
        style="position: absolute"
        @click="isClicked = true"
        :class="{ 'is-clicked': isClicked }"
    >
        <div id="envelope" :class="isOpen ? 'open' : 'close'">
            <div class="front flap"></div>
            <div class="front pocket"></div>
        </div>
        <p class="warning mid" :class="{ active: isWarning }">
            This message will disappear 10 seconds after u open it
        </p>
        <div class="text mid" :class="{ active: isText, closed: isTextClosed }">
            <div class="title">
                <p>Donte Saint Cali</p>
                <p>Release Party</p>
            </div>
            <div class="infos">
                <p>Jeudi 9 mai 2024</p>
                <p>20h</p>
                <p>Paris, Scandle 68 rue blanche 75009</p>
            </div>
        </div>
    </div>
</template>

<script lang="ts" setup>
const target = ref<HTMLDivElement>();
const isClicked = ref<boolean>(false);
const isOpen = ref<boolean>(false);
const isWarning = ref<boolean>(false);
const isText = ref<boolean>(false);
const isTextClosed = ref<boolean>(false);

watchOnce(isClicked, () => {
    setTimeout(() => {
        isOpen.value = true;
        setTimeout(() => {
            isWarning.value = true;
            setTimeout(() => {
                isWarning.value = false;
                isText.value = true;
                setTimeout(() => {
                    isTextClosed.value = true;
                }, 12000);
            }, 3500);
        }, 1400);
    }, 500);
});
</script>

<style lang="scss" scoped>
@use 'sass:math';

.custom-transition {
    transition: all ease 0.3s;
    user-select: none;
    cursor: pointer;

    &.is-clicked {
        cursor: default !important;
        user-select: text;
    }
}

.text {
    color: white;
    display: flex;
    flex-direction: column;
    align-items: start;
    gap: 10px;
    transition: opacity ease-out 1s;
    width: 85vw;

    & > div {
        overflow: hidden;
        display: flex;
        flex-direction: column;
    }

    p {
        transition: all ease-out 1s 1s;
    }

    .title {
        flex-basis: 100%;
        p {
            font-family: 'Ade Display', sans-serif;
            font-size: 40px;
            text-transform: uppercase;
            margin-top: 5px;
            transform: translateX(110%);
        }
    }

    .infos {
        flex-basis: 100%;
        p {
            font-family: 'Montserrat', sans-serif;
            font-weight: 300;
            font-size: 20px;
            transform: translateX(-110%);
        }
    }

    &.active {
        p {
            transform: translateX(0%);
        }
    }

    &.closed {
        opacity: 0;
        pointer-events: none;
    }
}

.warning {
    font-family: 'Helvetica Medium', sans-serif;
    text-transform: uppercase;
    color: white;
    font-weight: 400;
    font-size: 25px;
    opacity: 0;
    transition: all ease-out 0.5s;
    width: 85vw;
    text-align: center;

    &.active {
        opacity: 1;
    }
}

$color-env: #f0f0f0;
$color-env2: darken($color-env, 3%);
$color-flap: darken($color-env, 20%);
$color-bg: lighten($color-env, 48%);

$env-border-radius: 6px;
$env-width: 280px;
$env-height: 180px;

#envelope {
    position: relative;
    width: $env-width;
    height: $env-height;
    border-bottom-left-radius: $env-border-radius;
    border-bottom-right-radius: $env-border-radius;
    margin-left: auto;
    margin-right: auto;
    background-color: $color-flap;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);

    transition: opacity ease-out 0.8s 0.8s;

    &.open {
        opacity: 0;
    }
}

.front {
    position: absolute;
    width: 0;
    height: 0;
    z-index: 3;
}

.flap {
    border-left: math.div($env-width, 2) solid transparent;
    border-right: math.div($env-width, 2) solid transparent;
    border-bottom: math.div($env-height, 2) - 8 solid transparent; /* a little smaller */
    border-top: math.div($env-height, 2) + 8 solid $color-flap; /* a little larger */
    transform-origin: top;
    pointer-events: none;
}

.pocket {
    border-left: math.div($env-width, 2) solid $color-env;
    border-right: math.div($env-width, 2) solid $color-env;
    border-bottom: math.div($env-height, 2) solid $color-env2;
    border-top: math.div($env-height, 2) solid transparent;
    border-bottom-left-radius: $env-border-radius;
    border-bottom-right-radius: $env-border-radius;
}

.open .flap {
    transform: rotateX(180deg);
    transition:
        transform 0.4s ease,
        z-index 0.6s;
    z-index: 1;
}

.close .flap {
    transform: rotateX(0deg);
    transition:
        transform 0.4s 0.6s ease,
        z-index 1s;
    z-index: 5;
}

.close .letter {
    transform: translateY(0px);
    transition:
        transform 0.4s ease,
        z-index 1s;
    z-index: 1;
}

.open .letter {
    transform: translateY(-(math.div($env-height, 3)));
    transition:
        transform 0.4s 0.6s ease,
        z-index 0.6s;
    z-index: 2;
}
</style>
