<template>
  <!-- <main> -->
  <main class="min-w-screen min-h-screen flex items-center p-5 lg:p-10 overflow-hidden relative hero-section">
    <div class="border-8 border-yellow-20 rounded-lg border-dashed  absolute top-20 bottom-20 left-20 right-20 z-0">
    </div>
    <div class="w-full max-w-4xl rounded-lg bg-white shadow-xl p-10 lg:p-20 mx-auto text-gray-800 relative md:text-left">
      <div class="text-center">
        <div class="text-center px-10">
          <div class="mb-10">
            <div class="w-10 h-10 inline-flex items-center justify-center rounded-full bg-indigo-100 text-black  mb-4">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 my-6 " fill="none" viewBox="0 0 24 24"
                stroke="currentColor" stroke-width="2">
                <path stroke-linecap="round" stroke-linejoin="round"
                  d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12" />
              </svg>
            </div>
            <h2 class="text-2xl leading-7 font-semibold">
              Drop like it's hot
            </h2>
            <p class="mt-3 text-gray-600">
              No limit</p>
            <p class="mt-4 text-gray-500 tracking-wide border-t border-dashed ">Upload or drag & drop your file SVG,
              PNG, JPG or GIF. </p>
          </div>
          <div class="flex flex-col items-center justify-center">
            <form onSubmit="window.location.reload();">
              <label>File
                <input type="file" id="file" ref="file" value="Reset" @change="handleFileUpload" />
              </label>
              <button @click="submitFile"
                class="flex mx-auto mt-16 text-white  border-0 py-2 px-8 focus:outline-none  rounded text-lg btn-style">Upload</button>
            </form>

          </div>

        </div>
      </div>
    </div>
  </main>
  <!-- </main> -->
</template>

<script>
import { Client, Storage, ID } from "appwrite";
const client = new Client();
const storage = new Storage(client);

export { client, storage, };

client
  .setEndpoint('http://localhost:90/v1') // Your API Endpoint
  .setProject('647170480f75d7bd5b41') // Your project ID
  ;

export default {
  name: 'FileUploader',
  data() {
    return {
      file: null,
    };
  },
  methods: {
    handleFileUpload(event) {
      this.file = event.target.files[0];
    },
    async submitFile() {
      try {
        const response = await storage.createFile('64717d445b7a640fc647', ID.unique(), document.getElementById('file').files[0]);
        console.log(response); // Success
      } catch (error) {
        console.log(error); // Failure
      }
    }


  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Work+Sans&display=swap');

.hero-section {
  font-family: 'Work Sans', sans-serif;
  background-color: #5E8AD5;
}

.btn-style {
  background-color: #5E8AD5;
}
</style>