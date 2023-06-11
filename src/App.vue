<template>
  <div id="app">
    <div class="section" style="width: 500px; margin: auto;">
        <QRScanner
            v-bind:qrbox="250"
            v-bind:fps="10"
            style="width: 500px;"
            @result="onScan" />
       
    </div>
    <div>
  <h1>Results</h1>
  <div v-for="(item, index) in items" :key="index">{{item}}</div>
  
  
    </div>
  </div>
  </template>
  
  
  
  <script setup lang="ts">
  import { Html5QrcodeResult } from 'html5-qrcode';
  import QRScanner from './components/QRCodeScanner.vue';
  import { ref } from 'vue';
  
  const items = ref<string[]>([])
    function onScan(decodedText: string, decodedResult: Html5QrcodeResult) {
      items.value.push(decodedText)
      console.log("decodedText", decodedText);
      console.log("decodedResult", decodedResult);
    }
  
  
  </script>
  