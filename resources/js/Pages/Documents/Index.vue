<template>
  <AppLayout>
    <template #header>
      <h2 class="font-semibold text-xl text-gray-800 leading-tight">
        Documents
      </h2>

      <Link :href="route('documents.create')">
        <JetButton>
          New Document
          <svg xmlns="http://www.w3.org/2000/svg" class="ml-3 h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
            <path stroke-linecap="round" stroke-linejoin="round" d="M12 6v6m0 0v6m0-6h6m-6 0H6"/>
          </svg>
        </JetButton>
      </Link>
    </template>

    <div class="py-8">
      <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
        <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">

          <table class="w-full">
            <thead>
              <tr>
                <th class="bg-gray-50 uppercase text-gray-400 border-b text-left px-4 py-2 font-light text-sm w-14">#</th>
                <th class="bg-gray-50 uppercase text-gray-400 border-b text-left px-4 py-2 font-light text-sm">Name</th>
                <th class="bg-gray-50 uppercase text-gray-400 border-b text-left px-4 py-2 font-light text-sm">Description</th>
                <th class="bg-gray-50 uppercase text-gray-400 border-b text-left px-4 py-2 font-light text-sm w-60">&nbsp;</th>
              </tr>
            </thead>

            <tbody>
              <tr v-for="(document, index) in documents" :key="document.id">
                <td class="border-b text-left px-4 py-2 font-normal text-gray-800 text-md">{{ index +1 }}</td>
                <td class="border-b text-left px-4 py-2 font-normal text-gray-800 text-md">{{ document.name }}</td>
                <td class="border-b text-left px-4 py-2 font-normal text-gray-800 text-md">{{ document.description }}</td>
                <td class="border-b text-right px-4 py-2 font-normal text-gray-800 text-md">
                  Show  <Link :href="route('templates.create')">Template</Link>  Delete
                </td>
              </tr>

              <tr v-if="! documents.length">
                <td colspan="4" class="text-center py-6">
                  <span class="text-md text-slate-400">No documents created yed.</span>
                  <br>
                  <Link class="inline-block mt-2" :href="route('documents.create')">
                    <JetButton>
                      Create Document
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 ml-3" viewBox="0 0 20 20" fill="currentColor">
                        <path fill-rule="evenodd" d="M6 2a2 2 0 00-2 2v12a2 2 0 002 2h8a2 2 0 002-2V7.414A2 2 0 0015.414 6L12 2.586A2 2 0 0010.586 2H6zm5 6a1 1 0 10-2 0v2H7a1 1 0 100 2h2v2a1 1 0 102 0v-2h2a1 1 0 100-2h-2V8z" clip-rule="evenodd" />
                      </svg>
                    </JetButton>
                  </Link>
                </td>
              </tr>
            </tbody>
          </table>

        </div>
      </div>
    </div>
  </AppLayout>
</template>

<script>
import AppLayout from "@/Layouts/AppLayout.vue";
import JetButton from "@/Jetstream/Button.vue";
import { Link } from "@inertiajs/inertia-vue3";

export default {
  components: {
    AppLayout,
    JetButton,
    Link,
  },

  props: {
    documents: Array
  }
};
</script>
