<template>
    <div class="">
        <Tabs value="0">
            <TabList>
                <Tab value="0">VALUES</Tab>
                <Tab value="1">IPO UPDATE</Tab>
            </TabList>
            <TabPanels>
                <TabPanel value="0">
                    <div class="">
                        <div class="py-5 px-2">
                            <h2 class="text-xl font-bold mb-4">{{ props.values.ipoName }}</h2>
                            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                                <div class="flex ">
                                    <span class="font-medium">IPO Symbol:</span>
                                    <span class="px-2">{{ props.values.ipoSymbol }}</span>
                                </div>
                                <div class="flex ">
                                    <span class="font-medium">ISIN:</span>
                                    <span class="px-2">{{ props.values.isin }}</span>
                                </div>
                                <div class="flex ">
                                    <span class="font-medium">Issue Type:</span>
                                    <span class="px-2">{{ props.values.issueType }}</span>
                                </div>
                                <div class="flex ">
                                    <span class="font-medium">Start Date:</span>
                                    <span class="px-2">{{ props.values.biddingStartDate }}</span>
                                </div>
                                <div class="flex">
                                    <span class="font-medium">End Date:</span>
                                    <span class="px-2">{{ props.values.biddingEndDate }}</span>
                                </div>
                                <div class="flex ">
                                    <span class="font-medium">Min Price:</span>
                                    <span class="px-2">₹ {{ props.values.minPrice }} .00</span>
                                </div>
                                <div class="flex ">
                                    <span class="font-medium">Max Price:</span>
                                    <span class="px-2">₹ {{ props.values.maxPrice }} .00</span>
                                </div>
                                <div class="flex ">
                                    <span class="font-medium">Lot Size:</span>
                                    <span class="px-2">{{ props.values.lotSize }}</span>
                                </div>
                                <div class="flex ">
                                    <span class="font-medium">Registrar:</span>
                                    <span class="px-2">{{ props.values.registrar }}</span>
                                </div>
                                <div class="flex ">
                                    <span class="font-medium">Entry Date:</span>
                                    <span class="px-2">{{ props.values.entryDate }}</span>
                                </div>
                                <div class="flex">
                                    <span class="font-medium">Entry Time:</span>
                                    <span class="px-2">{{ props.values.entryTime }}</span>
                                </div>
                                <div class="flex">
                                    <span class="font-medium">Sub Type:</span>
                                    <span class="px-2">{{ props.values.subType }}</span>
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
                        <div class="flex justify-center py-2 px-6 max-w-lg w-full">
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

                        <div class="flex justify-center py-2 px-6 max-w-lg w-full">
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

                        <div class="flex justify-center py-2 px-6 max-w-lg w-full">
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

                        <div class="flex flex-col gap-6 py-2 px-6 max-w-lg w-full">
                            <label for="CompanyLogo" class="font-semibold">Company Logo</label>
                            <div class="flex flex-col gap-2 py-3 w-full border border-gray-300 rounded-md">
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

                        <div class="flex flex-col gap-6 py-2 px-6 max-w-lg w-full">
                            <label for="PdfUpload" class="font-semibold">Upload PDF</label>
                                         <div class="flex flex-col gap-2 py-3 w-full border border-gray-300 rounded-md">
                                <Toast />
                            <FileUpload
                                ref="pdfupload"
                                mode="basic"
                                name="pdf[]"
                                url="/api/upload"
                                accept="application/pdf"
                                :maxFileSize="2000000"
                                @upload="onPdfUpload"
                                class="border rounded-md shadow-sm p-2"
                            />
                            </div>
                        </div>

                        <div class="flex flex-col gap-6 items-center justify-center py-4 px-6 max-w-lg w-full">
                            <div class="flex flex-col gap-2 w-full">
                                <Button 
                                    label="SUBMIT" 
                                    @click="submitData" 
                                    :style="{ backgroundColor: isSubmitEnabled ? '#059669' : '#ccc' }" 
                                    :disabled="!isSubmitEnabled"
                                />
                            </div>
                        </div>
                    </div>
                </TabPanel>
            </TabPanels>
        </Tabs>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import Tabs from 'primevue/tabs';
import TabList from 'primevue/tablist';
import Tab from 'primevue/tab';
import TabPanels from 'primevue/tabpanels';
import TabPanel from 'primevue/tabpanel';
import Toast from 'primevue/toast';
import FileUpload from 'primevue/fileupload';
import Button from 'primevue/button';
import InputText from 'primevue/inputtext';
import Textarea from 'primevue/textarea';

const props = defineProps({
    values: {
        type: Object,
        default: () => ({})
    },
});

const fileupload = ref();
const pdfupload = ref();
const Subscription = ref('');
const Strength = ref('');
const Weakness = ref('');

const isSubmitEnabled = computed(() => {
    return Subscription.value || Strength.value || Weakness.value || fileupload.value.files.length > 0 || pdfupload.value.files.length > 0;
});

const onUpload = () => {
    toast.add({
        severity: 'info',
        summary: 'Success',
        detail: 'File Uploaded',
        life: 3000,
    });
};

const onPdfUpload = () => {
    toast.add({
        severity: 'info',
        summary: 'Success',
        detail: 'PDF Uploaded',
        life: 3000,
    });
};

const submitData = async () => {
    const companyLogo = await getBase64(fileupload.value.files[0]);
    const pdfFile = await getBase64(pdfupload.value.files[0]);

    const data = {
        symbol: props.values.ipoSymbol,
        isin: props.values.isin,
        subscription: Subscription.value,
        strength: Strength.value,
        weakness: Weakness.value,
        companyLogo: companyLogo,
        rhp_url: pdfFile
    };

    try {
        const response = await fetch('https://ipo.gwcindia.in/nse-api/api-ipo-details-update.php', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
                'Cookie': 'PHPSESSID=58ms57q01adt66dtbuj3d42era'
            },
            body: JSON.stringify(data)
        });

        if (response.ok) {
            toast.add({
                severity: 'success',
                summary: 'Success',
                detail: 'Data submitted successfully',
                life: 3000,
            });
        } else {
            throw new Error('Failed to submit data');
        }
    } catch (error) {
        toast.add({
            severity: 'error',
            summary: 'Error',
            detail: error.message,
            life: 3000,
        });
    }
};

const getBase64 = (file) => {
    return new Promise((resolve, reject) => {
        const reader = new FileReader();
        reader.readAsDataURL(file);
        reader.onload = () => resolve(reader.result);
        reader.onerror = (error) => reject(error);
    });
};
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
