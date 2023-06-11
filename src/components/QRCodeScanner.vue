<template>
    <div id="qr-code-full-region"></div>
  </template>
  
  <script setup lang="ts">
  import { onMounted } from 'vue';
  import { Html5QrcodeResult, Html5QrcodeScanner } from 'html5-qrcode';
  
  const qrbox = 250; // Set the size of the QR code scanning region
  const fps = 1; // Set the desired frames per second
  const emit = defineEmits(['result'])
     
  const onScanSuccess = (decodedText: string, decodedResult: Html5QrcodeResult) => {
    // Handle the scanned QR code result
    emit('result',decodedText)
    console.log('Decoded Text:', decodedText,decodedResult);
    console.log('Decoded Result:', decodedResult);
  };
  
  onMounted(() => {
    const config = {
      fps: fps,
      qrbox: qrbox,
    };
  
    const html5QrcodeScanner = new Html5QrcodeScanner(
      "qr-code-full-region", // ID of the element to render the scanner
      config,
      undefined
    );
  
    html5QrcodeScanner.render(onScanSuccess, ()=>{});
  });
  </script>
  
  