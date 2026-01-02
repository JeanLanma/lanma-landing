<template>
  <section id="contacto" class="py-24 bg-white overflow-hidden">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="relative bg-lanma-dark rounded-3xl shadow-2xl overflow-hidden lg:grid lg:grid-cols-2 lg:gap-4">
        
        <div class="pt-10 pb-12 px-6 sm:pt-16 sm:px-16 lg:py-16 lg:pr-0 xl:py-20 xl:px-20">
          <div class="lg:self-center">
            <h2 class="text-3xl font-extrabold text-white sm:text-4xl">
              <span class="block">¿Listo para ordenar tu operación?</span>
            </h2>
            <p class="mt-4 text-lg leading-6 text-blue-200">
              Déjanos entender tu negocio. Cuéntanos cuál es tu mayor dolor operativo hoy y te diremos cómo la tecnología puede resolverlo.
            </p>
            <div class="mt-8 text-base text-blue-200">
                <p>O envíanos un correo directo a:</p>
                <a href="mailto:contacto@lanmatech.com" class="font-bold text-white hover:text-lanma-accent transition-colors">contacto@lanmatech.com</a>
            </div>
          </div>
        </div>

        <div class="relative pt-10 pb-12 px-6 sm:pt-16 sm:px-16 lg:py-16 lg:pl-8 xl:py-20 xl:px-20 bg-gray-50 lg:bg-transparent">
            
            <div v-if="status === 'success'" class="bg-white rounded-xl p-8 text-center h-full flex flex-col justify-center items-center">
                <div class="w-16 h-16 bg-green-100 rounded-full flex items-center justify-center mb-4">
                    <span class="text-3xl">✅</span>
                </div>
                <h3 class="text-2xl font-bold text-lanma-dark">¡Mensaje Recibido!</h3>
                <p class="text-gray-500 mt-2">Gracias, {{ form.name }}. Analizaremos tu caso y te contactaremos en breve.</p>
                <button @click="resetForm" class="mt-6 text-lanma-primary font-medium hover:underline">Enviar otro mensaje</button>
            </div>

            <form v-else @submit.prevent="handleSubmit" class="bg-white rounded-xl shadow-xl p-8 space-y-6">
                
                <div>
                  <label for="name" class="block text-sm font-medium text-gray-700">Nombre Completo</label>
                  <input v-model="form.name" type="text" id="name" required 
                         class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-lanma-primary focus:ring-lanma-primary sm:text-sm px-4 py-3 bg-gray-50 border"
                         placeholder="Ej. Jean Desarrollador" />
                </div>

                <div>
                  <label for="email" class="block text-sm font-medium text-gray-700">Correo Electrónico</label>
                  <input v-model="form.email" type="email" id="email" required 
                         class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-lanma-primary focus:ring-lanma-primary sm:text-sm px-4 py-3 bg-gray-50 border"
                         placeholder="jean@empresa.com" />
                </div>

                <div>
                  <label for="message" class="block text-sm font-medium text-gray-700">¿Cuál es tu desafío actual?</label>
                  <textarea v-model="form.message" id="message" rows="4" required 
                            class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-lanma-primary focus:ring-lanma-primary sm:text-sm px-4 py-3 bg-gray-50 border"
                            placeholder="Ej. Mis inventarios no cuadran y pierdo tiempo en Excel..."></textarea>
                </div>

                <button type="submit" :disabled="status === 'loading'" 
                        class="w-full flex justify-center py-3 px-4 border border-transparent rounded-md shadow-sm text-sm font-medium text-white bg-lanma-primary hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-lanma-primary transition-all disabled:opacity-50 disabled:cursor-not-allowed">
                    <span v-if="status === 'loading'">Enviando...</span>
                    <span v-else>Solicitar Diagnóstico</span>
                </button>
            </form>

        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, reactive } from 'vue';

const status = ref('idle'); // idle, loading, success, error
const form = reactive({
    name: '',
    email: '',
    message: ''
});

const handleSubmit = async () => {
    status.value = 'loading';
    
    // SIMULACIÓN DE ENVÍO (Aquí conectarás tu API Laravel luego)
    // Por ahora, simulamos que tarda 1.5 segundos en llegar
    setTimeout(() => {
        console.log('Formulario enviado:', form);
        status.value = 'success';
    }, 1500);
};

const resetForm = () => {
    form.name = '';
    form.email = '';
    form.message = '';
    status.value = 'idle';
};
</script>