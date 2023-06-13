<template>
  <div id="qr-code-full-region"></div>
</template>

<script setup lang="ts">
import { onMounted } from "vue";
import { Html5QrcodeResult, Html5QrcodeScanner } from "html5-qrcode";

const props = defineProps({
  currentScanning: String,
});

const qrbox = 350; // Set the size of the QR code scanning region
const fps = 1; // Set the desired frames per second
const emit = defineEmits(["result"]);
let html5QrcodeScanner: Html5QrcodeScanner | null;

const onScanSuccess = (
  decodedText: string,
  decodedResult: Html5QrcodeResult
) => {
  emit("result", decodedText, decodedResult);

  if (props.currentScanning === "location") {
    html5QrcodeScanner?.clear();
  }
};

onMounted(() => {
  const config = {
    fps: fps,
    qrbox: qrbox,
    videoConstraints: { facingMode: { exact: "environment" } },
    legacyMode: false,
  };

  html5QrcodeScanner = new Html5QrcodeScanner(
    "qr-code-full-region", // ID of the element to render the scanner
    config,
    undefined
  );

  html5QrcodeScanner.render(onScanSuccess, () => {});
});
</script>
