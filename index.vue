new Vue({
    el: '#app',
    template: `
        <div class="row" style="margin-top: 30px;">
            <div class="dropdown col-sm">
                <span>Categoria:</span>
                <select class="form-control form-control-sm" v-model="selectedCategoria">
                    <option value="">Select a Category</option>
                    <option v-for="(produto_obj, produto) in categorias" :value="produto">{{produto}}</option>
                </select>
            </div>
            <div class="dropdown col-sm">
                <span>Produto:</span>
                <select class="form-control form-control-sm" :disabled="produtos.length == 0" v-model="selectedProduto">
                    <option value="">Select a Product</option>
                    <option v-for="(marca_obj, marca) in produtos">{{marca}}</option>
                </select>
            </div>
            <div class="dropdown col-sm">
                <span>Marca:</span>
                <select class="form-control form-control-sm" :disabled="marcas.length == 0" v-model="selectedMarca">
                    <option value="">Select a Branding</option>
                    <option v-for="marca in marcas">{{marca}}</option>
                </select>
            </div>
        </div>
    `,
    data: function() {
        return {
            categorias: {
                "Food": {
                    "Cereals": ["Cereals1", "Cereals2", "Cereals3", "Cereals4"],
                    "Breakfast": ["Breakfast1", "Breakfast2", "Breakfast3", "Breakfast4"],
                    "Launch": ["Launch1", "Launch2", "Launch3", "Launch4"]
                },
                "Wear": {
                    "Jeans": ["Jeans1", "Jeans2", "Jeans3", "Jeans4", "Jeans5", "Jeans6"],
                    "Shoes": ["Shoes1", "Shoes2", "Shoes3", "Shoes4"],
                }
            },
            produtos: [],
            marcas: [],
            selectedCategoria: "",
            selectedProduto: "",
            selectedMarca: ""
        }
    },
    watch: {
        selectedCategoria: function() {
            // Clear previously selected values
            this.produtos = [];
            this.marcas = [];
            this.selectedProduto = "";
            this.selectedMarca = "";
            if (this.selectedCategoria.length > 0) {
                this.produtos = this.categorias[this.selectedCategoria]
            }
        },
        selectedProduto: function() {
            this.marcas = [];
            this.selectedMarca = "";
            if (this.selectedProduto.length > 0) {
                this.marcas = this.categorias[this.selectedCategoria][this.selectedProduto]
            }
        }
    }
})