<template>

  <AppLayout>
    
    <template #header>
      <h2 class="font-semibold text-xl text-gray-800 leading-tight">
        Documents
      </h2>

      <Link :href="route('documents.index')">
        <JetButton>
          Regresar
        </JetButton>
      </Link>
    </template>

    <div class="py-8">
      <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
        <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">

          <form v-on:submit.prevent="save()">
            <div class="p-4">

              <JetValidationErrors/>

              <div class="mb-4">
                <JetLabel value="Name"/>
                <JetInput type="text" class="mt-1 w-full" v-model="form.name"/>
              </div>

              <div class="mb-4">
                <JetLabel value="Description"/>
                <JetInput type="text" class="mt-1 w-full" v-model="form.description"/>
              </div>

              <div class="mb-4">
                <JetLabel value="Document"/>
                <JetSecondaryButton class="mt-1" v-on:click="$refs.document_file.click()" v-if="! form.document">
                  Select document
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 ml-3" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-8l-4-4m0 0L8 8m4-4v12" />
                  </svg>
                </JetSecondaryButton>
                <JetSecondaryButton class="mt-1" v-else v-on:click="form.document = null">
                  {{ form.document && form.document.name }}
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 ml-3" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
                  </svg>
                </JetSecondaryButton>
                <input type="file" class="hidden" ref="document_file" v-on:change="form.document = $event.target.files[0]">
              </div>

              <div class="mt-8">
                <JetButton type="submit" :disabled="form.processing">Guardar</JetButton>
              </div>

            </div>
          </form>

        </div>
      </div>
    </div>

  </AppLayout>

</template>

<script>
import AppLayout from '@/Layouts/AppLayout.vue';
import JetButton from '@/Jetstream/Button.vue';
import JetSecondaryButton from '@/Jetstream/SecondaryButton.vue';
import JetValidationErrors from '@/Jetstream/ValidationErrors.vue';
import JetLabel from '@/Jetstream/Label.vue';
import JetInput from '@/Jetstream/Input.vue';
import { Link } from '@inertiajs/inertia-vue3';

export default {

  components: {
    AppLayout,
    JetButton,
    JetLabel,
    JetInput,
    Link,
    JetSecondaryButton,
    JetValidationErrors
  },

  data() {

    return {

      form: this.$inertia.form({

        name: '',
        description: '',
        document: ''

      })

    }

  },

  methods: {

    save() {

      this.form.post(route('documents.store'), {
        preserveScroll: true,
      })

    }

  }


}
</script>