<template>
    <div class="px-4 sm:px-4 lg:px-4">
        <div class="mt-8 flow-root">
            <div class="-mx-4 -my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
                <div class="inline-block min-w-full py-2 align-middle sm:px-6 lg:px-8">
                    <div class="overflow-hidden shadow ring-1 ring-black/5 sm:rounded-lg">
                        <div class="flex justify-between items-center p-4">
                            <input
                                type="text"
                                v-model="searchTerm"
                                placeholder="Search..."
                                class="border rounded p-2 focus:outline-none focus:ring-0"
                                aria-label="Search clients"
                            />
                            <Button type="button" label="Add" icon="pi pi-plus" :loading="loading" severity="contrast"/>
                        </div>
                        <DataTable 
                            :value="filteredClients" 
                            showGridlines 
                            class="rounded-md text-sm" 
                            paginator 
                            :rows="10" 
                            :rowsPerPageOptions="[10, 20, 40, 50]"
                        >
                            <Column field="id" header="ID" sortable></Column>
                            <Column field="ipoName" header="Ipo Name" sortable></Column>
                            <Column field="ipoSymbol" header="Ipo Symbol" sortable></Column>
                            <Column field="isin" header="ISIN" sortable></Column>
                            <Column field="lotSize" header="Lot Size" sortable></Column>
                            <Column field="biddingStartDate" header="Start date" sortable></Column>
                            <Column field="biddingEndDate" header="End Date" sortable></Column>
                            <Column field="cutOffPrice" header="Cutoff Price" sortable></Column>
                            <Column header="Action">
                                <template #body="slotProps">
                                    <Button
                                        icon="pi pi-eye"
                                        rounded
                                        aria-label="View client details"
                                        @click.prevent="viewClient(slotProps.data)"
                                        severity="secondary"
                                    />
                                </template>
                            </Column>
                            <template #paginatorend>
                                <span>Total Records: {{ filteredClients.length }}</span>
                            </template>
                            <template #empty>
                                <span class="flex justify-center items-center text-center">No Records Found!</span>
                            </template>
                        </DataTable>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, computed, defineProps, defineEmits } from 'vue';
import 'primeicons/primeicons.css';

const props = defineProps({
    people: {
        type: Array,
        default: () => [] // Default to an empty array
    },
});
console.log(props.people,"people")


const emit = defineEmits(['view-client']);
const searchTerm = ref('');

// Computed property for filtered clients based on search term
const filteredClients = computed(() => {
    if (!props.people || !Array.isArray(props.people)) {
        console.error("Invalid data format for 'people'. Expected an array.");
        return [];
    }
    
    return props.people
        .filter(client => 
            Object.values(client).some(value =>
                String(value).toLowerCase().includes(searchTerm.value.toLowerCase())
            )
        )
        .sort((a, b) => new Date(b.RecordDate) - new Date(a.RecordDate)); // Sorting in descending order
});

// Function to handle viewing a specific client

const viewClient = (client) => {
    console.log("Viewing client:", client);
    emit('view-client', client); // Emit an event to open the side panel and pass the client data
};
</script>

<style scoped>
/* Add any additional styles here */
</style>