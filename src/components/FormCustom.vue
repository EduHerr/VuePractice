<template>
  <form @submit.prevent="handleSubmit" class="space-y-4">
    <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
      <div>
        <label class="block mb-2">Nombre</label>
        <input v-model="formData.nombre" type="text" name="nombre"
          class="w-full p-2 border border-gray-300 rounded focus:outline-none focus:ring-2 focus:ring-blue-500" />
        <p v-if="errors.nombre" class="text-red-500 text-sm">{{ errors.nombre }}</p>
      </div>
      <div>
        <label class="block mb-2">DOB</label>
        <input v-model="formData.dob" type="date" name="dob"
          class="w-full p-2 border border-gray-300 rounded focus:outline-none focus:ring-2 focus:ring-blue-500" />
        <p v-if="errors.dob" class="text-red-500 text-sm">{{ errors.dob }}</p>
      </div>
      <div>
        <label class="block mb-2">RFC</label>
        <input v-model="formData.rfc" type="text" name="rfc"
          class="w-full p-2 border border-gray-300 rounded focus:outline-none focus:ring-2 focus:ring-blue-500" />
        <p v-if="errors.rfc" class="text-red-500 text-sm">{{ errors.rfc }}</p>
      </div>
      <div>
        <label class="block mb-2">C.P.</label>
        <input v-model="formData.cp" type="text" name="cp"
          class="w-full p-2 border border-gray-300 rounded focus:outline-none focus:ring-2 focus:ring-blue-500" />
        <p v-if="errors.cp" class="text-red-500 text-sm">{{ errors.cp }}</p>
      </div>
      <div>
        <label class="block mb-2">Dirección</label>
        <input v-model="formData.direccion" type="text" name="direccion"
          class="w-full p-2 border border-gray-300 rounded focus:outline-none focus:ring-2 focus:ring-blue-500" />
        <p v-if="errors.direccion" class="text-red-500 text-sm">{{ errors.direccion }}</p>
      </div>
      <div>
        <label class="block mb-2">Prod. Fav.</label>
        <select v-model="formData.prodFav" name="prodFav"
          class="w-full p-2 border border-gray-300 rounded focus:outline-none focus:ring-2 focus:ring-blue-500">
          <p v-if="errors.prodFav" class="text-red-500 text-sm">{{ errors.prodFav }}</p>
          <option value="">Seleccione un producto</option>
          <option value="Producto A">Producto A</option>
          <option value="Producto B">Producto B</option>
        </select>
        <p v-if="errors.prodFav" class="text-red-500 text-sm">{{ errors.prodFav }}</p>
      </div>
      <div>
        <label class="block mb-2">Beneficio</label>
        <select v-model="formData.beneficio" name="beneficio"
          class="w-full p-2 border border-gray-300 rounded focus:outline-none focus:ring-2 focus:ring-blue-500">
          <option value="">Seleccione un beneficio</option>
          <option value="descuento">10% descuento</option>
          <option value="gratis">Producto gratis</option>
        </select>
        <p v-if="errors.beneficio" class="text-red-500 text-sm">{{ errors.beneficio }}</p>
      </div>
      <div>
        <label class="block mb-2">Mail</label>
        <input v-model="formData.mail" type="email" name="mail"
          class="w-full p-2 border border-gray-300 rounded focus:outline-none focus:ring-2 focus:ring-blue-500" />
        <p v-if="errors.mail" class="text-red-500 text-sm">{{ errors.mail }}</p>
      </div>
      <div>
        <label class="block mb-2">Celular</label>
        <input v-model="formData.celular" type="text" name="celular"
          class="w-full p-2 border border-gray-300 rounded focus:outline-none focus:ring-2 focus:ring-blue-500" />
        <p v-if="errors.celular" class="text-red-500 text-sm">{{ errors.celular }}</p>
      </div>
    </div>
    <button type="submit" class="bg-blue-500 text-white py-2 px-4 rounded hover:bg-blue-600 transition">
      Enviar
    </button>
  </form>
</template>

<script lang="ts">
import { defineComponent, reactive } from 'vue';

export default defineComponent({
  name: 'FormCustom',
  setup(_, { emit }) {
    const formData = reactive({
      nombre: '',
      dob: '',
      rfc: '',
      cp: '',
      direccion: '',
      prodFav: '',
      beneficio: '',
      mail: '',
      celular: ''
    });

    const errors = reactive({
      nombre: '',
      dob: '',
      rfc: '',
      cp: '',
      direccion: '',
      prodFav: '',
      beneficio: '',
      mail: '',
      celular: ''
    });

    const validateForm = () => {
      errors.nombre = formData.nombre ? '' : 'Nombre es requerido';
      errors.dob = formData.dob ? '' : 'Fecha de nacimiento es requerida';
      errors.rfc = formData.rfc ? '' : 'RFC es requerido';
      errors.cp = formData.cp ? '' : 'Código postal es requerido';
      errors.direccion = formData.direccion ? '' : 'Dirección es requerida';
      errors.prodFav = formData.prodFav ? '' : 'Producto favorito es requerido';
      errors.beneficio = formData.beneficio ? '' : 'Beneficio es requerido';
      errors.mail = formData.mail && /^[\w-]+(\.[\w-]+)*@([\w-]+\.)+[a-zA-Z]{2,7}$/.test(formData.mail)
        ? ''
        : 'Email es inválido o requerido';
      errors.celular = formData.celular && /^[0-9]{10}$/.test(formData.celular)
        ? ''
        : 'Celular debe ser de 10 dígitos';

      return Object.values(errors).every(error => !error);
    };

    const clearFormData = () => {
      formData.nombre = '';
      formData.dob = '';
      formData.rfc = '';
      formData.cp = '';
      formData.direccion = '';
      formData.prodFav = '';
      formData.beneficio = '';
      formData.mail = '';
      formData.celular = '';
    };

    const handleSubmit = () => {
      if (validateForm()) {
        emit('form-data', { ...formData });
        clearFormData();
      }
    };

    return {
      formData,
      errors,
      handleSubmit
    };
  }
});
</script>
