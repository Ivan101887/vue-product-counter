<template>
	<li class="productItem">
		<div class="productItem__head">
			<h2 class="productItem__title">{{ parentData.name }}</h2>
			<p class="productItem__desc">{{ parentData.desc }}</p>
			<b class="productItem__price">
				${{ String(parentData.price).replace(/\B(?=(\d{3})+(?!\d))/g, ",") }}
			</b>
		</div>
		<figure class="productItem__body">
			<img
				:src="parentData.src"
				:alt="parentData.name"
				class="productItem__img"
			/>
		</figure>
		<div class="productItem__foot">
			<input
				class="productItem__btn"
				type="button"
				value="-"
				:disabled="counterNum === min"
				@click="counterNum--"
			/>
			<input
				type="text"
				:value="counterNum"
				disabled
				class="productItem__counter"
				@input="$emit('update-total')"
			/>
			<input
				class="productItem__btn"
				type="button"
				value="+"
				:disabled="counterNum === max"
				@click="counterNum++"
			/>
		</div>
	</li>
</template>
<script>
	export default {
		name: "product-item",
		props: {
			parentData: Object,
			parentIndex: Number,
		},
		data() {
			return {
				counterNum: 0,
				max: 5,
				min: 0,
			};
		},
		watch: {
			counterNum(nval, oval) {
				this.$emit("update-total", nval - oval);
			},
		},
	};
</script>
<style lang="scss" scoped>
	.productItem {
		border: 1px solid #ddd;
		padding: 15px;
		&__head {
			text: {
				align: center;
			}
		}
		&__foot {
			text: {
				align: center;
			}
		}
		&__title {
			font: {
				size: 20px;
				weight: 600;
			}
		}
		&__desc {
			margin: {
				top: 24px;
				bottom: 24px;
			}
			font: {
				size: 0.9rem;
			}
		}
		&__img {
			display: block;
			width: 100%;
			height: auto;
		}
		&__price {
			font: {
				size: 42px;
				weight: 600;
			}
			color: #f40077;
		}
		&__btn {
			display: inline-block;
			padding: 7px 15px;
			border: {
				width: 1px;
				style: solid;
				color: #ddd;
				radius: 3px;
			}
			font: {
				size: 16px;
				weight: 600;
			}
			background: {
				color: transparent;
			}
			cursor: pointer;
			&:disabled {
				cursor: default;
				background: {
					color: #f7f7f7;
				}
				color: #ddd;
			}
		}
		&__counter {
			text: {
				align: center;
			}
			font: {
				size: 22px;
			}
			background: {
				color: transparent;
			}
			width: 120px;
			border: 0;
		}
	}
</style>