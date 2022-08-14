<template>
    <AppLayout>
        <div class="py-8">
            <div class="mx-auto sm:px-6 lg:px-8">
                <h1 class="my-6 text-xl">Perfiles de cargo</h1>
                <p>
                    Lorem Ipsum es simplemente el texto de relleno de las
                    imprentas y archivos de texto. Lorem Ipsum ha sido el texto
                    de relleno estándar de las industrias desde el año 1500,
                    cuando un impresor (N. del T. persona que se dedica a la
                    imprenta) desconocido usó una galería de textos y los mezcló
                    de tal manera que logró hacer un libro de textos especimen.
                </p>
                <!--  <template
                    v-for="(componente, index) in componentes"
                    :key="index"
                >
                    <FieldInput @addfield="addfield" />
                </template> -->

                <!-- CREAR COMPONENTE EN VUE -->
                <transition-group name="list">
                    <div
                        class="my-6 w-full flex justify-center"
                        v-for="input in inputs"
                        :key="input.id"
                    >
                        <input
                            class="w-1/3 inline-block shadow appearance-none border rounded mr-4 py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                            id="username"
                            type="text"
                            placeholder="Username"
                        />
                        <input
                            class="w-1/3 shadow appearance-none border rounded mr-4 py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                            id="username"
                            type="text"
                            placeholder="__Username__"
                        />

                        <button
                            class="w-1/6 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
                            @click="addInput(input)"
                            v-if="!input.state"
                        >
                            Add Others
                        </button>

                        <button
                            class="w-1/6 bg-red-600 hover:bg-red-700 text-white font-bold py-2 px-4 rounded ui button big toggle"
                            v-if="input.state"
                            @click="deleteInput(input)"
                        >
                            Delete
                        </button>
                    </div>
                </transition-group>
            </div>
        </div>
    </AppLayout>
</template>
<script>
import AppLayout from "@/Layouts/AppLayout.vue";
/* import FieldInput from "@/components/FieldInput.vue"; */

export default {
    components: {
        AppLayout,
        /* FieldInput, */
    },
    data() {
        return {
            inputs: [
                {
                    id: crypto.randomUUID(),
                    label: "",
                    input: "",
                    state: false,
                },
            ],
        };
    },
    methods: {
        changeState(input) {
            input.state = true;
        },
        addInput(input) {
            this.inputs.push({
                id: crypto.randomUUID(),
                label: "",
                input: "",
                state: false,
            });

            this.changeState(input);
        },
        deleteInput(fieldSelected) {
            this.inputs = this.inputs.filter(
                (input) => fieldSelected.id !== input.id
            );
        },
    },
};
</script>
<style>
.list-enter-active,
.list-leave-active {
    transition: all 0.5s ease;
}
.list-enter-from,
.list-leave-to {
    opacity: 0;
    transform: translateX(30px);
}
</style>
