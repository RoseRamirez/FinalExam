<template>
  <div>
    <Layout>
      <div class="flex justify-center w-full">
        <div class="bg-white flex flex-col w-1/3 mt-20 p-6">
          <div class="flex flex-row justify-between">
            <h2 class="text-lg">Stock Form</h2>

            <inertia-link :href="route('stock.destroy', form.id)" method="delete">
              Delete
            </inertia-link>
          </div>

          <form id="stock-form" name="stock-form" v-on:submit.prevent="submit">

        <div class="flex flex-col pt-6">
                            <label for="id">ID</label>
                            <input
                                type="text"
                                id="id"
                                name="id"
                                v-model="form.id"
                                autocomplete="off"
                                readonly
                            />
                            <div class="text-red-700 text-sm">
                                {{ errors.id }}
                            </div>
                            {{ form.id }}
                        </div>

                        <div class="flex flex-col pt-6">
                            <label for="stock_category_id">Stock Category ID</label>
                            <input
                                type="text"
                                id="stock_category_id"
                                name="stock_category_idid"
                                v-model="form.stock_category_id"
                                autocomplete="off"
                            />
                            <div class="text-red-700 text-sm">
                                {{ errors.stock_category_id }}
                            </div>
                            {{ form.stock_category_id  }}
                        </div>

                        <div class="flex flex-col pt-6">
                            <label for="description">Description</label>
                            <input
                                type="text"
                                id="description"
                                name="description"
                                v-model="form.description"
                                autocomplete="off"
                            />
                            <div class="text-red-700 text-sm">
                                {{ errors.description }}
                            </div>
                        </div>

                        <div class="flex flex-col pt-6">
                            <label for="uom">Stock Category</label>
                            <select name="uom" id="uom" v-model="form.uom">
                                <option value="F">BOWL</option>
                                <option value="R">PK50</option>
                                <option value="D">BX</option>
                                <option value="F">BAG</option>
                                <option value="R">PK</option>
                                <option value="D">KIT</option>
                                <option value="F">CS</option>
                                <option value="R">CM</option>
                                <option value="D">M</option>
                                <option value="F">CTN</option>
                                <option value="R">EA</option>
                                <option value="D">YD</option>
                                <option value="F">SGL</option>
                                <option value="R">GROSS</option>
                                <option value="D">BKT</option>
                                <option value="F">P100</option>
                                <option value="R">PAR</option>
                                <option value="D">RACK</option>
                                <option value="F">FT</option>
                                <option value="R">IN</option>
                                <option value="D">SET</option>
                                <option value="F">GAL</option>
                                <option value="R">RL</option>
                                <option value="D">CRD</option>
                                <option value="F">SQFT</option>
                                <option value="R">TUBE</option>
                                <option value="D">SHT</option>
                                <option value="F">LOT</option>
                                <option value="R">MM</option>
                                <option value="D">M</option>
                                <option value="F">BOWL</option>
                                <option value="R">SET1</option>
                                <option value="D">SET2</option>
                                <option value="F">SET3</option>
                                <option value="R">SET4</option>
                                <option value="D">SET5</option>
                            </select>

                            <div class="text-red-700 text-sm">
                                {{ errors.uom }}
                            </div>
                        </div>

                        <div class="flex flex-col pt-6">
                            <label for="barcode">Barcode</label>
                            <input
                                type="text"
                                id="barcode"
                                name="barcode"
                                v-model="form.barcode"
                            />
                            <div class="text-red-700 text-sm">
                                {{ errors.barcode }}
                            </div>
                        </div>

                       <div class="flex flex-col pt-6">
                            <label for="discontinued">Type</label>
                            <select name="discontinued" id="discontinued" v-model="form.discontinued">
                                <option value="Y">Yes</option>
                                <option value="N">No</option>
                            </select>

                            <div class="text-red-700 text-sm">
                                {{ errors.discontinued }}
                            </div>
                        </div>

                        <div class="flex flex-col pt-6">
                            <button
                                type="submit"
                                class="bg-indigo-800 text-white p-2"
                            >
                                Update
                            </button>
                        </div>
                    </form>
                </div>
            </div>
        </Layout>
    </div>
</template>

<script>
import { ref, reactive } from "vue";
import Layout from "@/Layouts/Authenticated";
import { Inertia } from "@inertiajs/inertia";

export default {
  components: {
    Layout,
  },

  props: {
    errors: Object,
    model: Object,
  },

   setup(props, context) {
    const form = reactive({
      id: props.model.id,
      description: props.model.description,
      stock_category_id: props.model.stock_category_id,
      uom: props.model.uom,
      barcode: props.model.barcode,
      discontinued: props.model.discontinued ,
      
    });

    const submit = () => {
            Inertia.put(route("stock.update", form), form, {
                onSuccess: () => {
                    // Handle success event
                    form.id = null;
                    form.description = null;
                    form.stock_category_id = null,
                    form.uom = null;
                    form.barcode = null;
                    form.discontinued = "N";
                    form.photo_path = null;
                    //   this.reset();
                },
            });
        };

              return {
            form,
            submit,
        };
    },
};
</script>

