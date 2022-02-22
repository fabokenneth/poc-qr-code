<template>
  <h1>{{ msg }}</h1>
  <h3 v-if="isQrScannerLoaded && !isQrCodeScanned"> Scan your QR code</h3>
  <StreamBarcodeReader
    
    @decode="onDecode"
    @loaded="onLoaded"
    class="code-reader"
></StreamBarcodeReader>
  <Modal :show="isQrCodeScanned">
    <template #modal-content>
      <div class="content-wrapper">
        <h2 class="device_title">
          DEVICE INFORMATIONS
        </h2>
        <span>Manufacturer : {{state.qrCodeContent.manufacturer}}</span>
        <span>Model: {{state.qrCodeContent.model}}</span>
        <span>Serial: {{state.qrCodeContent.serial}}</span>
      </div>
    </template>
  </Modal>
</template>

<script>
import {computed, defineComponent, reactive} from "vue";
import { StreamBarcodeReader } from "vue-barcode-reader";
import Modal from "./Modal.vue";

export default defineComponent({
  components: {
    Modal,
    StreamBarcodeReader,
  },
  props: {
    msg: {
      type: String,
      required: true,
    },
  },
  setup: (props) => {

const state = reactive({
  scannerLoaded: false,
  scanningDone: false,
  qrCodeContent: {},

})

const isQrScannerLoaded = computed(() => state.scannerLoaded);

const isQrCodeScanned = computed(() => state.scanningDone)

const onDecode = (value) => {
  console.log(value);
  state.qrCodeContent = JSON.parse(value)
  state.scanningDone = true;
};
const onLoaded = () => state.scannerLoaded = true;

    return {
      state,
      isQrScannerLoaded,
      isQrCodeScanned,
      onDecode,
      onLoaded
    };
  }
});
</script>

<style  scoped>
a {
  color: #42b983;
}
.code-reader::v-deep .overlay-element {
  display: none !important;
}

.content-wrapper{
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 400px;
  padding: 15px;
}
</style>
