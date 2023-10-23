<template>
  <div>
    <h1>DES Encryption Example</h1>
    <div>
      <label for="inputText">Input Text:</label>
      <input type="text" v-model="inputText" id="inputText" />
    </div>
    <div>
      <button @click="encryptText">Encrypt</button>
      <button @click="decryptText">Decrypt</button>
    </div>
    <div v-if="encryptedText">
      <p>Encrypted Text: {{ encryptedText }}</p>
    </div>
    <div v-if="decryptedText">
      <p>Decrypted Text: {{ decryptedText }}</p>
    </div>
  </div>
</template>

<script>
import CryptoJS from 'crypto-js';

export default {
  data() {
    return {
      inputText: '',
      encryptedText: '',
      decryptedText: '',
      secretKey: 'YourSecretKey', // 56-bit DES key
    };
  },
  methods: {
    encryptText() {
      if (this.inputText) {
        const encrypted = CryptoJS.DES.encrypt(this.inputText, this.secretKey);
        this.encryptedText = encrypted.toString();
      } else {
        this.encryptedText = 'Please enter some text to encrypt.';
      }
    },
    decryptText() {
      if (this.encryptedText) {
        try {
          const decrypted = CryptoJS.DES.decrypt(this.encryptedText, this.secretKey);
          this.decryptedText = decrypted.toString(CryptoJS.enc.Utf8);
        } catch (error) {
          this.decryptedText = 'Decryption failed. Check the secret key.';
        }
      } else {
        this.decryptedText = 'No encrypted text to decrypt.';
      }
    },
  },
};
</script>
