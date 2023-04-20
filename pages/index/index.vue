<template>
	<view class="content">
		<view class="menus">
			<view class="menu" v-for="menu in menus" :key="menu._id">
				{{ menu.name }}
			</view>
		</view>
		<button @click="addMenu">新增菜单</button>
	</view>
</template>

<script>
const db = uniCloud.database()

export default {
	data() {
		return {
			menus: [],
		}
	},
	async onLoad() {
		try {
			const { result } = await db.collection('menus').get()
			this.menus = result.data
			console.log(this.menus)
		} catch (e) {
			console.log({ e })
			//TODO handle the exception
		}
	},
	methods: {
		async addMenu() {
			try {
				const res = await db.collection('menus').add({
					name: '鱼香肉丝',
					tag: [1, 2, 3],
					mainIngredient: [
						{ name: '猪肉', weight: '200g' },
						{ name: '蒜苗', weight: '150g' },
					],
					secondIngredient: [
						{ name: '生姜', weight: '5g' },
						{ name: '蒜末', weight: '5g' },
					],
					otherIngredient: [
						{ name: '盐', weight: '1/2勺' },
						{ name: '味精', weight: '1/4勺' },
						{ name: '糖', weight: '2勺' },
						{ name: '醋', weight: '3勺' },
					],
				})
				console.log({ res })
			} catch (e) {
				console.log({ e })
				//TODO handle the exception
			}
		},
	},
}
</script>

<style>
.content {
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
}
</style>
