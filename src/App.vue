<template>
  <h1 class="text-4xl font-bold text-center text-gray-800">Vue Practice</h1>
  <div className="container mx-auto p-4">
    <div className="grid grid-cols-1 md:grid-cols-2 gap-4 items-center">
      <div className="p-4">
        <FormCustom @form-data="addFormData"></FormCustom>
      </div>
      <div className="p-4">
        <TableCustom :headers="theads" :data="tbody">
          <tr v-for="(row, index) in tbody" :key="index" class="hover:bg-gray-50 transition-colors">
            <td v-for="(cell, i) in row" :key="i" class="px-6 py-4 border-b text-gray-700 text-sm">
              {{ cell }}
            </td>
          </tr>
        </TableCustom>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from "vue-class-component";
import FormCustom from "./components/FormCustom.vue";
import TableCustom from "./components/TableCustom.vue";

@Options({
  components: {
    FormCustom,
    TableCustom
  },
})
export default class App extends Vue {
  theads: string[] = ['Nombre', 'Dob', 'Rfc', 'C.P.', 'Direccion', 'Prod. Fav.', 'Beneficio', 'Mail', 'Celular'];
  tbody: any[] = [];

  addFormData(data: any) {
    this.tbody.push(data);
  }
}
</script>
