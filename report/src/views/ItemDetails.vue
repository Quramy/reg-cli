<template>
    <div>
        <div class="items" v-for="item in items" v-bind:key="item.encoded">
            <a :href="'#' + item.encoded" :id="item.encoded" :class="'ui link ' + color">
                <i :class="'ui icon ' + icon"></i>{{item.raw}}
            </a>
            <div class="captures">
                <div v-if="diffDir" class="capture" v-on:click="open(diffDir + item.raw, actualDir + item.raw)">
                    <capture-image :src="diffDir + item.raw" :bg="actualDir + item.raw" :kind="'Diff'"></capture-image>
                </div>
                <div v-if="actualDir" class="capture" v-on:click="open(actualDir + item.raw)">
                    <capture-image :src="actualDir + item.raw" :kind="'After'"></capture-image>
                </div>
                <div v-if="expectedDir" class="capture" v-on:click="open(expectedDir + item.raw)">
                    <capture-image :src="expectedDir + item.raw" :kind="'Before'"></capture-image>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
const CaptureImage = require('./CaptureImage.vue');

module.exports = {
    name: 'ItemDetails',
    components: {
        'capture-image': CaptureImage,
    },
    props: ['items', 'color', 'icon', 'open', 'diffDir', 'actualDir', 'expectedDir'],
    data: () => ({
        // showSummary: false,
    }),
}
</script>

<style scoped src="../styles/common.css"></style>
<style scoped>
.capture {
    flex-basis: 30%;
    cursor: pointer;
}

.captures {
    display: flex;
    justify-content: space-between;
    margin: 15px 0 40px;
}
</style>
