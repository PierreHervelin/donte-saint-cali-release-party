<template>
    <div>
        <AppEnvelope :default-position="{ x: 50, y: 50 }" />
    </div>
</template>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Libre+Caslon+Text:wght@400;700&family=Montserrat:ital,wght@0,100..900;1,100..900&family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap');

@font-face {
    font-family: 'Helvetica Medium';
    src:
        url('./assets/helvetica_medium_condensed-webfont.woff2') format('woff2'),
        url('./assets/helvetica_medium_condensed-webfont.woff') format('woff');
    font-weight: normal;
    font-style: normal;
}

@font-face {
    font-family: 'Ade Display';
    src:
        url('./assets/adedisplay-webfont.woff2') format('woff2'),
        url('./assets/adedisplay-webfont.woff') format('woff');
    font-weight: normal;
    font-style: normal;
}

.mid {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}

body {
    background: #0b0b0b;
}

*,
*::after,
*::before {
    padding: 0;
    margin: 0;
}
</style>
