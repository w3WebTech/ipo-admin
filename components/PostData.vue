<template>
    <div class="">
        <Tabs value="0">
            <TabList>
                <Tab value="0">VALUES</Tab>
                <Tab value="1">IPO UPDATE</Tab>
                
            </TabList>
            <TabPanels>
              <TabPanel value="0">
    <div class="card">
        <div class="p-4">
            <h2 class="text-xl font-bold mb-4">{{ props.values.ipoName }}</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                <div class="flex ">
                    <span class="font-medium">IPO Symbol:</span>
                    <span  class="px-2">{{ props.values.ipoSymbol }}</span>
                </div>
                <div class="flex ">
                    <span class="font-medium">ISIN:</span>
                    <span  class="px-2">{{ props.values.isin }}</span>
                </div>
                <div class="flex ">
                    <span class="font-medium">Issue Type:</span>
                    <span  class="px-2">{{ props.values.issueType }}</span>
                </div>
                <div class="flex ">
                    <span class="font-medium">Start Date:</span>
                    <span  class="px-2">{{ props.values.biddingStartDate }}</span>
                </div>
                <div class="flex">
                    <span class="font-medium">End Date:</span>
                    <span  class="px-2">{{ props.values.biddingEndDate }}</span>
                </div>
                <div class="flex ">
                    <span class="font-medium">Min Price:</span>
                    <span class="px-2">₹ {{ props.values.minPrice }} .oo</span>
                </div>
                <div class="flex ">
                    <span class="font-medium">Max Price:</span>
                    <span class="px-2">₹ {{ props.values.maxPrice }} .00</span>
                </div>
                <div class="flex ">
                    <span class="font-medium">Lot Size:</span>
                    <span  class="px-2">{{ props.values.lotSize }}</span>
                </div>
                <div class="flex ">
                    <span class="font-medium">Registrar:</span>
                    <span  class="px-2">{{ props.values.registrar }}</span>
                </div>
                <div class="flex ">
                    <span class="font-medium">Entry Date:</span>
                    <span  class="px-2">{{ props.values.entryDate }}</span>
                </div>
                <div class="flex">
                    <span class="font-medium">Entry Time:</span>
                    <span  class="px-2">{{ props.values.entryTime }}</span>
                </div>
                <div class="flex">
                    <span class="font-medium">Sub Type:</span>
                    <span  class="px-2">{{ props.values.subType }}</span>
                </div>
                <div class="flex">
                    <span class="font-medium">Cutoff Price:</span>
                    <span class="px-2"> ₹ {{ props.values.cutOffPrice }} .00</span>
                </div>
                
            </div>
        </div>
    </div>
</TabPanel>
                <TabPanel value="1">
                    <div class="l">
    
     
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
                </TabPanel>
                
            </TabPanels>
        </Tabs>
    </div>
</template>

<script setup>
import { ref } from 'vue';

import Tabs from 'primevue/tabs';
import TabList from 'primevue/tablist';
import Tab from 'primevue/tab';
import TabPanels from 'primevue/tabpanels';
import TabPanel from 'primevue/tabpanel';



const props = defineProps({
  values: {
    type: Object, // Change type to Object
    default: () => ({}) // Default to an empty object
  },
});
console.log(props.values,"values")
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
  
.card {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 16px;
  margin: 16px 0;

  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}


label {
  font-size: 1rem;
  font-weight: 600;
  color: #333;
}


input,
textarea {
  padding: 8px;
  border-radius: 4px;
  border: 1px solid #d1d5db;
  font-size: 1rem;
  width: 100%;
  box-sizing: border-box;
}


.file-upload-button {
  padding: 10px 16px;
  border: 1px solid #d1d5db;
  border-radius: 4px;
}

.max-w-lg {
  max-width: 800px;
}
</style>