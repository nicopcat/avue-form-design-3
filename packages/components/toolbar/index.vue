<template>
	<el-header class="toolbar">
		<div v-if="undoRedo">
			<el-button link :icon="RefreshLeft" :disabled="historySteps.index == 0" @click="$emit('undo')">撤销</el-button>
			<el-button link :icon="RefreshRight" :disabled="historySteps.index == historySteps.steps.length - 1"
				@click="$emit('redo')">重做</el-button>
		</div>
		<div style="display: flex; align-items: center; font-weight: bold">
			<iframe
				src="https://ghbtns.com/github-btn.html?user=sscfaith&repo=avue-form-desiglabelPositionn&type=star&count=true"
				frameborder="0" scrolling="0" width="100" height="20" title="GitHub" style="margin-left: 10px"
				v-if="showGithubStar"></iframe>
			<slot name="toolbar-left"></slot>
			<el-button v-if="toolbar.includes('import')" link :icon="Upload" @click="$emit('import')">导入JSON</el-button>
			<el-button v-if="toolbar.includes('generate')" link :icon="Download" @click="$emit('generate')">生成JSON</el-button>
			<el-button v-if="toolbar.includes('preview')" link :icon="View" @click="$emit('preview')">预览</el-button>
			<el-button v-if="toolbar.includes('save')" link type="primary" @click="$emit('save')">保存</el-button>
			<el-button v-if="toolbar.includes('clear')" class="danger" link :icon="Delete" @click="$emit('clear')">清空</el-button>
			<slot name="toolbar-right"></slot>
		</div>
	</el-header>
</template>

<script setup>
// Icon
import {
	RefreshLeft,
	RefreshRight,
	Document,
	Upload,
	Download,
	View,
	Delete,
} from "@element-plus/icons-vue";

// Props
defineProps({
	showGithubStar: {
		type: Boolean,
		default: false,
	},
	undoRedo: {
		// 撤销重做
		type: Boolean,
		default: true,
	},
	toolbar: {
		// 工具栏按钮
		type: Array,
		default: () => {
			return ["import", "generate", "preview", "clear", "save"];
		},
	},
	historySteps: {
		type: Object,
		default: () => {
			return {
				index: 0,
				maxStep: 20,
				steps: [],
				storage: false,
			};
		},
	},
});

defineEmits(["undo", "redo", "import", "generate", "preview", "clear", "save"]);

</script>

<style lang="scss" scoped>
.toolbar {
	width: 100%;
	height: 45px !important;
	display: flex;
	justify-content: space-between;
	align-items: center;
	border-bottom: solid 2px #e4e7ed;
	border-left: 1px solid #e0e0e0;
	border-right: 1px solid #e0e0e0;
}
</style>
