<template>
    <div class="l">
      <div class=" flex justify-center py-2 px-6 max-w-lg w-full text-xl font-bold">IPO UPDATE</div>
      <!-- Subscription Card -->
      <div class=" flex justify-center py-2 px-6 max-w-lg w-full">
        <div class="flex flex-col gap-2 py-2 w-full">
          <label for="Subscription" class="font-semibold">Subscription</label>
          <InputText
            id="Subscription"
            v-model="Subscription"
            size="large"
            aria-describedby="username-help"
            class="p-2 border rounded-md shadow-sm"
          />
        </div>
      </div>
  
      <!-- Strength Card -->
      <div class=" flex justify-center py-2 px-6 max-w-lg w-full">
        <div class="flex flex-col gap-2 w-full">
          <label for="Strength" class="font-semibold">Strength</label>
          <IftaLabel>
            <Textarea
              id="Strength"
              v-model="Strength"
              rows="3"
              cols="30"
              style="resize: none"
              class="p-2 border rounded-md shadow-sm"
            />
          </IftaLabel>
        </div>
      </div>
  

      <div class=" flex justify-center py-2 px-6 max-w-lg w-full">
        <div class="flex flex-col gap-2 w-full">
          <label for="Weakness" class="font-semibold">Weakness</label>
          <IftaLabel>
            <Textarea
              id="Weakness"
              v-model="Weakness"
              rows="3"
              cols="30"
              style="resize: none"
              class="p-2 border rounded-md shadow-sm"
            />
          </IftaLabel>
        </div>
      </div>
  
      <div class=" flex flex-col gap-6 items-center justify-center py-2 px-6 max-w-lg w-full">
        <div class="flex flex-col gap-2 w-full">
          <label for="Weakness" class="font-semibold">Company Logo</label>
          <Toast />
          <FileUpload
            ref="fileupload"
            mode="basic"
            name="demo[]"
            url="/api/upload"
            accept="image/*"
            :maxFileSize="1000000"
            @upload="onUpload"
            class="border rounded-md shadow-sm p-2"
          />
        </div>
      </div>
      <div class=" flex flex-col gap-6 items-center justify-center py-4 px-6 max-w-lg w-full">
        <div class="flex flex-col gap-2 w-full">
         
          <Button label="SUBMIT"  severity="secondary"/>
        </div>
      </div>


  
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const fileupload = ref();
  
  const upload = () => {
    fileupload.value.upload();
  };
  
  const onUpload = () => {
    toast.add({
      severity: 'info',
      summary: 'Success',
      detail: 'File Uploaded',
      life: 3000,
    });
  };
  
  const Subscription = ref('');
  const Strength = ref('');
  const Weakness = ref('');
  </script>
  
  <style scoped>
  /* Global card styling */
  .card {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 16px;
    margin: 16px 0;

    border-radius: 8px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  }
  
  /* Label styling */
  label {
    font-size: 1rem;
    font-weight: 600;
    color: #333;
  }
  
  /* Input and Textarea styling */
  input,
  textarea {
    padding: 8px;
    border-radius: 4px;
    border: 1px solid #d1d5db;
    font-size: 1rem;
    width: 100%;
    box-sizing: border-box;
  }
  
  /* File Upload Button */
  .file-upload-button {
    padding: 10px 16px;
    border: 1px solid #d1d5db;
    border-radius: 4px;
  }
  
  /* Consistent max-width */
  .max-w-lg {
    max-width: 800px;
  }
  </style>
  