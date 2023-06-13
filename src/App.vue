<template>
  <div id="app">
    <div>
      <h1>scan Location</h1>
      <div class="section">
        <QRScanner
          currentScanning="location"
          v-bind:qrbox="250"
          v-bind:fps="10"
          style="width: 100%"
          @result="onScan"
        />
      </div>
    </div>

    <div>
      <h3>Scaned Location: {{ location }}</h3>
      <button v-if="!isScanningAssets" @click="startScanningAssets">
        Scan assets
      </button>
    </div>
    <div>
      <div
        v-if="isScanningAssets"
        class="section"
        style="width: 500px; margin: auto"
      >
        <QRScanner
          currentScanning="assets"
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

const isScanningAssets = ref(false);
const location = ref<string>("");
const assets = ref<string[]>([]);

function onScan(decodedText: string, decodedResult: Html5QrcodeResult) {
  if (!isScanningAssets.value) {
    location.value = decodedText;
  } else {
    assets.value.push(decodedText);
  }
  console.log(decodedResult);
}

function startScanningAssets() {
  isScanningAssets.value = true;
}
</script>
