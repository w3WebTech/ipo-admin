<template>
  <div>
    <button @click="sidebarOpen = true" class="lg:hidden">Open Sidebar</button>

    <TransitionRoot as="template" :show="sidebarOpen">
      <Dialog class="relative z-50 lg:hidden" @close="sidebarOpen = false">
        <TransitionChild as="template" enter="transition-opacity ease-linear duration-300" enter-from="opacity-0"
          enter-to="opacity-100" leave="transition-opacity ease-linear duration-300" leave-from="opacity-100"
          leave-to="opacity-0">
          <div class="fixed inset-0 bg-gray-900/80" />
        </TransitionChild>

        <div class="fixed inset-0 flex">
          <TransitionChild as="template" enter="transition ease-in-out duration-300 transform"
            enter-from="-translate-x-full" enter-to="translate-x-0"
            leave="transition ease-in-out duration-300 transform" leave-from="translate-x-0"
            leave-to="-translate-x-full">
            <DialogPanel class="relative mr-16 flex w-full max-w-xs flex-1">
              <div class="flex grow flex-col gap-y-5 overflow-y-auto bg-indigo-600 px-6 pb-4">
                <div class="flex h-16 shrink-0 items-center">
                  IPO ADMIN
                </div>
                <nav class="flex flex-1 flex-col">
                  <ul role="list" class="flex flex-1 flex-col gap-y-7">
                    <li>
                      <ul role="list" class="-mx-2 space-y-1">
                        <li v-for="item in navigation" :key="item.name">
                          <a :href="item.href"
                            :class="[item.current ? 'bg-indigo-700 text-white' : 'text-indigo-200 hover:bg-indigo-700 hover:text-white', 'group flex gap-x-3 rounded-md p-2 text-sm/6 font-semibold']">
                            <component :is="item.icon"
                              :class="[item.current ? 'text-white' : 'text-indigo-200 group-hover:text-white', 'h-5 w-5 shrink-0']"
                              aria-hidden="true" />
                            {{ item.name }}
                          </a>
                        </li>
                      </ul>
                    </li>
                    <li class="mt-auto">
                      <a href="#" @click.prevent="handleSignOut"
                        class="group -mx-2 flex gap-x-3 rounded-md p-2 text-sm/6 font-semibold text-indigo-200 hover:bg-indigo-700 hover:text-white">
                        <Cog6ToothIcon class="h-5 w-5 shrink-0 text-indigo-200 group-hover:text-white" aria-hidden="true" />
                        Sign out
                      </a>
                    </li>
                  </ul>
                </nav>
              </div>
            </DialogPanel>
          </TransitionChild>
        </div>
      </Dialog>
    </TransitionRoot>

    <div class="hidden lg:fixed lg:inset-y-0 lg:z-50 lg:flex lg:w-72 lg:flex-col">
      <div class="flex grow flex-col gap-y-5 overflow-y-auto bg-indigo-600 px-6 pb-4">
        <div class="items-center text-white font-bold pt-5 text-2xl">
          AP ADMIN
        </div>
        <nav class="flex flex-1 flex-col">
          <ul role="list" class="flex flex-1 flex-col gap-y-7">
            <li>
              <ul role="list" class="-mx-2 space-y-1">
                <li v-for="item in navigation" :key="item.name">
                  <a :href="item.href"
                    :class="[item.current ? 'bg-indigo-700 text-white' : 'text-indigo-200 hover:bg-indigo-700 hover:text-white', 'group flex gap-x-3 rounded-md p-2 text-sm/6 font-semibold']">
                    <component :is="item.icon"
                      :class="[item.current ? 'text-white' : 'text-indigo-200 group-hover:text-white', 'h-5 w-5 shrink-0']"
                      aria-hidden="true" />
                    {{ item.name }}
                  </a>
                </li>
              </ul>
            </li>
            <li class="mt-auto">
              <a href="#" @click.prevent="handleSignOut"
                class="group -mx-2 flex gap-x-3 rounded-md p-2 text-sm/6 font-semibold text-indigo-200 hover:bg-indigo-700 hover:text-white">
                <Cog6ToothIcon class="h-5 w-5 shrink-0 text-indigo-200 group-hover:text-white" aria-hidden="true" />
                Sign out
              </a>
            </li>
          </ul>
        </nav>
      </div>
    </div>

    <div class="lg:pl-72">
      <main class="py-3">
        <div class="px-4 sm:px-6 lg:px-8">
          <div>
            <div class="grid grid-cols-1 sm:hidden">
              <select aria-label="Select a tab" class="col-start-1 row-start-1 w-full" @change="handleTabChange">
                <option v-for="tab in tabs" :key="tab.name" :value="tab.href" :selected="tab.current">{{ tab.name }}</option>
              </select>
              <ChevronDownIcon class="pointer-events-none col-start-1 row-start-1 mr-2 size-5 self-center justify-self-end fill-gray-500" aria-hidden="true" />
            </div>
            <div class="hidden sm:block">
              <div class="border-b border-gray-200 ">
                <nav class="-mb-px flex space-x-8" aria-label="Tabs">
                  <a v-for="tab in tabs" :key="tab.name" :href="tab.href"
                    :class="[tab.current ? 'border-indigo-500 text-indigo-600 text-md' : ' text-md border-transparent text-gray-500 hover:border-gray-300 hover:text-gray-700', 'whitespace-nowrap border-b-2 px-1 py-4 text-sm font-medium']"
                    :aria-current="tab.current ? 'page' : undefined" @click.prevent="setCurrentTab(tab)">
                    {{ tab.name }}
                  </a>
                </nav>
              </div>
            </div>

            <!-- Tab Content Section -->
            <div class="mt-4">
              <div v-if="tabs[0].current">
                <newtable :people="nseData" @view-client="openSidePanel" />
              </div>
              <div v-if="tabs[1].current">
                <bsetable :people="bseData" @view-client="openSidePanel" />
              </div>
            </div>
          </div>
        </div>
      </main>
    </div>
    <TransitionRoot as="template" :show="open">
              <Dialog class="relative z-10 " @close="open = false">
                <div class="fixed inset-0" />

                <div class="fixed inset-0 overflow-hidden">
                  <div class="absolute inset-0 overflow-hidden">
                    <div class="pointer-events-none fixed inset-y-0 right-0 flex max-w-full pl-10 sm:pl-16">
                      <TransitionChild as="template"
                        enter="transform transition ease-in-out duration-500 sm:duration-700"
                        enter-from="translate-x-full" enter-to="translate-x-0"
                        leave="transform transition ease-in-out duration-500 sm:duration-700" leave-from="translate-x-0"
                        leave-to="translate-x-full">
                        <DialogPanel class="pointer-events-auto w-screen max-w-2xl">
                          <div class="flex h-full flex-col overflow-y-scroll bg-white py-6 shadow-xl">
                            <div class="px-4 sm:px-6">
                              <!-- <div class="flex items-start justify-between">
                           
                                <div class="ml-3 flex h-7 items-center">
                                  <button type="button"
                                    class="relative rounded-md bg-white text-gray-400 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2"
                                    @click="open = false">
                                    <span class="absolute -inset-2.5" />
                                    <span class="sr-only">Close panel</span>
                                    <XMarkIcon class="size-6" aria-hidden="true" />
                                  </button>
                                </div>
                              </div> -->
                            </div>
                            <div class="relative mt-6 flex-1 px-2">
                              <!-- <Accortion :questions="selectedClient.questions" > -->
                             <!-- <questiontabs :questions="selectedClient.data" @approve="handleApprove"
                                @reject="handleReject" @updateStatus="handleUpdateStatus" />-->
                              <!-- <questiontabs 
  :questions="selectedClient.data" 
  :pdf-url="selectedClient.pdf"  
  @approve="handleApprove"
  @reject="handleReject"
  @updateStatus="handleUpdateStatus" 
/> -->
<PostData/>


                            </div>
                          </div>
                        </DialogPanel>
                      </TransitionChild>
                    </div>
                  </div>
                </div>
              </Dialog>
            </TransitionRoot>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRouter } from 'vue-router';
import newtable from './components/newtable.vue';
import { Dialog, DialogPanel, TransitionChild, TransitionRoot } from '@headlessui/vue';
import { Cog6ToothIcon, ChevronDownIcon } from '@heroicons/vue/24/outline';

const router = useRouter();
const sidebarOpen = ref(false);
const open = ref(false); // Initialize sidebarOpen as a reactive reference
const nseData = ref([]);
const bseData = ref([]);
const tabs = ref([
  { name: 'NSE', href: '#nse', current: true },
  { name: 'BSE', href: '#bse', current: false },
]);

const navigation = [
  { name: 'Dashboard', href: '#', icon: 'HomeIcon', current: true },
  // Add more navigation items as needed
];

const setCurrentTab = async (selectedTab) => {
  tabs.value.forEach(tab => {
    tab.current = tab.name === selectedTab.name;
  });
  window.location.hash = selectedTab.href;

  // Fetch data based on the selected tab
  if (selectedTab.name === 'NSE') {
    await fetchNSEData();
  } else if (selectedTab.name === 'BSE') {
    await fetchBSEData();
  }
};

const fetchNSEData = async () => {
    try {
        const response = await fetch('https://ipo.gwcindia.in/nse-api/api-ipo-master.php');
        const data = await response.json();
        
        // Combine the open, closed, and upcoming arrays into one
        nseData.value = [
            ...data.open,      // Spread the open array
            ...data.closed,    // Spread the closed array
            ...data.upcoming   // Spread the upcoming array
        ];
        
        console.log(nseData.value, "Combined nseData"); // Log the combined data
    } catch (error) {
        console.error('Error fetching NSE data:', error);
    }
};

const bseApiUrl = 'https://ipo.gwcindia.in/api/bse/v1/ipolist';

const fetchBSEData = async () => {
  try {
    const response = await fetch(bseApiUrl, {
      method: 'GET',
      headers: {
        'Authorization': '21279C8DC0753CD1A90DEBF3C1C5CEDB8B5B77E0455EE804C9CA03BB706CD02A'
      }
    });
    
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }

    const data = await response.json();
  console.log(data,"data")
    bseData.value = [
      ...data.metaData.open,      // Spread the open array
      ...data.metaData.closed,    // Spread the closed array
      ...data.metaData.upcoming   // Spread the upcoming array
    ];
  } catch (error) {
    console.error('Error fetching BSE data:', error);
  }
};

// Call fetchNSEData when the component is mounted
onMounted(() => {
  fetchNSEData(); // Fetch NSE data by default
});
const openSidePanel = (client) => {
  console.log("Selected Client: ", client); // Debugging
  open.value = true;

  // Open the side panel
};

const handleSignOut = () => {
  console.log("Sign out clicked");
  localStorage.removeItem('email');
  localStorage.removeItem('password');
  router.push('/'); // Adjust the path to your login page
};

</script>

<style scoped>
/* Add any additional styles here */
</style>