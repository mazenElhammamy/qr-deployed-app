<template>
  <div id="app">
    <div v-if="!closeLocationScanner">
      <h1>scan Location</h1>
      <div class="section" style="width: 500px; margin: auto">
        <QRScanner
          :asset="asset"
          v-bind:qrbox="250"
          v-bind:fps="10"
          style="width: 500px"
          @result="onScan"
        />
      </div>
    </div>

    <div v-else>
      <h3>Scaned Location: {{ location }}</h3>
      <button v-if="!asset" @click="openSanner">Scan assets</button>
    </div>
    <div>
      <div v-if="asset" class="section" style="width: 500px; margin: auto">
        <QRScanner
          :asset="asset"
          v-bind:qrbox="250"
          v-bind:fps="10"
          style="width: 500px"
          @result="onScan"
        />
        <div>
          <h3>Scaned Assets</h3>
          <div v-for="(asset, index) in assets" :key="index">{{ asset }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { Html5QrcodeResult } from "html5-qrcode";
import QRScanner from "./components/QRCodeScanner.vue";
import { ref } from "vue";

const asset = ref(false);
const location = ref<string>("");
const assets = ref<string[]>([]);
const closeLocationScanner = ref(false);

function onScan(decodedText: string, decodedResult: Html5QrcodeResult) {
  if (!asset.value) {
    location.value = decodedText;
    closeLocationScanner.value = true;
  } else {
    assets.value.push(decodedText);
  }
  console.log(decodedResult);
}

function openSanner() {
  asset.value = true;
}
</script>
