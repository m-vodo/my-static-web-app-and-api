<script>
import ButtonFooter from '@/components/button-footer.vue';

export default {
  name: 'ProductDetail',
  props: {
    product: {
      type: Object,
      default() {},
    },
  },
  components: { ButtonFooter },
  data() {
    return {
      addMode: false,
      editingProduct: { ...this.product },
    };
  },
  watch: {
    product() {
      if (this.product && this.product.id) {
        this.editingProduct = { ...this.product };
        this.addMode = false;
      } else {
        this.editingProduct = { id: undefined, name: '', description: '' };
        this.addMode = true;
      }
    },
  },
  methods: {
    clear() {
      this.$emit('unselect');
    },
    saveProduct() {
      this.$emit('save', this.editingProduct);
      this.clear();
    },
  },
};
</script>

<template>
  <div class="card edit-detail">
    <header class="card-header">
      <p class="card-header-title">{{ editingProduct.name }}</p>
    </header>
    <div class="card-content">
      <div class="content">
        <div class="field" v-if="editingProduct.id">
          <label class="label" for="id">
            <input
              id="id"
              class="input"
              name="id"
              placeholder="99999"
              readonly
              type="text"
              v-model="editingProduct.id"
            />
            id
          </label>
        </div>
        <div class="field">
          <label class="label" for="name">
            <input
              id="name"
              class="input"
              name="name"
              placeholder="Oranges"
              type="text"
              v-model="editingProduct.name"
            />
            name
          </label>
        </div>
        <div class="field">
          <label class="label" for="description">
            <input
              id="description"
              class="input"
              name="description"
              placeholder="box"
              type="text"
              v-model="editingProduct.description"
            />
            description
          </label>
        </div>
        <div class="field">
          <label class="label" for="quantity">
            <input
              id="quantity"
              class="input"
              name="quantity"
              placeholder="1"
              type="number"
              min="1"
              max="100"
              v-model="editingProduct.quantity"
            />
            quantity
          </label>
        </div>
      </div>
    </div>
    <footer class="card-footer">
      <ButtonFooter
        class="card-footer-item"
        label="Cancel"
        :className="'cancel-button'"
        :iconClasses="'fas fa-undo'"
        :item="editingProduct"
        @clicked="clear"
      ></ButtonFooter>
      <ButtonFooter
        class="card-footer-item"
        :className="'save-button'"
        :iconClasses="'fas fa-save'"
        :item="editingProduct"
        label="Save"
        @clicked="saveProduct"
      ></ButtonFooter>
    </footer>
  </div>
</template>
