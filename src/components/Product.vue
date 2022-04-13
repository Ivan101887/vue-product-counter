<template>
	<main class="main">
		<ul class="product container mx-auto">
			<ProductItem
				v-for="item in data"
				:key="item.name"
				:parent-data="item"
				@update-total="updateTotal"
			/>
			<product-total :parent-data="sum" />
		</ul>
	</main>
</template>
<script>
	import ProductItem from "./ProductItem.vue";
	import ProductTotal from "./ProductTotal.vue";
	export default {
		components: { ProductItem, ProductTotal },
		name: "Product",
		data() {
			return {
				data: [],
				sum: 0,
			};
		},
		async created() {
			try {
				const api = "./data.json";
				const res = await this.$http(api);
				this.data = res.data;
			} catch (e) {
				console.log("資料連接錯誤:\n", e);
			}
		},
		methods: {
			updateTotal(val) {
				this.sum += val;
			},
		},
	};
</script>
<style lang="scss" scoped>
	.product {
		display: grid;
		grid: {
			template-columns: repeat(4, 1fr);
			column-gap: 30px;
			row-gap: 30px;
		}
		margin: {
			top: 25px;
		}
	}
</style>